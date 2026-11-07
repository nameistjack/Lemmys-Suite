---
layout: page
title: "map_marker.layout — Map marker widget"
section: DOCUMENTATION
permalink: /docs/layouts/advanced-groups/helper/map_marker.html
---
{% raw %}
# map_marker.layout — Map marker widget

**Mod:** Advanced Groups  
**File:** `AdvancedGroups/gui/layouts/helper/map_marker.layout`  
**Root:** `FrameWidget` `Root`, size 320 × 64  
**Widgets:** 4

Marker icon drawn on map widgets (main map, spawn map).

## Preview

Wireframe drawn straight from the layout file: positions, sizes, colours and default text are exact. Image widgets appear as dashed placeholders, and anything hidden at start inside the root is left out.

![map_marker](../../../images/layouts/advanced-groups/helper/map_marker.png)

## Loaded by

- `AdvancedGroups/scripts/5_Mission/AdvancedGroups/GUI/AGMapMarkerWidget.c` line 33

## Widget tree

Positions and sizes are in pixels when the widget uses exact sizing, otherwise they are fractions of the parent (0–1).

| Widget | Type | Position | Size | Text / notes |
|---|---|---|---|---|
| `Root` | FrameWidget |  | 320 × 64 |  |
| &nbsp;&nbsp;└ `MarkerIcon` | ImageWidget | 0 -12 | 32 × 32 |  |
| &nbsp;&nbsp;└ `PlayerTriangleCanvas` | CanvasWidget | 0 0 | 320 × 64 | hidden at start |
| &nbsp;&nbsp;└ `MarkerLabel` | TextWidget | 20 15 | 280 × 20 | "Marker Name" |

{% endraw %}
