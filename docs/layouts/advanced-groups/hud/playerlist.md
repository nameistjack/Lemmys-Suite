---
layout: page
title: "playerlist.layout — Group player list"
section: DOCUMENTATION
permalink: /docs/layouts/advanced-groups/hud/playerlist.html
---
{% raw %}
# playerlist.layout — Group player list

**Mod:** Advanced Groups  
**File:** `AdvancedGroups/gui/layouts/hud/playerlist.layout`  
**Root:** `PanelWidget` `Root`, size 330 × 220  
**Widgets:** 4

On-screen list of group members.

## Preview

Wireframe drawn straight from the layout file: positions, sizes, colours and default text are exact. Image widgets appear as dashed placeholders, and anything hidden at start inside the root is left out.

![playerlist](../../../images/layouts/advanced-groups/hud/playerlist.png)

## Loaded by

- `AdvancedGroups/scripts/4_World/AdvancedGroups/HUD/AGPlayerList.c` line 11

## Widget tree

Positions and sizes are in pixels when the widget uses exact sizing, otherwise they are fractions of the parent (0–1).

| Widget | Type | Position | Size | Text / notes |
|---|---|---|---|---|
| `Root` | PanelWidget | 34 92 | 330 × 220 |  |
| &nbsp;&nbsp;└ `BG` | PanelWidget |  | 330 × 220 |  |
| &nbsp;&nbsp;└ `GroupNameLabel` | TextWidget | 8 6 | 314 × 30 |  |
| &nbsp;&nbsp;└ `MemberRows` | ScrollWidget | 8 42 | 314 × 168 |  |

{% endraw %}
