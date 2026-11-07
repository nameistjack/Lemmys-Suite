---
layout: page
title: "lsc_section_row.layout — Section rail row"
section: DOCUMENTATION
permalink: /docs/layouts/advanced-groups/suite/lsc_section_row.html
---
{% raw %}
# lsc_section_row.layout — Section rail row

**Mod:** Advanced Groups  
**File:** `AdvancedGroups/gui/layouts/suite/lsc_section_row.layout`  
**Root:** `PanelWidget` `row_section`, size 268 × 34  
**Widgets:** 6

One section in the left rail with its pending-changes badge.

> Advanced Banking ships an identical copy in `Advanced_Banking/gui/suite/`, used only when Advanced Groups is not loaded.

## Preview

Wireframe drawn straight from the layout file: positions, sizes, colours and default text are exact. Image widgets appear as dashed placeholders, and anything hidden at start inside the root is left out.

![lsc_section_row](../../../images/layouts/advanced-groups/suite/lsc_section_row.png)

## Loaded by

- `AdvancedGroups/scripts/5_Mission/AdvancedGroups/SuiteConsole/LSCConsoleMenu.c` line 653
- `Advanced_Banking/scripts/5_Mission/AdvancedBanking/SuiteConsole/LSCConsoleMenu.c` line 660

## Widget tree

Positions and sizes are in pixels when the widget uses exact sizing, otherwise they are fractions of the parent (0–1).

| Widget | Type | Position | Size | Text / notes |
|---|---|---|---|---|
| `row_section` | PanelWidget | 0 0 | 268 × 34 |  |
| &nbsp;&nbsp;└ `btn_hit` | ButtonWidget | 0 0 | 268 × 34 |  |
| &nbsp;&nbsp;└ `panel_strip` | PanelWidget | 0 0 | 4 × 34 |  |
| &nbsp;&nbsp;└ `txt_title` | TextWidget | 18 0 | 200 × 34 | "Section" |
| &nbsp;&nbsp;└ `badge_pending` | PanelWidget | 228 9 | 28 × 16 | hidden at start |
| &nbsp;&nbsp;&nbsp;&nbsp;└ `txt_count` | TextWidget | 0 0 | 28 × 16 | "2" |

{% endraw %}
