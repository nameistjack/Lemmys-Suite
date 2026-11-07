---
layout: page
title: "ag_zone_card_header.layout — Zone card header"
section: DOCUMENTATION
permalink: /docs/layouts/advanced-groups/hud/ag_zone_card_header.html
---
{% raw %}
# ag_zone_card_header.layout — Zone card header

**Mod:** Advanced Groups  
**File:** `AdvancedGroups/gui/layouts/hud/ag_zone_card_header.layout`  
**Root:** `PanelWidget` `rootFrame`, size 360 × 40  
**Widgets:** 4

Header of a zone group (Safe zones, No-build, Territories...) in the zone panel.

## Preview

Wireframe drawn straight from the layout file: positions, sizes, colours and default text are exact. Image widgets appear as dashed placeholders, and anything hidden at start inside the root is left out.

![ag_zone_card_header](../../../images/layouts/advanced-groups/hud/ag_zone_card_header.png)

## Loaded by

- `AdvancedGroups/scripts/5_Mission/AdvancedGroups/GUI/Pages/AGPageAdmin.c` line 768

## Widget tree

Positions and sizes are in pixels when the widget uses exact sizing, otherwise they are fractions of the parent (0–1).

| Widget | Type | Position | Size | Text / notes |
|---|---|---|---|---|
| `rootFrame` | PanelWidget | 0 0 | 360 × 40 |  |
| &nbsp;&nbsp;└ `CardAccent` | PanelWidget | 0 0 | 4 × 40 |  |
| &nbsp;&nbsp;└ `btnCollapse` | ButtonWidget | 10 6 | 32 × 28 | "-" |
| &nbsp;&nbsp;└ `title` | TextWidget | 52 0 | 294 × 40 | "Category" |

{% endraw %}
