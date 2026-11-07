---
layout: page
title: "minimap_blip.layout — Minimap blip"
section: DOCUMENTATION
permalink: /docs/layouts/advanced-groups/hud/minimap_blip.html
---
{% raw %}
# minimap_blip.layout — Minimap blip

**Mod:** Advanced Groups  
**File:** `AdvancedGroups/gui/layouts/hud/minimap_blip.layout`  
**Root:** `PanelWidget` `MinimapBlip`, size 14 × 14  
**Widgets:** 3

One teammate or marker dot on the minimap.

## Preview

Wireframe drawn straight from the layout file: positions, sizes, colours and default text are exact. Image widgets appear as dashed placeholders, and anything hidden at start inside the root is left out.

![minimap_blip](../../../images/layouts/advanced-groups/hud/minimap_blip.png)

## Loaded by

- `AdvancedGroups/scripts/4_World/AdvancedGroups/HUD/AGMinimap.c` line 213

## Widget tree

Positions and sizes are in pixels when the widget uses exact sizing, otherwise they are fractions of the parent (0–1).

| Widget | Type | Position | Size | Text / notes |
|---|---|---|---|---|
| `MinimapBlip` | PanelWidget | 0 0 | 14 × 14 | hidden at start |
| &nbsp;&nbsp;└ `BlipDot` | PanelWidget | 0 0 | 6 × 6 |  |
| &nbsp;&nbsp;└ `BlipIcon` | ImageWidget | 0 0 | 14 × 14 | hidden at start |

{% endraw %}
