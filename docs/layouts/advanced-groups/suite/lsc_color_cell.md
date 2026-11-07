---
layout: page
title: "lsc_color_cell.layout — Colour swatch"
section: DOCUMENTATION
permalink: /docs/layouts/advanced-groups/suite/lsc_color_cell.html
---
{% raw %}
# lsc_color_cell.layout — Colour swatch

**Mod:** Advanced Groups  
**File:** `AdvancedGroups/gui/layouts/suite/lsc_color_cell.layout`  
**Root:** `PanelWidget` `color_cell`, size 46 × 46  
**Widgets:** 4

One clickable swatch in the colour picker.

> Advanced Banking ships an identical copy in `Advanced_Banking/gui/suite/`, used only when Advanced Groups is not loaded.

## Preview

Wireframe drawn straight from the layout file: positions, sizes, colours and default text are exact. Image widgets appear as dashed placeholders, and anything hidden at start inside the root is left out.

![lsc_color_cell](../../../images/layouts/advanced-groups/suite/lsc_color_cell.png)

## Loaded by

- `AdvancedGroups/scripts/5_Mission/AdvancedGroups/SuiteConsole/LSCConsoleMenu.c` line 2448
- `Advanced_Banking/scripts/5_Mission/AdvancedBanking/SuiteConsole/LSCConsoleMenu.c` line 2455

## Widget tree

Positions and sizes are in pixels when the widget uses exact sizing, otherwise they are fractions of the parent (0–1).

| Widget | Type | Position | Size | Text / notes |
|---|---|---|---|---|
| `color_cell` | PanelWidget | 0 0 | 46 × 46 |  |
| &nbsp;&nbsp;└ `panel_ring` | PanelWidget | 0 0 | 46 × 46 | hidden at start |
| &nbsp;&nbsp;└ `panel_fill` | PanelWidget | 3 3 | 40 × 40 |  |
| &nbsp;&nbsp;└ `btn_cell` | ButtonWidget | 0 0 | 46 × 46 |  |

{% endraw %}
