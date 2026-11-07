---
layout: page
title: "compass.layout — Compass bar"
section: DOCUMENTATION
permalink: /docs/layouts/advanced-groups/hud/compass.html
---
{% raw %}
# compass.layout — Compass bar

**Mod:** Advanced Groups  
**File:** `AdvancedGroups/gui/layouts/hud/compass.layout`  
**Root:** `PanelWidget` `Root`, size 980 × 43  
**Widgets:** 8

Compass strip at the top of the screen with bearings and marker pips.

## Preview

Wireframe drawn straight from the layout file: positions, sizes, colours and default text are exact. Image widgets appear as dashed placeholders, and anything hidden at start inside the root is left out.

![compass](../../../images/layouts/advanced-groups/hud/compass.png)

## Loaded by

- `AdvancedGroups/scripts/4_World/AdvancedGroups/HUD/AGCompass.c` line 10

## Widget tree

Positions and sizes are in pixels when the widget uses exact sizing, otherwise they are fractions of the parent (0–1).

| Widget | Type | Position | Size | Text / notes |
|---|---|---|---|---|
| `Root` | PanelWidget | 0 22 | 980 × 43 |  |
| &nbsp;&nbsp;└ `CompassL3` | TextWidget | 30 6 | 100 × 30 |  |
| &nbsp;&nbsp;└ `CompassL2` | TextWidget | 150 5 | 110 × 32 |  |
| &nbsp;&nbsp;└ `CompassL1` | TextWidget | 285 4 | 120 × 34 |  |
| &nbsp;&nbsp;└ `CompassDir` | TextWidget | 425 0 | 130 × 43 | "N 0" |
| &nbsp;&nbsp;└ `CompassR1` | TextWidget | 575 4 | 120 × 34 |  |
| &nbsp;&nbsp;└ `CompassR2` | TextWidget | 720 5 | 110 × 32 |  |
| &nbsp;&nbsp;└ `CompassR3` | TextWidget | 850 6 | 100 × 30 |  |

{% endraw %}
