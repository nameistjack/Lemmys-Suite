---
layout: page
title: "marker_label.layout — 3D marker label"
section: DOCUMENTATION
permalink: /docs/layouts/advanced-groups/hud/marker_label.html
---
{% raw %}
# marker_label.layout — 3D marker label

**Mod:** Advanced Groups  
**File:** `AdvancedGroups/gui/layouts/hud/marker_label.layout`  
**Root:** `PanelWidget` `MarkerLabel`, size 320 × 43  
**Widgets:** 4

Label drawn in the world for a 3D marker: icon, name and distance.

## Preview

Wireframe drawn straight from the layout file: positions, sizes, colours and default text are exact. Image widgets appear as dashed placeholders, and anything hidden at start inside the root is left out.

![marker_label](../../../images/layouts/advanced-groups/hud/marker_label.png)

## Loaded by

- `AdvancedGroups/scripts/4_World/AdvancedGroups/HUD/AG3DMarkers.c` line 36

## Widget tree

Positions and sizes are in pixels when the widget uses exact sizing, otherwise they are fractions of the parent (0–1).

| Widget | Type | Position | Size | Text / notes |
|---|---|---|---|---|
| `MarkerLabel` | PanelWidget |  | 320 × 43 |  |
| &nbsp;&nbsp;└ `LabelBG` | PanelWidget |  | 320 × 43 |  |
| &nbsp;&nbsp;└ `LabelIcon` | ImageWidget | 7 5 | 32 × 32 |  |
| &nbsp;&nbsp;└ `LabelText` | TextWidget | 45 4 | 268 × 35 |  |

{% endraw %}
