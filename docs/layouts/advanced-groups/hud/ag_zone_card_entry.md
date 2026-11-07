---
layout: page
title: "ag_zone_card_entry.layout — Zone card row"
section: DOCUMENTATION
permalink: /docs/layouts/advanced-groups/hud/ag_zone_card_entry.html
---
{% raw %}
# ag_zone_card_entry.layout — Zone card row

**Mod:** Advanced Groups  
**File:** `AdvancedGroups/gui/layouts/hud/ag_zone_card_entry.layout`  
**Root:** `PanelWidget` `rootFrame`, size 360 × 44  
**Widgets:** 3

One zone in the zone panel.

## Preview

Wireframe drawn straight from the layout file: positions, sizes, colours and default text are exact. Image widgets appear as dashed placeholders, and anything hidden at start inside the root is left out.

![ag_zone_card_entry](../../../images/layouts/advanced-groups/hud/ag_zone_card_entry.png)

## Loaded by

- `AdvancedGroups/scripts/5_Mission/AdvancedGroups/GUI/Pages/AGPageAdmin.c` line 788

## Widget tree

Positions and sizes are in pixels when the widget uses exact sizing, otherwise they are fractions of the parent (0–1).

| Widget | Type | Position | Size | Text / notes |
|---|---|---|---|---|
| `rootFrame` | PanelWidget | 0 0 | 360 × 44 |  |
| &nbsp;&nbsp;└ `CardAccent` | PanelWidget | 0 0 | 3 × 44 |  |
| &nbsp;&nbsp;└ `btnSelect` | ButtonWidget | 8 4 | 344 × 36 | "Zone" |

{% endraw %}
