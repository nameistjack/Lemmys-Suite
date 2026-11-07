---
layout: page
title: Public API
section: FOR MOD AUTHORS
permalink: /api/
---

# Public API

Everything below is server-side and stable: it keeps working across builds unless the version number says otherwise. Don't call `AGServerManager` or `IABBankService` directly. Those are internal and change without notice.

Always check readiness and the version first. The suite starts its modules one tick after `MissionServer` is constructed, so calling from your own constructor is too early.

```c
if (!AGPublicAPI.IsReady() || !AGPublicAPI.SupportsAPIVersion(4)) return;
```

Since the suite mods are optional for you, wrap the calls in `#ifdef AdvancedGroups` / `#ifdef Advanced_Banking` and don't put them in your `requiredAddons`.

## Advanced Groups: `AGPublicAPI` (version 4)

### Groups

```c
AGGroupData GetGroupForPlayer(string steamId)   // copy, or null
AGGroupData GetGroupById(string groupId)        // copy, or null
bool        IsPlayerInGroup(string steamId)
bool        SetGroupCategory(PlayerBase admin, string groupId, string categoryName)
bool        SetGroupColor(PlayerBase leaderOrOfficer, string hexColor)
```

`steamId` is `PlayerIdentity.GetId()`. The returned group is a snapshot, so changing it does nothing. `SetGroupCategory` and `SetGroupColor` run the same permission checks as the in-game buttons.

### Chat

```c
bool SendServerMessage(string message, PlayerBase recipient = null)              // [Server] channel
bool SendGlobalMessage(string senderName, string message, PlayerBase recipient = null)
bool SendGroupMessage(string groupId, string senderName, string message)
```

Leave `recipient` as null to send to everyone. Players can't post in the Server channel, so a message there always comes from a script.

To see or swallow player messages, mod the chat handler. Return `false` from `BeforePlayerMessage` to stop a message, which is how you add your own `/commands`:

```c
modded class AGChatHandler
{
    override bool BeforePlayerMessage(PlayerIdentity sender, int channel, inout string message)
    {
        if (message.IndexOf("/bounty") == 0)
        {
            MyBountyService.Handle(sender, message);
            return false;
        }
        return super.BeforePlayerMessage(sender, channel, message);
    }
}
```

### Markers

```c
// strikeStyle: 0 outline, 1 lines, 2 cross-hatch (API 4). strikeColor "" = circle colour.
bool PlaceGroupMarker(PlayerBase player, string label, int markerType, vector pos,
                      float circleRadius = 0, string hexColor = "", int visibilityState = 2,
                      int strikeStyle = 0, string strikeColor = "")
bool PlacePrivateMarker(PlayerBase player, string label, int markerType, vector pos,
                        float circleRadius = 0, string hexColor = "", int visibilityState = 2,
                        int strikeStyle = 0, string strikeColor = "")
```

These act as if the player placed the marker: group permissions, marker limits and the player circle cap all apply. `visibilityState`: 1 = map only, 2 = map + 3D, 3 = 3D only.

**Event markers** belong to your mod, not to a player. Every player sees them, and they aren't saved in the server config. Use them for anything temporary:

```c
bool PlaceEventMarker(string ownerId, string ownerName, string label, int markerType, vector pos,
                      string hexColor, int displayMode = AG_SVRMARKER_SHOW_ALL,
                      float circleRadius = 0, string circleColor = "",
                      bool drawStrikeLines = false, string strikeColor = "", bool replaceExisting = true)
int  RemoveEventMarkers(string ownerId, string label = "")   // returns how many were removed
int  FindEventMarker(string ownerId, string label = "")      // marker id or -1
```

- `ownerId` may only use `A-Z a-z 0-9 . _ -` and be at most 64 characters. Pick one and keep it, for example `"MyMissionMod"`.
- `label` is at most 96 characters, with no line breaks and no `|`.
- With `replaceExisting`, placing the same owner and label again moves the marker instead of adding another.
- `RemoveEventMarkers(ownerId)` with no label clears all of your markers. Do this in your own cleanup.

This is how Banking marks a robbery:

```c
AGPublicAPI.PlaceEventMarker("AdvancedBanking", "Advanced Banking", "ATM robbery: Chernogorsk",
    AGMarkerType.ROBBER, atmPos, "FF3B30", AG_SVRMARKER_SHOW_ALL, 75, "FF3B30");
// ... later
AGPublicAPI.RemoveEventMarkers("AdvancedBanking", "ATM robbery: Chernogorsk");
```

`markerType` is a value of `AGMarkerType`, from `GENERIC` (0) up to `COUNT - 1`. Values outside that range are rejected. `displayMode` is one of `AG_SVRMARKER_SHOW_ALL`, `_3D`, `_2D` or `_NONE`.

### Zones and territories (new in 4)

```c
bool   IsSafeZone(vector pos)
bool   IsNoBuildZone(vector pos)
string GetTerritoryOwnerAt(vector pos, out string groupId)  // "" when nobody owns it
bool   CanBuildAt(PlayerBase player, vector pos)            // no-build zones + territory rules
```

`GetTerritoryOwnerAt` returns the group name. `groupId` is filled for flag claims and left empty for admin-assigned Territory zones, which are matched by name. `CanBuildAt` is the same check the build and placement actions use, so your own placement action will agree with ours.

### Version history

| Version | Added |
|---|---|
| 2 | markers and event markers |
| 3 | chat helpers and `AGChatHandler` |
| 4 | strike style and colour on player markers; zone and territory queries |

## Advanced Banking: `IABPublicAPI` (version 2)

```c
IABOperationResult CreditPersonal(PlayerBase player, int amount, string reason, string requestId)
IABOperationResult DebitPersonal (PlayerBase player, int amount, string reason, string requestId)
IABOperationResult CreditGroup   (PlayerBase player, int amount, string reason, string requestId)
IABOperationResult DebitGroup    (PlayerBase player, int amount, string reason, string requestId)
IABOperationResult DepositCash   (PlayerBase player, int amount, bool groupAccount, string requestId)
IABOperationResult WithdrawCash  (PlayerBase player, int amount, bool groupAccount, string requestId)
IABOperationResult TransferPersonal(PlayerBase player, string targetSteamId, int amount, string requestId)

int GetPersonalBalance(PlayerBase player)   // -1 if unavailable   (new in 2)
int GetGroupBalance(PlayerBase player)      // -1 without a usable group account (new in 2)
```

`IABOperationResult` has `success`, `code` (for example `INSUFFICIENT_FUNDS`, `BALANCE_LIMIT`, `DAILY_LIMIT`, `ACCOUNT_RESTRICTED`, `DUPLICATE_REQUEST` or `NOT_READY`), `message`, `balance`, `fee` and `transactionId`.

**About `requestId`.** An id that was already used returns `DUPLICATE_REQUEST` instead of paying again, so a reward isn't paid twice when a script fires twice. The server remembers the last `processedRequestLimit` ids per account (default 128). Make it unique per real event and the same for retries of that event:

```c
string requestId = "MyQuests:" + player.GetIdentity().GetId() + ":" + questId;
IABOperationResult r = IABPublicAPI.CreditPersonal(player, 2500, "Quest reward", requestId);
if (!r.success) Print("[MyQuests] payout failed: " + r.code + " " + r.message);
```

Credits and debits go through the same caps, frozen and archived checks, and audit trail as everything else. The `reason` appears in the player's history and the admin log.

## Control Room providers

To put your own mod's settings into the Control Room, write a provider in Lemmy's Core under `scripts/5_Mission/LemmysCore/Providers/`. Wrap it in `#ifdef YourMod` and register it in `LMSProviderBootstrap.EnsureRegistered()`.

```c
class LMSProviderMyMod : LMSConfigProvider
{
    protected ref MyModConfig m_Config;

    override string ModuleId() { return "MyMod"; }
    override string Title() { return "My Mod"; }

    override void Describe(LMSSchemaBuilder s)
    {
        s.Section("general", "General", "What this page controls.");
        s.Toggle("enabled", "Enabled", "Turns the feature on.");
        s.Int("limit", "Limit", "Explain it for a human.", 1, 100, "items");
        s.Choice("mode", "Mode", "Pick one.", "0|Off;1|Normal;2|Hard");
    }

    override bool Load(out string error) { m_Config = MyModLoader.Load(); return m_Config != null; }
    override Class Target(string sectionId) { return m_Config; }
    override Class DefaultTarget(string sectionId) { return Made(new MyModConfig()); }
    override bool Persist(out string error) { return MyModLoader.Save(m_Config); }
    override void Activate(LMSApplyContext context) { MyModService.Get().Reload(); }
    override void ConfigFiles(notnull array<string> paths) { paths.Insert(MyModLoader.PATH); }
}
```

Field keys are your config's member names. Defaults come from `DefaultTarget`, so there's no second copy of them to keep in sync.

Two things that will bite you:

- **Return new objects through `Made(...)`.** Returning `new X()` straight from a method declared as returning `Class` fails to compile ("not strong ref").
- **Store lists of records in `array<ref ...>`, not an `array<ref Class>` of non-managed classes.** For records use `Collection(...)` with `ItemCount`, `ItemAt`, `NewItem`, `ClearItems` and `AppendItem`. String lists use `Words(...)` and convert in `ReadCustom` / `WriteCustom`.
