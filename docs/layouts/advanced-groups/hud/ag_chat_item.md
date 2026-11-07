---
layout: page
title: "ag_chat_item.layout — Chat message row"
section: DOCUMENTATION
permalink: /docs/layouts/advanced-groups/hud/ag_chat_item.html
---
{% raw %}
# ag_chat_item.layout — Chat message row

**Mod:** Advanced Groups  
**File:** `AdvancedGroups/gui/layouts/hud/ag_chat_item.layout`  
**Root:** `PanelWidget` `rootFrame`, size 860 × 24  
**Widgets:** 7

One chat line: channel tag, role tag, group tag, sender name and message text, wrapped across rows when long.

## Preview

Wireframe drawn straight from the layout file: positions, sizes, colours and default text are exact. Image widgets appear as dashed placeholders, and anything hidden at start inside the root is left out.

![ag_chat_item](../../../images/layouts/advanced-groups/hud/ag_chat_item.png)

## Loaded by

- `AdvancedGroups/scripts/5_Mission/AdvancedGroups/GUI/Chat/AGChatLine.c` line 17

## Widget tree

Positions and sizes are in pixels when the widget uses exact sizing, otherwise they are fractions of the parent (0–1).

| Widget | Type | Position | Size | Text / notes |
|---|---|---|---|---|
| `rootFrame` | PanelWidget | 0 0 | 860 × 24 |  |
| &nbsp;&nbsp;└ `ChatWrapSpacer` | WrapSpacerWidget | 0 0 | 860 × 24 |  |
| &nbsp;&nbsp;&nbsp;&nbsp;└ `ChannelTag` | TextWidget | 0 0 | 1 × 1 |  |
| &nbsp;&nbsp;&nbsp;&nbsp;└ `RoleTag` | TextWidget | 0 0 | 1 × 1 |  |
| &nbsp;&nbsp;&nbsp;&nbsp;└ `GroupTag` | TextWidget | 0 0 | 1 × 1 |  |
| &nbsp;&nbsp;&nbsp;&nbsp;└ `SenderName` | TextWidget | 0 0 | 1 × 1 |  |
| &nbsp;&nbsp;&nbsp;&nbsp;└ `MessageText` | TextWidget | 0 0 | 400 × 24 |  |

{% endraw %}
