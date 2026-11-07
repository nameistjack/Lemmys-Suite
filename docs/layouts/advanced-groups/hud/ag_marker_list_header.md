---
layout: page
title: "ag_marker_list_header.layout — Marker list section header"
section: DOCUMENTATION
permalink: /docs/layouts/advanced-groups/hud/ag_marker_list_header.html
---
{% raw %}
# ag_marker_list_header.layout — Marker list section header

**Mod:** Advanced Groups  
**File:** `AdvancedGroups/gui/layouts/hud/ag_marker_list_header.layout`  
**Root:** `PanelWidget` `rootFrame`, size 484 × 40  
**Widgets:** 6

Header row in the marker list (Group, Private, Server, Events).

## Preview

Wireframe drawn straight from the layout file: positions, sizes, colours and default text are exact. Image widgets appear as dashed placeholders, and anything hidden at start inside the root is left out.

![ag_marker_list_header](../../../images/layouts/advanced-groups/hud/ag_marker_list_header.png)

## Loaded by

- `AdvancedGroups/scripts/5_Mission/AdvancedGroups/GUI/Pages/AGPageMarkers.c` line 1457

## Widget tree

Positions and sizes are in pixels when the widget uses exact sizing, otherwise they are fractions of the parent (0–1).

| Widget | Type | Position | Size | Text / notes |
|---|---|---|---|---|
| `rootFrame` | PanelWidget | 0 0 | 484 × 40 |  |
| &nbsp;&nbsp;└ `CardAccent` | PanelWidget | 0 0 | 4 × 40 |  |
| &nbsp;&nbsp;└ `title` | TextWidget | 50 0 | 294 × 40 | "Category" |
| &nbsp;&nbsp;└ `btnCollapse` | ButtonWidget | 10 6 | 32 × 28 | "-" |
| &nbsp;&nbsp;└ `btnToggle3D` | ButtonWidget | 350 6 | 58 × 28 | "3D", hidden at start |
| &nbsp;&nbsp;└ `btnToggleVis` | ButtonWidget | 414 6 | 58 × 28 | "2D", hidden at start |

{% endraw %}
