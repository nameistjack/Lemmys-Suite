---
layout: page
title: "Herosper Keycards Remastered"
section: DOCUMENTATION
permalink: /docs/herosper-keycards-remastered.html
---
{% raw %}
# Herosper Keycards Remastered

A standalone remaster of the Workshop mod **Herosper Keycards** (`2886051760`). It ships Herosper's original models, textures, sounds and server plugin in one mod (Herosper released the mod for anyone to update and publish), makes keycard doors work on DayZ 1.30, and turns every keycard door into a raid: a reward crate, loot tables, AI defence waves, server messages and Discord posts. Everything is set up in game with the raid editor.

It does not need Lemmy's Core, Advanced Groups or Advanced Banking.

[Steam Workshop](https://steamcommunity.com/sharedfiles/filedetails/?id=3751107885) · [Video](https://youtu.be/nTquudUszAM) · [Discord support](https://discord.gg/MnWuw7wZ79)

## Installation

```
-mod=@CF;@HerosperKeycards_Remastered
```

Load it on server and client. It is standalone: **do not** also load the original `@HerosperKeycards` or the old `@HerosperKeycards_130_Fix`. They define the same classes and the game stops with script errors. Existing doors, `config.json` and `KCR_*` files keep working, because every class name is unchanged.

The mod folder holds five PBOs, all signed with the same key (put the `.bikey` in the server `keys\` folder):

| PBO | Contents |
|---|---|
| `HerosperKeycards_Remastered.pbo` | Remastered: 1.30 fixes, raids, raid editor, colour doors and cards |
| `KlimaX_Doors.pbo` | Herosper's door models and textures |
| `RedemptionKeyCards.pbo` | Herosper's keycard and crate models and textures |
| `KeyCardSystem.pbo` | Herosper's door and keycard scripts, alarm sounds |
| `KeyCardSystemServer.pbo` | Herosper's server plugin (door saving and spawning) |

### Packing from source

The four Herosper parts live in `P:\HerosperKeycards_Remastered_Assets\<name>\`. Pack **each folder as its own PBO** with the prefix equal to the folder name (`KlimaX_Doors`, `RedemptionKeyCards`, `KeyCardSystem`, `KeyCardSystemServer`) and **binarize turned off**: the models and door configs are already binarized and their texture paths depend on those prefixes. Packing the whole `_Assets` folder as one PBO gives `Unknown type 'Land_KlimaX_T3Door'` on start. `pack-herosper-remastered.bat` in the projects folder packs all five correctly.

On the first start the server creates `$profile:KeyCardSystem/EditorAdmins.json`. Stop the server, add your SteamID64 and start it again:

```json
{ "AdminSteam64Ids": ["7656119XXXXXXXXXX"] }
```

Files from builds before the rename (`H130_Doors.json`, `H130_LootTables.json`, `H130_Scales.json`) are copied to the new `KCR_*` names on the first start; the old files stay where they are.

## DayZ 1.30 door compatibility

- DayZ 1.30's door action only accepts `BuildingBase` targets. Herosper's keycard doors derive from `Building`, so they stopped opening. Keycard doors now use their own door path; every other door keeps the vanilla 1.30 behaviour.
- The held card and the target door are checked again on the server, and the card is consumed on the server.
- Doors whose objects were deleted (for example while the server shuts down) are removed from KeyCardSystem's list before its timer reaches them, which stops a null-pointer crash on shutdown.

## Doors and keycards

Herosper's mod has three door models and one keycard model; every variant is a texture swap:

| Herosper door | Model | Opened by |
|---|---|---|
| T1 | container door | `RedemptionKeyCard_ASW1` (T1, orange) |
| T2 · T4 · T7 | sliding door — cyan, green, Blackmarket | `ASW2` (T2) · `ASW4` (Green) · `ASW7` (Blackmarket) |
| T3 · T5 · T6 | vault door — red, purple, lime | `ASW3` (T3) · `ASW5` (Purple) · `ASW6` (Lime) |

Remastered adds six colours. Each colour has a sliding **door** (Herosper's T2 model), a **vault** (the T3 model) and a **keycard** (the card model); the card opens both doors of its colour by default:

| Colour | Sliding door | Vault | Keycard |
|---|---|---|---|
| Yellow | `Land_KCR_YellowDoor` | `Land_KCR_YellowVault` | `KCR_KeyCard_Yellow` |
| Blue | `Land_KCR_BlueDoor` | `Land_KCR_BlueVault` | `KCR_KeyCard_Blue` |
| Orange | `Land_KCR_OrangeDoor` | `Land_KCR_OrangeVault` | `KCR_KeyCard_Orange` |
| White | `Land_KCR_WhiteDoor` | `Land_KCR_WhiteVault` | `KCR_KeyCard_White` |
| Pink | `Land_KCR_PinkDoor` | `Land_KCR_PinkVault` | `KCR_KeyCard_Pink` |
| Teal | `Land_KCR_TealDoor` | `Land_KCR_TealVault` | `KCR_KeyCard_Teal` |

They appear in the editor's door class list as *Yellow door*, *Yellow vault* and so on, and any door can still be given its own card list.

**Textures.** The colour cards, doors and vaults use the textures in `HerosperKeycards_Remastered\data\cards\` and `data\doors\` (`<colour>_card_co.paa`, `<colour>_door_co.paa`). To use your own, replace those `.paa` files, or add new ones and change that class's `hiddenSelectionsTextures` line in `config.cpp`. The sliding door and the card have one texture; the vault has two — keep the second (the grey metal part) as it is. Herosper's mod may be updated and republished, so recolours of their textures can ship too.

**Loot.** Add the new cards to your `types.xml` like any item, for example:

```xml
<type name="KCR_KeyCard_Yellow"><nominal>2</nominal><lifetime>3600</lifetime><restock>1800</restock><min>1</min><quantmin>-1</quantmin><quantmax>-1</quantmax><cost>100</cost><flags count_in_cargo="0" count_in_hoarder="0" count_in_map="1" count_in_player="0" crafted="0" deloot="0"/><category name="tools"/><usage name="Military"/></type>
<type name="KCR_KeyCard_Blue"><nominal>2</nominal><lifetime>3600</lifetime><restock>1800</restock><min>1</min><quantmin>-1</quantmin><quantmax>-1</quantmax><cost>100</cost><flags count_in_cargo="0" count_in_hoarder="0" count_in_map="1" count_in_player="0" crafted="0" deloot="0"/><category name="tools"/><usage name="Military"/></type>
```

## How a raid works

1. A player swipes the right keycard. The door opens and stays open for **AUTO CLOSE** seconds.
2. If the door has **AI defence**, defenders spawn in waves. The unlocking player is told to eliminate every defender before the door locks.
3. With **CRATE AFTER AI DEFEATED** on (the default), the reward crate only appears once every defender of every wave is dead. With it off, the crate appears at once and the AI attack while players loot. Doors without AI defence always spawn the crate on unlock.
4. The crate is filled from the door's loot table and is removed when the door locks again.
5. If the door locks before the defenders are dead, the raid **fails**: no more waves, the remaining defenders are removed and no crate appears.
6. A door can only start a new raid after its **raid cooldown**. Unlocking it again during the cooldown gives no crate and no raid, and the player is told how long is left.

Defenders that despawn after **AI REMOVED AFTER** do not count as a win.

## The raid editor

Press **Numpad 6** in game (rebindable under *Settings → Controls → Herosper Keycards Remastered*). The server only answers admins listed in `EditorAdmins.json`; for everyone else the key does nothing.

### Doors tab

The list on the left shows every keycard door by its name (or class and grid), with `C` for a crate and `AI` for AI defence. **NEW DOOR** starts a blank door, **DELETE** removes one. Each door has three sub-tabs.

**DOOR**
- Door class (T1–T7), position, orientation, scale, auto close and close delay.
- **KEYCARDS THAT OPEN IT** — leave empty for the original rule: each Herosper card opens its own tier (`RedemptionKeyCard_ASW1` opens T1 … `ASW7` opens T7). Search and **ADD** any item class instead — a card from another mod, a key, a custom item — and only those open this door. A parent class (for example `KeyCard_ParentBase`) allows every item derived from it.
- **CARD USED UP** — on (default) the card is consumed when the door opens; off makes it reusable.
- **NAME** — used in announcements, Discord posts, the log and the door list, for example *"A secured door was opened at Military Bunker (grid 49 101)"*. Without a name the grid reference is used.
- Saving spawns, moves or replaces the door straight away — no restart.

**CRATE AND LOOT**
- Crate class, position, orientation, scale and loot table (click the button to cycle through tables). Leave the crate class empty for no crate.
- **CRATE AFTER AI DEFEATED** on / off, see [How a raid works](#how-a-raid-works).

**AI DEFENCE**
- **AI DEFENCE** and **ANNOUNCE** (server-wide messages for this door) on / off.
- **AI classes:** type two or more letters in the search box, pick a class in the results and press **ADD** (or double-click). Only creatures that use the game's built-in AI (infected and animals) are listed; an exact class name typed in the box can be added too. **REMOVE** takes the selected class off the door. Each spawn picks one class at random.
- AI per wave, waves, seconds between waves, raid cooldown, AI removed after.
- **Spawn points** (optional): **PLACE IN WORLD** or **ADD MY POSITION**. Each AI picks a random point and appears within **SPREAD AROUND EACH POINT**. Without points, AI appear in a ring between the minimum and maximum distance around the door.
- All waves must arrive at least **30 seconds before the door locks**. A door whose waves do not fit is refused on save with the numbers, for example *"the last wave arrives after 90 s, but the door locks after 60 s"*.

**Where AI spawn.** Every spawn spot is moved onto the game's AI navigation mesh, so defenders never start inside a wall, a rock or an object. Points placed on an upper floor keep their height; the spread only looks for floor at that level. A defender that still falls through a floor is put back where it spawned. Indoors, keep the spread at 1–2 m and place a point in each room.

### Loot tables tab

Named tables, reused by any number of doors.

- **Search items** on the left covers every spawnable item, weapon and magazine. **ADD TO TABLE** or double-click adds it.
- Click an entry on the right to change **MIN QTY**, **MAX QTY** and **CHANCE %**, then **UPDATE ENTRY** — or **REMOVE**.
- **MOST ENTRIES PER CRATE** caps how many entries can drop into one crate (0 = no limit).
- **SAVE TABLE** stores the table; **NEW TABLE** and **DELETE** manage the list.

### Settings tab

Discord webhook on / off and its URL. They are stored in KeyCardSystem's own `config.json` (`enableWebhook`, `webhookURL`), so KeyCardSystem uses the same channel. Saving with the webhook on posts a test message.

## Placing objects

**PLACE IN WORLD** closes the editor and shows the object (door, crate) or a yellow barrel (spawn point) where you aim. Saved spawn points are shown as red barrels; both exist only on your screen.

| Key | Action |
|---|---|
| Crosshair | moves the object to where you aim |
| Arrow keys | fine-move along the ground relative to the camera (0.5 m/s, **Shift** 3 m/s); the object stops following the crosshair |
| L | follow the crosshair again |
| Q / E | rotate |
| Page Up / Page Down | raise / lower |
| Numpad − / + or [ / ] | scale (doors and crates) |
| Left click | place |
| Backspace | cancel |

The aim ignores your own character, your gear and the editor's previews, and keeps the last good spot when the crosshair points at nothing. Arrow-key moves keep the height of the spot; correct it with Page Up / Page Down.

**PREVIEW HERE** shows the door at the typed values. **VIEW IN WORLD** closes the editor and leaves every preview standing; **Backspace** brings the editor back.

## Messages and logs

- **In game** (per door, when ANNOUNCE is on): door unlocked, each wave, threat eliminated (with "the reward crate is unlocked"), raid failed. Players within 300 m are told about the unlocked crate even with ANNOUNCE off.
- **Discord:** door unlocked (with who opened it), defenders deployed, threat defeated, raid failed or ended, crate emptied.
- **`$profile:KeyCardSystem/KCR_Raids.log`:** unlocks, waves, defeats, failures, crates, looting and every editor save with the spawn result, time-stamped.

## Files

All under `$profile:KeyCardSystem/`:

| File | Holds |
|---|---|
| `config.json` | KeyCardSystem's own door list, auto-close times and webhook (written by the editor) |
| `EditorAdmins.json` | SteamID64s allowed to open the editor |
| `KCR_Doors.json` | Per door: name, crate, loot table, AI defence and announce settings |
| `KCR_LootTables.json` | Loot tables |
| `KCR_Scales.json` | Door and crate sizes |
| `KCR_Raids.log` | Raid and editor log |

## Troubleshooting

| Problem | Cause and fix |
|---|---|
| `Unknown type 'Land_KlimaX_T3Door'` (or another `Land_KlimaX_` class) on start | Herosper's parts were packed into one PBO or with the wrong prefix. Pack the four `_Assets` folders as separate PBOs (see *Packing from source*). |
| Script errors about classes defined twice | The original `@HerosperKeycards` or `@HerosperKeycards_130_Fix` is still loaded. Remove it from server and client. |
| Numpad 6 does nothing | Your SteamID64 is not in `EditorAdmins.json`; the server log shows `Editor hotkey ignored for non-admin <id>`. If the *Herosper Keycards Remastered* entry is missing from the Controls menu, the PBO is old — repack and restart the game. |
| Saved door does not appear | Check `KCR_Raids.log`: it lists every save with the spawn result and position. A very small scale (for example 0.4) can make a door hard to spot. |
| AI spawn on the ground floor | Update: older builds dropped every spawn onto the terrain. Place points on the floor you want and keep the spread small. |
| Crate never appears | With CRATE AFTER AI DEFEATED on, every defender must die before the door locks. Raise AUTO CLOSE or lower the waves. |

{% endraw %}
