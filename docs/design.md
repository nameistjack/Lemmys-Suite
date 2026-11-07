---
layout: page
title: "Design file"
section: DOCUMENTATION
permalink: /docs/design.html
---
{% raw %}
# Design file

Every screen in the suite is described twice:

1. **Layout pages (this repository).** Each `.layout` file has its own page under [layouts/](layouts/index.html). The page has a rendered wireframe, the scripts that load it, and a full widget tree with positions, sizes, styles and default text. Those wireframes come straight from the layout files, so they are always as current as the files themselves.
2. **Figma file.** It is the editable design board for mock-ups and future changes: [Lemmy's Suite — UI Layouts](https://www.figma.com/design/RToPRRSRGZrCsp9lOhPHJd).

## What is in the Figma file

Each layout is a card. The card title is the file name. Under it sits a dark stage, drawn at the layout's real pixel size, with every widget as a named layer. Layer names match the widget names in the `.layout` file, so a layer such as `btn_apply` is the `btn_apply` widget in the code.

| Page | Contents |
|---|---|
| **Control Room** | All 14 `suite/lsc_*` layouts: the console window, the module, section, header, note, field, lines, collection, item, history and diff rows, the colour picker modal and cell, and the map picker modal. Modals that start hidden are drawn open so you can see them. |
| **Advanced Groups** | HUD and helper layouts: compass, minimap and blips, player list and member row, info panel, marker label, map marker, map legend, chat root, item and input, and the notification toast. The main menu pages (`ag_main_menu`, `ag_page_*`, the zone editor, the spawn menu and the invite menu) are still to be added. Until then, use their wireframes in the layout pages. |
| **Advanced Banking & Theme** | The Arctic Glass palette cover, plus `BankingMenuTabbed.layout` drawn three times: once for each tab (Banking, Transfers, Administration). |

The legacy config editor pages (`admin/config_pages/ag_config_page_*`) are fallbacks that are kept for reference. They are documented in the layout pages only.

## Palette (Arctic Glass)

| Token | Colour | Used for |
|---|---|---|
| Ice | `#38E8FF` | Accent edges, overlines, primary buttons |
| Surface | `#08171C` at 94 % | Window panels |
| Card | `#0D2430` at 86 % | Rails and content panels |
| Row | `#123342` at 90 % | Setting rows |
| Input | `#051217` | Edit boxes and list boxes |
| Text | `#DEE6E8` | Primary text |
| Muted | `#A3B0B8` | Help text |
| Faint | `#5E7078` | Meta text and hints |
| Good | `#54F2A1` | Live state, Apply |
| Warn | `#FFD166` | Restart tags, banners |
| Pending | `#FF8A1F` | Pending-change badges |
| Danger | `#FF4C61` | Discard, Delete |

## Keeping them in sync

The `.layout` files are the source of truth. When a layout changes, its page under `layouts/` is regenerated from the file. If you edit a screen in Figma first, carry the change into the `.layout` file by hand. Keep the layer names identical so that scripts and docs still line up.

{% endraw %}
