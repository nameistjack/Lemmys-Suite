---
layout: page
title: "lsc_header_row.layout — Section header"
section: DOCUMENTATION
permalink: /docs/layouts/advanced-groups/suite/lsc_header_row.html
---
{% raw %}
# lsc_header_row.layout — Section header

**Mod:** Advanced Groups  
**File:** `AdvancedGroups/gui/layouts/suite/lsc_header_row.layout`  
**Root:** `FrameWidget` `row_header`, size 1280 × 90  
**Widgets:** 4

Breadcrumb, title and summary at the top of a section.

> Advanced Banking ships an identical copy in `Advanced_Banking/gui/suite/`, used only when Advanced Groups is not loaded.

## Preview

Wireframe drawn straight from the layout file: positions, sizes, colours and default text are exact. Image widgets appear as dashed placeholders, and anything hidden at start inside the root is left out.

![lsc_header_row](../../../images/layouts/advanced-groups/suite/lsc_header_row.png)

## Loaded by

- `AdvancedGroups/scripts/5_Mission/AdvancedGroups/SuiteConsole/LSCConsoleMenu.c` line 928
- `AdvancedGroups/scripts/5_Mission/AdvancedGroups/SuiteConsole/LSCConsoleMenu.c` line 929
- `Advanced_Banking/scripts/5_Mission/AdvancedBanking/SuiteConsole/LSCConsoleMenu.c` line 935
- `Advanced_Banking/scripts/5_Mission/AdvancedBanking/SuiteConsole/LSCConsoleMenu.c` line 936

## Widget tree

Positions and sizes are in pixels when the widget uses exact sizing, otherwise they are fractions of the parent (0–1).

| Widget | Type | Position | Size | Text / notes |
|---|---|---|---|---|
| `row_header` | FrameWidget | 0 0 | 1280 × 90 |  |
| &nbsp;&nbsp;└ `txt_crumb` | TextWidget | 0 8 | 1280 × 14 | "MODULE  /  SECTION" |
| &nbsp;&nbsp;└ `txt_title` | TextWidget | 0 26 | 1280 × 32 | "Section" |
| &nbsp;&nbsp;└ `txt_summary` | TextWidget | 0 60 | 1280 × 20 |  |

{% endraw %}
