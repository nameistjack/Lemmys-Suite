---
layout: page
title: Herosper Keycards Remastered
section: COMPANION MOD
permalink: /keycards/
---

# Herosper Keycards Remastered

A load-after add-on for the Workshop mod **Herosper Keycards** (`2886051760`). It makes keycard doors work on DayZ 1.30 and turns every keycard door into a raid. It does not need Lemmy's Core, Advanced Groups or Advanced Banking.

The full guide — every editor field, the placement keys, files and troubleshooting — is in the [documentation]({{ site.baseurl }}/docs/herosper-keycards-remastered.html).

## What a raid looks like

1. A player swipes the right keycard and the door opens for its **auto close** time.
2. AI defenders spawn in waves around the door or at spawn points you placed — on the navigation mesh, so never inside walls, and on the floor you placed them on.
3. The **reward crate** appears once every defender is dead (or straight away, if you switch *crate after AI defeated* off). It is filled from the door's **loot table**.
4. If the door locks before the defenders are dead, the raid fails: defenders are removed and no crate appears.
5. Server-wide messages, Discord posts and `KCR_Raids.log` record the unlock, each wave, the result and the looting. Doors can have a **name** that is used in all of them.

## The raid editor

Press **Numpad 6** in game. Only admins in `$profile:KeyCardSystem/EditorAdmins.json` get an answer.

- **Doors** — door class, position, rotation, scale, auto close, name; crate class, position and loot table; AI classes (search and add), waves, timing, spawn points and cooldown. Saving spawns or moves the door live.
- **Loot tables** — search every item, add it, set min and max quantity and chance per entry.
- **Settings** — Discord webhook, shared with KeyCardSystem's own `config.json`.

Placing objects: aim with the crosshair, **arrow keys** fine-move (Shift faster), **L** back to the crosshair, **Q / E** rotate, **Page Up / Down** height, **Numpad − / +** scale, **left click** place, **Backspace** cancel. Spawn points are shown as glowing spheres.

## Install

```text
-mod=@CF;@HerosperKeycards;@HerosperKeycards_Remastered
```

Load it after Herosper Keycards on server and client; `KeyCardSystemServer.pbo` stays server-only. Remove any older `@HerosperKeycards_130_Fix`. Start once, then add your SteamID64 to `EditorAdmins.json`.
