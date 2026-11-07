---
layout: page
title: "ag_marker_list_entry.layout — Marker list row"
section: DOCUMENTATION
permalink: /docs/layouts/advanced-groups/hud/ag_marker_list_entry.html
---
{% raw %}
# ag_marker_list_entry.layout — Marker list row

**Mod:** Advanced Groups  
**File:** `AdvancedGroups/gui/layouts/hud/ag_marker_list_entry.layout`  
**Root:** `PanelWidget` `rootFrame`, size 484 × 40  
**Widgets:** 8

One marker in the marker list with icon, name and distance; click to centre the map on it.

## Preview

Wireframe drawn straight from the layout file: positions, sizes, colours and default text are exact. Image widgets appear as dashed placeholders, and anything hidden at start inside the root is left out.

![ag_marker_list_entry](../../../images/layouts/advanced-groups/hud/ag_marker_list_entry.png)

## Loaded by

- `AdvancedGroups/scripts/5_Mission/AdvancedGroups/GUI/Pages/AGPageMarkers.c` line 1510

## Widget tree

Positions and sizes are in pixels when the widget uses exact sizing, otherwise they are fractions of the parent (0–1).

| Widget | Type | Position | Size | Text / notes |
|---|---|---|---|---|
| `rootFrame` | PanelWidget | 0 0 | 484 × 40 |  |
| &nbsp;&nbsp;└ `CardAccent` | PanelWidget | 0 0 | 3 × 40 |  |
| &nbsp;&nbsp;└ `icon` | ImageWidget | 4 6 | 28 × 28 |  |
| &nbsp;&nbsp;└ `title` | TextWidget | 34 0 | 280 × 40 | "Marker Name" |
| &nbsp;&nbsp;└ `btnToggle3D` | ButtonWidget | 318 6 | 52 × 28 | "3D" |
| &nbsp;&nbsp;└ `btnToggle2D` | ButtonWidget | 374 6 | 52 × 28 | "2D" |
| &nbsp;&nbsp;└ `btnDelete` | ButtonWidget | 430 6 | 34 × 28 |  |
| &nbsp;&nbsp;&nbsp;&nbsp;└ `IconDelete` | ImageWidget | 7 4 | 20 × 20 |  |

{% endraw %}
