---
layout: page
title: "ag_map_legend_row.layout — Map legend row"
section: DOCUMENTATION
permalink: /docs/layouts/advanced-groups/hud/ag_map_legend_row.html
---
{% raw %}
# ag_map_legend_row.layout — Map legend row

**Mod:** Advanced Groups  
**File:** `AdvancedGroups/gui/layouts/hud/ag_map_legend_row.layout`  
**Root:** `FrameWidget` `ag_map_legend_row`, size 232 × 22  
**Widgets:** 3

One icon + label row in the map legend.

## Preview

Wireframe drawn straight from the layout file: positions, sizes, colours and default text are exact. Image widgets appear as dashed placeholders, and anything hidden at start inside the root is left out.

![ag_map_legend_row](../../../images/layouts/advanced-groups/hud/ag_map_legend_row.png)

## Loaded by

- `AdvancedGroups/scripts/5_Mission/AdvancedGroups/GUI/Pages/AGPageMarkers.c` line 232

## Widget tree

Positions and sizes are in pixels when the widget uses exact sizing, otherwise they are fractions of the parent (0–1).

| Widget | Type | Position | Size | Text / notes |
|---|---|---|---|---|
| `ag_map_legend_row` | FrameWidget | 0 0 | 232 × 22 |  |
| &nbsp;&nbsp;└ `img_icon` | ImageWidget | 0 2 | 18 × 18 |  |
| &nbsp;&nbsp;└ `txt_label` | TextWidget | 28 0 | 204 × 22 |  |

{% endraw %}
