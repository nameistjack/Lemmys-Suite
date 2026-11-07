---
layout: page
title: "ag_map_legend.layout — Map legend box"
section: DOCUMENTATION
permalink: /docs/layouts/advanced-groups/hud/ag_map_legend.html
---
{% raw %}
# ag_map_legend.layout — Map legend box

**Mod:** Advanced Groups  
**File:** `AdvancedGroups/gui/layouts/hud/ag_map_legend.layout`  
**Root:** `PanelWidget` `ag_map_legend`, size 260 × 60  
**Widgets:** 4

Legend box at the bottom right of the map, filled from the Map legend list in the Control Room.

## Preview

Wireframe drawn straight from the layout file: positions, sizes, colours and default text are exact. Image widgets appear as dashed placeholders, and anything hidden at start inside the root is left out.

![ag_map_legend](../../../images/layouts/advanced-groups/hud/ag_map_legend.png)

## Loaded by

- `AdvancedGroups/scripts/5_Mission/AdvancedGroups/GUI/Pages/AGPageMarkers.c` line 194

## Widget tree

Positions and sizes are in pixels when the widget uses exact sizing, otherwise they are fractions of the parent (0–1).

| Widget | Type | Position | Size | Text / notes |
|---|---|---|---|---|
| `ag_map_legend` | PanelWidget | 24 96 | 260 × 60 | hidden at start |
| &nbsp;&nbsp;└ `panel_edge` | PanelWidget | 0 0 | 260 × 2 |  |
| &nbsp;&nbsp;└ `txt_title` | TextWidget | 14 10 | 232 × 16 | "MAP LEGEND" |
| &nbsp;&nbsp;└ `host_legend` | WrapSpacerWidget | 14 32 | 232 × 20 |  |

{% endraw %}
