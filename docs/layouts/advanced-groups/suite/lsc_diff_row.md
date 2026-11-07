---
layout: page
title: "lsc_diff_row.layout — Review change row"
section: DOCUMENTATION
permalink: /docs/layouts/advanced-groups/suite/lsc_diff_row.html
---
{% raw %}
# lsc_diff_row.layout — Review change row

**Mod:** Advanced Groups  
**File:** `AdvancedGroups/gui/layouts/suite/lsc_diff_row.layout`  
**Root:** `PanelWidget` `row_diff`, size 832 × 62  
**Widgets:** 13

One pending change in the Review dialog: before -> after and REVERT.

> Advanced Banking ships an identical copy in `Advanced_Banking/gui/suite/`, used only when Advanced Groups is not loaded.

## Preview

Wireframe drawn straight from the layout file: positions, sizes, colours and default text are exact. Image widgets appear as dashed placeholders, and anything hidden at start inside the root is left out.

![lsc_diff_row](../../../images/layouts/advanced-groups/suite/lsc_diff_row.png)

## Loaded by

- `AdvancedGroups/scripts/5_Mission/AdvancedGroups/SuiteConsole/LSCConsoleMenu.c` line 2587
- `AdvancedGroups/scripts/5_Mission/AdvancedGroups/SuiteConsole/LSCConsoleMenu.c` line 2588
- `Advanced_Banking/scripts/5_Mission/AdvancedBanking/SuiteConsole/LSCConsoleMenu.c` line 2594
- `Advanced_Banking/scripts/5_Mission/AdvancedBanking/SuiteConsole/LSCConsoleMenu.c` line 2595

## Widget tree

Positions and sizes are in pixels when the widget uses exact sizing, otherwise they are fractions of the parent (0–1).

| Widget | Type | Position | Size | Text / notes |
|---|---|---|---|---|
| `row_diff` | PanelWidget | 0 0 | 832 × 62 |  |
| &nbsp;&nbsp;└ `panel_strip` | PanelWidget | 0 0 | 4 × 62 |  |
| &nbsp;&nbsp;└ `txt_title` | TextWidget | 16 10 | 660 × 20 |  |
| &nbsp;&nbsp;└ `txt_before` | TextWidget | 16 34 | 200 × 18 |  |
| &nbsp;&nbsp;└ `txt_arrow` | TextWidget | 216 34 | 30 × 18 | ">>" |
| &nbsp;&nbsp;└ `txt_after` | TextWidget | 246 34 | 430 × 18 |  |
| &nbsp;&nbsp;└ `btn_revert` | ButtonWidget | 708 15 | 112 × 32 |  |
| &nbsp;&nbsp;&nbsp;&nbsp;└ `panel_bg` | PanelWidget | 0 0 | 112 × 32 |  |
| &nbsp;&nbsp;&nbsp;&nbsp;└ `line_t` | PanelWidget | 0 0 | 112 × 1 |  |
| &nbsp;&nbsp;&nbsp;&nbsp;└ `line_b` | PanelWidget | 0 31 | 112 × 1 |  |
| &nbsp;&nbsp;&nbsp;&nbsp;└ `line_l` | PanelWidget | 0 0 | 1 × 32 |  |
| &nbsp;&nbsp;&nbsp;&nbsp;└ `line_r` | PanelWidget | 111 0 | 1 × 32 |  |
| &nbsp;&nbsp;&nbsp;&nbsp;└ `txt_label` | TextWidget | 0 0 | 112 × 32 | "REVERT" |

{% endraw %}
