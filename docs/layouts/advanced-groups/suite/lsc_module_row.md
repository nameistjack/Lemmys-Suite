---
layout: page
title: "lsc_module_row.layout — Module card / rail row"
section: DOCUMENTATION
permalink: /docs/layouts/advanced-groups/suite/lsc_module_row.html
---
{% raw %}
# lsc_module_row.layout — Module card / rail row

**Mod:** Advanced Groups  
**File:** `AdvancedGroups/gui/layouts/suite/lsc_module_row.layout`  
**Root:** `PanelWidget` `row_module`, size 268 × 54  
**Widgets:** 7

A module card on the overview, the ALL MODULES back row and the tool rows (Group manager, Zone and marker map).

> Advanced Banking ships an identical copy in `Advanced_Banking/gui/suite/`, used only when Advanced Groups is not loaded.

## Preview

Wireframe drawn straight from the layout file: positions, sizes, colours and default text are exact. Image widgets appear as dashed placeholders, and anything hidden at start inside the root is left out.

![lsc_module_row](../../../images/layouts/advanced-groups/suite/lsc_module_row.png)

## Loaded by

- `AdvancedGroups/scripts/5_Mission/AdvancedGroups/SuiteConsole/LSCConsoleMenu.c` line 634
- `AdvancedGroups/scripts/5_Mission/AdvancedGroups/SuiteConsole/LSCConsoleMenu.c` line 679
- `AdvancedGroups/scripts/5_Mission/AdvancedGroups/SuiteConsole/LSCConsoleMenu.c` line 839
- `AdvancedGroups/scripts/5_Mission/AdvancedGroups/SuiteConsole/LSCConsoleMenu.c` line 840
- `Advanced_Banking/scripts/5_Mission/AdvancedBanking/SuiteConsole/LSCConsoleMenu.c` line 641
- `Advanced_Banking/scripts/5_Mission/AdvancedBanking/SuiteConsole/LSCConsoleMenu.c` line 686
- `Advanced_Banking/scripts/5_Mission/AdvancedBanking/SuiteConsole/LSCConsoleMenu.c` line 846
- `Advanced_Banking/scripts/5_Mission/AdvancedBanking/SuiteConsole/LSCConsoleMenu.c` line 847

## Widget tree

Positions and sizes are in pixels when the widget uses exact sizing, otherwise they are fractions of the parent (0–1).

| Widget | Type | Position | Size | Text / notes |
|---|---|---|---|---|
| `row_module` | PanelWidget | 0 0 | 268 × 54 |  |
| &nbsp;&nbsp;└ `btn_hit` | ButtonWidget | 0 0 | 268 × 54 |  |
| &nbsp;&nbsp;└ `panel_strip` | PanelWidget | 0 0 | 4 × 54 |  |
| &nbsp;&nbsp;└ `txt_title` | TextWidget | 18 8 | 200 × 20 | "Module" |
| &nbsp;&nbsp;└ `txt_sub` | TextWidget | 18 30 | 236 × 16 |  |
| &nbsp;&nbsp;└ `badge_pending` | PanelWidget | 228 19 | 28 × 16 | hidden at start |
| &nbsp;&nbsp;&nbsp;&nbsp;└ `txt_count` | TextWidget | 0 0 | 28 × 16 | "3" |

{% endraw %}
