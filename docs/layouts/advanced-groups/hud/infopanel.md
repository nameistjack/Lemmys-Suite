---
layout: page
title: "infopanel.layout — Info panel"
section: DOCUMENTATION
permalink: /docs/layouts/advanced-groups/hud/infopanel.html
---
{% raw %}
# infopanel.layout — Info panel

**Mod:** Advanced Groups  
**File:** `AdvancedGroups/gui/layouts/hud/infopanel.layout`  
**Root:** `PanelWidget` `Root`, size 346 × 42  
**Widgets:** 3

Small on-screen info box (zone name, territory owner, notices).

## Preview

Wireframe drawn straight from the layout file: positions, sizes, colours and default text are exact. Image widgets appear as dashed placeholders, and anything hidden at start inside the root is left out.

![infopanel](../../../images/layouts/advanced-groups/hud/infopanel.png)

## Loaded by

- `AdvancedGroups/scripts/4_World/AdvancedGroups/HUD/AGInfoPanel.c` line 9

## Widget tree

Positions and sizes are in pixels when the widget uses exact sizing, otherwise they are fractions of the parent (0–1).

| Widget | Type | Position | Size | Text / notes |
|---|---|---|---|---|
| `Root` | PanelWidget | 38 22 | 346 × 42 |  |
| &nbsp;&nbsp;└ `BG` | PanelWidget |  | 346 × 42 |  |
| &nbsp;&nbsp;└ `GroupName` | TextWidget | 10 4 | 325 × 34 |  |

{% endraw %}
