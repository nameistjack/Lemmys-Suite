---
layout: page
title: Setup
section: INSTALL AND RUN
permalink: /setup/
---

# Setup

## What goes where

| Mod | PBO prefix | Server | Client | Needs |
|---|---|---|---|---|
| Community Framework | | `-mod` | yes | |
| Lemmy's Core | `Lemmys_Core` | `-serverMod` | **no** | CF |
| Advanced Groups | `AdvancedGroups` | `-mod` | yes | CF, Lemmy's Core on the server |
| Advanced Banking | `Advanced_Banking` | `-mod` | yes | CF, Lemmy's Core on the server; Groups is optional |
| Herosper Keycards Remastered *(companion)* | `HerosperKeycards_Remastered` | `-mod` | yes | Herosper Keycards (Workshop 2886051760) |

A typical launch line:

```text
Server:  -mod=@CF;@Advanced Groups by Lemmy Maverick;@AdvancedBanking
         -serverMod=@Lemmys_Core
Client:  -mod=@CF;@Advanced Groups by Lemmy Maverick;@AdvancedBanking
```

Use the folder names your mods actually have. Put CF first. Clients must run the exact same Groups and Banking build as the server. Groups checks this on join, and a mismatch shows "client/server version mismatch" in chat.

Copy each client mod's `.bikey` into the server's `keys` folder. Core is server-only and doesn't need its key there.

## Pick what you run

**Groups + Core.** Groups, chat, map, markers, zones, territories and spawn selection, all configured in the Control Room.

**Banking + Core.** Personal accounts, ATMs, robberies and the TraderPlus import. Group accounts are hidden without Groups.

**Full suite.** Groups + Banking + Core: group accounts appear, the ATM checks the player's rank in their group for group deposits, withdrawals and transfers, and robberies show on the Groups map.

On the first start Core copies the old `$profile:AdvancedGroups/` and `$profile:Advanced_Banking/` folders into `$profile:LemmysSuite/` (copies, nothing is deleted). See [Lemmy's Core]({{ site.baseurl }}/core/) for what happens to old files.

## First start checklist

1. Start the server once with nothing configured and let it create the folders and default configs.
2. Stop it. Put your SteamID64 in `LemmysSuite/General/suite.json → adminSteamIds`.
3. Start again and join. Press **U** (or **Numpad 9** for Banking): the Control Room opens.
4. **Banking:** Control Room → Advanced Banking → *ATMs and currency* → **+ ADD ATM**. Aim, rotate with Q / E, **left click** to place, then **APPLY LIVE**. The ATM appears straight away.
5. **Groups:** set up spawn points for your map before enabling spawn selection. The packed points are Chernarus coordinates.
6. Check the server RPT and `LemmysSuite/Logs/` for lines starting with `[AdvancedGroups]`, `[AdvancedBanking]` or `Core`. The migration result is in `General/suite.json → profileState`.

For Herosper Keycards Remastered, see [its page]({{ site.baseurl }}/keycards/).

## Things people get wrong

- **Editing JSON while the server runs.** The server keeps the config in memory and writes it back on the next save, which overwrites your edit. Use the Control Room, or stop the server first.
- **Overwriting profile files with the packed example configs.** `server_config.json` and `spawn_config.json` inside the PBO folder are examples and are never read at runtime.
- **Two copies of the console.** Banking ships its own copy of the Control Room client for servers without Groups. With Groups loaded, Banking's copy switches itself off. You don't need to remove anything.
- **The ATM alarm makes no sound.** `robberyAlarmSoundSet` is empty by default; add the name of a sound set your server has.
- **Territories do nothing.** They are off by default: `territoriesEnabled` in **Advanced Groups → Territories**.
- **Packing from the wrong folder.** Advanced Groups must be packed from `P:\Lemmys_suit\AdvancedGroups`. An older copy elsewhere has the same prefix but lacks the Control Room scripts, and Banking then fails with `Can't find variable 'LSCClient'`.

## Packing the suite yourself

Source folders sit side by side:

```text
P:\Lemmys_suit\
  AdvancedGroups\     → @Advanced Groups by Lemmy Maverick\addons\AdvancedGroups.pbo
  Advanced_Banking\   → @AdvancedBanking\addons\Advanced_Banking.pbo
  Lemmys_Core\        → @Lemmys_Core\addons\Lemmys_Core.pbo
```

In Addon Builder, select each inner folder as the source, not `P:\Lemmys_suit` itself. Keep the prefix from each folder's `$PBOPREFIX$`. Banking has an `exclude.lst`: it keeps the ATM's source `.tga`/`.png`/`.fbx` files and unused texture maps out of the PBO. Those are around 12 MB each, so check the packed size if it looks large. Don't exclude `*.cpp`, because `config.cpp` has to be inside.

Then sign the client PBOs with the same key. Test with a clean client against a clean server before you upload anything.

## Upgrading

1. Stop the server and back up `$profile:LemmysSuite/`, plus the old `AdvancedGroups` and `Advanced_Banking` profile folders if you still have them.
2. Replace server and client mods together.
3. Start and read the log. New settings are added with their defaults. Nothing you set is reset.
4. Rolling back means the old build **and** the profile backup from before the upgrade. An older build may not read files a newer build has migrated.
