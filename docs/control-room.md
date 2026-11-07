---
layout: page
title: "Control Room"
section: DOCUMENTATION
permalink: /docs/control-room.html
---
{% raw %}
# Control Room

The Control Room is the one place where every setting of every installed module is edited, in game, while the server runs. Changes are collected as *pending edits*, checked by the server, saved, backed up and applied live in one step.

> Visual reference: the `lsc_*` screens in the [design file](design.html); widget-level detail in the [layout reference](layouts/index.html#advanced-groups) (files under `suite/`).

## Who can open it

- **Suite administrators** — SteamID64s in *Lemmy's Core → Access → Suite administrators* (bootstrap the first one in `General\suite.json`, see [Installation](getting-started.html#first-start)). Full access to every module including the Core page.
- **Staff editors** — entries in *Lemmy's Core → Access → Staff editors*. Each lists the modules that person may edit (`AdvancedGroups`, `SpawnSystem`, `AdvancedBanking`, or `*` for all but Core). They never see the Core page.

The server checks access on every request; the client never decides on its own.

## Opening it

| How | Opens |
|---|---|
| **U** (*AG Toggle Admin Mode*) | The module overview |
| **Numpad 9** (*Advanced Banking admin*) | Straight into Advanced Banking |
| ATM → admin button | Straight into Advanced Banking |

The client says hello to the server, the server answers with the list of modules you may edit, and the window opens. If no answer arrives within 3 seconds, Lemmy's Core is not running on the server and a basic fallback editor opens instead — install Core as described in [Installation](getting-started.html).

## The window

```
┌ LEMMY'S SUITE · Control Room ─────────────── ● CONNECTED  REV 12 – Admin 21:04  [X] ┐
│ MODULES          │ [ Search every setting... ] [SHOW ADVANCED] [UNDO] [REDO]          │
│ < ALL MODULES    │ ─────────────────────────────────────────────────────────────────  │
│ GROUP MANAGER    │  ADVANCED GROUPS / PROTECTION                                       │
│                  │  Protection                                                         │
│ SECTIONS         │  Damage rules and protected areas.                                  │
│ Groups           │  ┌ Server-wide PvE                         [ON|OFF]  DEFAULT ┐      │
│ Chat ...      1  │  └ ...                                                        ┘      │
│ Protection    2  │                                                                     │
│ [VERSION HISTORY]│                                                                     │
├──────────────────┴─────────────────────────────────────────────────────────────────────┤
│ ● status line                       3 PENDING  [DISCARD] [REVIEW] [APPLY LIVE]          │
└─────────────────────────────────────────────────────────────────────────────────────────┘
```

- **Header** — connection state and the module's current revision: who applied it last and when.
- **Left rail** — on the overview it is empty; inside a module it shows *ALL MODULES* (back), the module's tools, its sections and *VERSION HISTORY*. An orange number on a section is how many pending edits it holds.
- **Toolbar** — search across every setting of the module; *SHOW ADVANCED* reveals rarely needed settings; *UNDO/REDO* step through your edits (Ctrl+Z / Ctrl+Y).
- **Content** — the settings of the chosen section.
- **Footer** — status messages, the pending count, *DISCARD* (throw away all edits), *REVIEW* (see every change before applying), *APPLY LIVE* (Ctrl+S).

### Overview and navigation

The window opens on the **module overview**: one card per module you may edit, with the number of pending edits on each. Click a card to enter it. *ALL MODULES* or **Esc** goes back; Esc on the overview closes the window. Pending edits are kept per module while you move around, so you can edit Groups, switch to Banking and come back.

Inside **Advanced Groups** the rail also offers **GROUP MANAGER** — every group on the server: members, ranks, tier, leader transfer, rename, disband, teleport.

Zones and server markers are edited directly in their sections (*Safe and no-build zones*, *Map, GPS and markers*) with the [map picker](#map-picker); the older separate zone and marker screens were removed.

## Editing settings

| Control | Used for |
|---|---|
| ON / OFF switch | toggles |
| Edit box | numbers, text, SteamIDs. Numbers outside their range are refused with a message under the box. |
| Choice button | fixed options (ranks, display modes, zone types...) — opens a searchable list |
| Colour box + swatch | `RRGGBB` colours. Click the swatch for the [colour picker](#colour-picker). |
| Multi-line box | lists: class names, words, SteamIDs, positions — one per line |
| **ADD CLASS** | class-name lists: opens a searchable list of every spawnable creature and AI class; each pick adds a line |
| **PICK ON MAP / ADD ON MAP** | positions: opens the [map picker](#map-picker) |
| **PLACE IN WORLD** | 3D objects such as ATMs: [world placement](#world-placement) |
| **MY HEADING** | rotations: uses the direction you are facing |
| **DEFAULT / REVERT** | DEFAULT sets the shipped default; when the value differs from the server, the button reverts it to the server value |

Under each control the row shows the default value, or *Was X – not applied yet* in orange while the edit is pending. Red text means the value is invalid; the section is marked red in the rail and *APPLY LIVE* refuses until it is fixed.

Tags next to a label:

| Tag | Meaning |
|---|---|
| CAREFUL | Can lock players out or change the whole server (for example server-wide PvE, administrator lists). Applying asks for a short note, stored in the history and audit log. |
| RESTART | Saved immediately but used only after the next restart. |
| ADVANCED | Hidden until SHOW ADVANCED. |
| READ ONLY | Shown for reference. |

### Lists

Lists (zones, server markers, ATM placements, tiers, VIP tiers...) show a header with the count and limit, **REVERT LIST** and **+ ADD**. Each record has **UP / DOWN** (order matters for some lists, for example VIP tiers), **COPY**, **DELETE** and **OPEN / CLOSE**. Removing a record can be undone until you apply.

When you add a record that has a position, its placement tool opens at once: the map for zones and markers, world placement for ATMs.

## Map picker

For zones (safe, no-build, PvE, PvP, territory and map areas, as circles or polygons), server markers and spawn points.

- **Click** the map to place the record. Dragging moves the map, the mouse wheel zooms.
- **MY POSITION** places it where you stand.
- The record you are editing is cyan; every other record of the same list is grey, with its radius circle or polygon outline drawn, so overlaps are visible while you place.
- **Polygons:** set the zone's shape to *Polygon*, then **ADD ON MAP** on *Polygon corners* and click around the area. Every click adds a numbered corner and the outline draws as you go. **UNDO POINT** removes the last corner. A polygon needs at least 3 corners.
- Every placement is a pending edit: it can be undone and changes nothing until you apply.

## World placement

For records that are real objects in the world (ATMs): the Control Room closes and a see-through preview follows your crosshair.

| Key | Action |
|---|---|
| Look | moves the preview to where you aim (up to 12 m). The preview itself is ignored, so it never climbs on top of itself. |
| Q / E | rotate |
| Page Up / Page Down | raise / lower |
| Left click | place |
| Backspace | cancel |

While placing, the normal left-click action (firing, hitting) is blocked, so the click only places the object.

The Control Room reopens on the record with its position and rotation filled in, pending until you apply.

## Colour picker

Click the swatch next to any colour setting: 12 hues in 6 shades plus a grey ramp. Click a colour to preview it next to the old value, or type a hex value. **USE COLOUR** (or double-click a swatch) makes it a pending edit.

## Review, apply and history

- **REVIEW** lists every pending change as *before → after*, each with its own REVERT. Changes tagged CAREFUL need a note.
- **APPLY LIVE** sends the changes. The server validates every value again, copies the current files into `History\`, saves, and hot-reloads the module. Everyone online sees the result immediately; other admins with the module open get a banner saying who changed it, and their own pending edits are kept.
- If another admin applied first, nothing is overwritten: you get a conflict message, the page refreshes, your edits stay pending, and you apply again after checking.
- **VERSION HISTORY** lists every saved version (who, when, what, note). **RESTORE** puts that version back live.

Every apply is written to the audit log with the actor's SteamID64, the revision and a summary.

## Keyboard

| Key | Action |
|---|---|
| Ctrl+Z / Ctrl+Y | Undo / redo |
| Ctrl+F | Search |
| Ctrl+S | Apply live |
| Esc | Close dialog → back to overview → close |

{% endraw %}
