---
layout: page
title: "Keybinds and chat commands"
section: DOCUMENTATION
permalink: /docs/keybinds-and-commands.html
---
{% raw %}
# Keybinds and chat commands

All keys can be changed in the game's *Controls* settings under **Advanced Groups**, **Advanced Banking** and **Herosper Keycards Remastered**.

## Advanced Groups

| Default key | Action | Input name |
|---|---|---|
| O | Open / close the group menu | `UAAGGroupMenu` |
| M | Open / close the map | `UAAGMap` |
| H | Show / hide the HUD | `UAAGHud` |
| Y | Cycle chat channel | `UAAGCycleChannel` |
| T | Ping the spot you look at | `UAAGPing` |
| B | GPS / minimap on or off | `UAAGToggleGPS` |
| U | Open the Control Room (admins and staff editors) | `UAAGAdminMode` |
| K | Cycle 3D markers (all, off, server, group, private, events) | `UAAGToggle3D` |

## Advanced Banking

| Default key | Action | Input name |
|---|---|---|
| Numpad 9 | Open the Control Room on Advanced Banking (banking admins) | `UAIABOpenAdmin` |

At an ATM (empty hands), scroll the mouse wheel to choose the action:

| Action | Key |
|---|---|
| Open Advanced Banking | F |
| Open Banking Administration (banking admins) | F |
| Breach Banking Terminal (robbery) | hold F |

## Herosper Keycards Remastered

| Default key | Action | Input name |
|---|---|---|
| Numpad 6 | Open the keycard raid editor (admins in `EditorAdmins.json`; ignored for everyone else) | `UAKCROpenEditor` |

Placing a door, crate or AI spawn point in the editor: aim with the crosshair, **arrow keys** fine-move (hold **Shift** for faster), **L** follows the crosshair again, **Q/E** rotate, **Page Up/Down** height, **Numpad − / +** or **[ ]** scale, **left click** place, **Backspace** cancel.

## Control Room

| Key | Action |
|---|---|
| Ctrl+Z / Ctrl+Y | Undo / redo |
| Ctrl+F | Search settings |
| Ctrl+S | Apply live |
| Esc | Close dialog → back to the module overview → close |

World placement (ATMs): look to aim, **Q/E** rotate, **Page Up/Down** height, **left click** place, **Backspace** cancel.

## Chat commands

| Command | Does |
|---|---|
| `/chat size 10-24` | Chat font size |
| `/chat width N` / `/chat height N` | Chat box size in pixels |
| `/chat pos X Y` | Chat box position (left, bottom) |
| `/chat fade SECONDS` | Fade messages after this long (0 = never) |
| `/chat time` | Timestamps on or off |
| `/chat reset` | Default chat box |
| `/reply <text>` | Answer the last player who mentioned you in global chat |
| `/votemute <name>` | Start a vote to mute a player (if the server enables it) |

`/chat` settings are saved on your PC.

{% endraw %}
