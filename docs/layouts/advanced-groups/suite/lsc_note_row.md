---
layout: page
title: "lsc_note_row.layout — Note row"
section: DOCUMENTATION
permalink: /docs/layouts/advanced-groups/suite/lsc_note_row.html
---
{% raw %}
# lsc_note_row.layout — Note row

**Mod:** Advanced Groups  
**File:** `AdvancedGroups/gui/layouts/suite/lsc_note_row.layout`  
**Root:** `PanelWidget` `row_note`, size 1280 × 56  
**Widgets:** 2

Informational line such as 'Loading module configuration'.

> Advanced Banking ships an identical copy in `Advanced_Banking/gui/suite/`, used only when Advanced Groups is not loaded.

## Preview

Wireframe drawn straight from the layout file: positions, sizes, colours and default text are exact. Image widgets appear as dashed placeholders, and anything hidden at start inside the root is left out.

![lsc_note_row](../../../images/layouts/advanced-groups/suite/lsc_note_row.png)

## Loaded by

- `AdvancedGroups/scripts/5_Mission/AdvancedGroups/SuiteConsole/LSCConsoleMenu.c` line 944
- `AdvancedGroups/scripts/5_Mission/AdvancedGroups/SuiteConsole/LSCConsoleMenu.c` line 945
- `Advanced_Banking/scripts/5_Mission/AdvancedBanking/SuiteConsole/LSCConsoleMenu.c` line 951
- `Advanced_Banking/scripts/5_Mission/AdvancedBanking/SuiteConsole/LSCConsoleMenu.c` line 952

## Widget tree

Positions and sizes are in pixels when the widget uses exact sizing, otherwise they are fractions of the parent (0–1).

| Widget | Type | Position | Size | Text / notes |
|---|---|---|---|---|
| `row_note` | PanelWidget | 0 0 | 1280 × 56 |  |
| &nbsp;&nbsp;└ `txt_note` | TextWidget | 20 0 | 1240 × 56 |  |

{% endraw %}
