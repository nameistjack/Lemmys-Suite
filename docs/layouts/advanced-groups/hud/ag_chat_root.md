---
layout: page
title: "ag_chat_root.layout — Chat history box"
section: DOCUMENTATION
permalink: /docs/layouts/advanced-groups/hud/ag_chat_root.html
---
{% raw %}
# ag_chat_root.layout — Chat history box

**Mod:** Advanced Groups  
**File:** `AdvancedGroups/gui/layouts/hud/ag_chat_root.layout`  
**Root:** `FrameWidget` `rootFrame`, size 900 × 240  
**Widgets:** 4

Replaces the vanilla chat: a clipped scroll box holding the message rows and the 'new messages below' hint.

## Preview

Wireframe drawn straight from the layout file: positions, sizes, colours and default text are exact. Image widgets appear as dashed placeholders, and anything hidden at start inside the root is left out.

![ag_chat_root](../../../images/layouts/advanced-groups/hud/ag_chat_root.png)

## Loaded by

- `AdvancedGroups/scripts/5_Mission/AdvancedGroups/GUI/Chat/AGChat.c` line 69

## Widget tree

Positions and sizes are in pixels when the widget uses exact sizing, otherwise they are fractions of the parent (0–1).

| Widget | Type | Position | Size | Text / notes |
|---|---|---|---|---|
| `rootFrame` | FrameWidget | 20 200 | 900 × 240 |  |
| &nbsp;&nbsp;└ `ChatScrollWidget` | ScrollWidget | 0 0 | 900 × 240 |  |
| &nbsp;&nbsp;&nbsp;&nbsp;└ `ChatWrapSpacer` | PanelWidget | 20 0 | 860 × 1 |  |
| &nbsp;&nbsp;└ `ChatNewHint` | TextWidget | 24 0 | 300 × 20 | "v  New messages below  (PgDn)", hidden at start |

{% endraw %}
