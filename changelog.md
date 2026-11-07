---
layout: page
title: Changes
section: CHANGELOG
permalink: /changelog/
---

# Changes

Newest first. Entries tagged **untested** compile-checked on our side but haven't had a full in-game run yet. Report anything odd. The full Advanced Groups history before the suite merge is in the [Advanced Groups changelog]({{ site.baseurl }}/docs/reference/CHANGELOG.html).

## Week of 7 November 2026

### Suite
- **Lemmy's Core is now the server-side dependency** of Advanced Groups and Advanced Banking. Load it with `-serverMod`; players don't download it.
- The documentation moved to this site: [Docs]({{ site.baseurl }}/docs/), with every page, setting and layout.

### Advanced Groups (untested)
- **Zones:** one *Safe and no-build zones* section in the Control Room for every zone type. New per-zone **map fill** (outline, strike lines, cross-hatch); **name** and **map icon** are optional. Hatching keeps its spacing at every zoom and is anchored to the map grid.
- The old Command, Config and Zones screens and the Control Room's separate zone and marker map were removed; zones and server markers are edited in their sections with the map picker.
- **HUD:** the group list shows health and blood bars per member and uses the group's tag colour; the minimap shows you as the same arrow as the map.
- World placement: **left click** places (was middle mouse); the preview no longer climbs onto itself.
- Fixed: group tiers showed "0 stored" in the Control Room; Apply Live was blocked by an unchanged invalid marker style; a reserved word broke `AGStyle.c`.

### Advanced Banking
- **ATM robbery fixed:** the breach is now *hold F* (it never showed with empty hands), starting it no longer crashes the server, and the result shows as an on-screen notice. A few seconds of network lag no longer makes a full breach count as too early.
- Withdrawals no longer fail with "server did not answer".
- Old `$profile:Advanced_Banking` config and accounts are adopted into the suite folders.
- Oversized text in the admin page's edit boxes fixed.

### Herosper Keycards Remastered (new, untested)
- Renamed from "1.30 fix"; saved files carry over.
- Raid editor on **Numpad 6** for admins in `EditorAdmins.json`.
- Search-and-add for AI classes and loot items; door names used in all messages.
- Reward crate only after the defenders are dead (switchable); waves must fit inside the door's open time; a raid fails if the door locks first.
- AI spawn on the navigation mesh at the placed floor; fall-through guard.
- Placement with arrow-key fine movement; spheres mark spawn points.
- Fixed: placement could save a spot behind the player; doors saved far from where they were aimed.

## 0.5.0-beta: November 2026

All three mods carry `0.5.0-beta` in their `config.cpp`.

### Fixed during beta testing

- Opening chat threw a NULL-pointer error inside vanilla `UpdateChannel`, because our chat layout has no vanilla channel label. We no longer call it.
- The Control Room's module and section lists on the left stayed empty. They are now laid out after every rebuild.
- The ATM amount check no longer relies on character codes to recognise digits. This is the most likely cause of the "Enter an amount greater than zero" message; if it still appears, the script log now shows exactly what the box contained.
- Chat timing now uses the game's millisecond clock, and the first three chat redraws log their size to the script log, so a blank chat box can be traced.
- Compile fixes: a variable named `owned` (a reserved word), a wrong spawn flag (`ECE_EQUIPPED` → `ECE_EQUIP`) and a `TextWidget.GetText` call that doesn't exist.


### Advanced Groups

**Chat** (untested)
- Long messages wrap onto extra lines instead of being cut off at the box edge.
- The scrollbar can be dragged while chat input is open. It used to ignore the mouse completely.
- The mouse wheel scrolls three lines and Page Up/Down one page. The old version scrolled a percentage of the history, so one wheel tick jumped further the more history you had.
- Turning a channel off in Settings now only hides it. Before, its messages were thrown away and didn't come back.
- Each line fades on its own timer instead of the whole box vanishing after 60 seconds. With chat open, everything is shown.
- A "New messages below" line appears when you have scrolled up and something new arrives.
- New `/chat size | width | height | pos | fade | time | reset` commands for per-player box layout. Saved in your client settings.
- The box keeps inside the screen on resolution changes, and the input bar follows the box.

**Markers** (untested)
- **My position** button in the marker popup. On an existing marker it moves the marker on confirm.
- Players can give group and private markers a circle, up to `playerMarkerMaxRadius` (500 m by default). Admins aren't capped.
- Strike lines have their own button: none, lines or cross-hatch, with six colours. The old toggle was a checkbox called "player tags" that only admins could see.
- The minimap draws the same hatch as the big map instead of a plus sign.

**Zones** (untested)
- The Zones admin page was 1800 px wide and pushed the map off screen, so polygons couldn't really be drawn there. It's now a 540 px panel on the left with the map beside it.
- Undo point, right-click a point to remove it, and **Point at me** / **Centre on me** to build a zone by walking it.
- Area shown while drawing. Polygons whose edges cross are drawn red and refused, on the client and again on the server.
- Zones are drawn with a hatch by type on the map and minimap: cross-hatch for safe zones, lines for rule zones, none for visual ones.
- New zone type **Territory** with an owner group name.
- Enter and leave notices for named zones (`zoneEnterMessages`).

**Safe zones** (untested)
- Players inside a safe zone can no longer shoot players outside it (`safeZoneBlockOutgoing`, on by default). Before, only the victim's position was checked.

**Territories** (new, untested, off by default)
- Building a flagpole claims land for the builder's group. Settings cover radius, distance to other groups, flags per group, owner-only building and dismantling, and moving intruders out on login.
- Claims show on the map and minimap in the group colour. A claim is released when its flag or group is gone.

**Control Room**
- New settings for everything above, plus a hatch style for server markers.

**API 4**
- Strike style and colour on `PlaceGroupMarker` / `PlacePrivateMarker`, plus `IsSafeZone`, `IsNoBuildZone`, `GetTerritoryOwnerAt` and `CanBuildAt`.

**Earlier this cycle**
- Group-hop and rejoin cooldowns, invite cooldown and in-person invites, and banned words in group names and tags.
- Item requirements for the map, compass and teammate visibility, a GPS item list, and a configurable map legend.
- Chat slow mode per channel, channel locks, `/votemute`, and filtered-word mutes. All of these persist across restarts.

### Advanced Banking

- **ATM robbery overhaul:**
  - an alarm in a radius;
  - police alerts by SteamID or group;
  - a map circle through Advanced Groups;
  - the robbery is abandoned when the robber dies, leaves or walks off, and the next robber starts from zero;
  - optional AI defence waves;
  - optional cash pools, so the loot depends on what the ATM actually holds.
- Per-ATM deposit, withdraw and robbery switches.
- VIP tiers: bonus balance cap, bonus paycheck and no transfer fees.
- Group accounts can cost money to open and can grow their cap per member.
- Timed paycheck bonus (`paycheckEventPercent` until `paycheckEventEnds`).
- One-time import of TraderPlus bank balances and currency classes, without TraderPlus installed. Each player is paid once, on their first ATM visit.
- **Deposit all** / **Withdraw all**. The amount field takes digits only, and the balance shows as current / maximum.
- **API 2:** `GetPersonalBalance`, `GetGroupBalance`.
- **Fixed:** the Deposit and Withdraw buttons were missing because one invalid property stopped the layout parser halfway through the file.
- **Fixed:** you could see the game world through the banking panels.

### Lemmy's Core

- **Fixed:** admins were refused by the Control Room even with their ID configured. The module catalog was being sent as an empty `{}`, so the client fell back to the old screen and its "admin id needs to be registered" message.
- **Fixed:** several "not strong ref" compile errors in the config schema and providers.
