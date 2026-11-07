---
layout: page
title: "ag_page_markers.layout — Markers page"
section: DOCUMENTATION
permalink: /docs/layouts/advanced-groups/hud/ag_page_markers.html
---
{% raw %}
# ag_page_markers.layout — Markers page

**Mod:** Advanced Groups  
**File:** `AdvancedGroups/gui/layouts/hud/ag_page_markers.layout`  
**Root:** `PanelWidget` `rootFrame`, size 520 × 1  
**Widgets:** 11

Map page for group and private markers. Hosts the shared map, the marker list, filters and the marker popup.

## Preview

Wireframe drawn straight from the layout file: positions, sizes, colours and default text are exact. Image widgets appear as dashed placeholders, and anything hidden at start inside the root is left out.

![ag_page_markers](../../../images/layouts/advanced-groups/hud/ag_page_markers.png)

## Loaded by

- `AdvancedGroups/scripts/5_Mission/AdvancedGroups/GUI/Pages/AGPageMarkers.c` line 181

## Widget tree

Positions and sizes are in pixels when the widget uses exact sizing, otherwise they are fractions of the parent (0–1).

| Widget | Type | Position | Size | Text / notes |
|---|---|---|---|---|
| `rootFrame` | PanelWidget | 0 0 | 520 × 1 |  |
| &nbsp;&nbsp;└ `title` | TextWidget | 0 18 | 520 × 34 | "Marker List:" |
| &nbsp;&nbsp;└ `MarkerCategoryControls` | PanelWidget | 18 56 | 484 × 32 |  |
| &nbsp;&nbsp;&nbsp;&nbsp;└ `BtnMarkersAll` | ButtonWidget | 0 0 | 238 × 28 | "SHOW ALL" |
| &nbsp;&nbsp;&nbsp;&nbsp;└ `BtnMarkersOff` | ButtonWidget | 246 0 | 238 × 28 | "HIDE ALL" |
| &nbsp;&nbsp;&nbsp;&nbsp;└ `BtnMarkersServer` | ButtonWidget | 0 0 | 154 × 28 | "SERVER: ON", hidden at start |
| &nbsp;&nbsp;&nbsp;&nbsp;└ `BtnMarkersGroup` | ButtonWidget | 160 0 | 100 × 28 | "GRP", hidden at start |
| &nbsp;&nbsp;&nbsp;&nbsp;└ `BtnMarkersPrivate` | ButtonWidget | 266 0 | 100 × 28 | "PRI", hidden at start |
| &nbsp;&nbsp;&nbsp;&nbsp;└ `BtnMarkersPlayers` | ButtonWidget | 372 0 | 106 × 28 | "PLY", hidden at start |
| &nbsp;&nbsp;└ `marker_scroll` | ScrollWidget | 18 96 | 484 × 944 |  |
| &nbsp;&nbsp;&nbsp;&nbsp;└ `marker_list` | PanelWidget | 0 0 | 484 × 1 |  |

{% endraw %}
