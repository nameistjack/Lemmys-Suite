---
layout: page
title: "Layout reference"
section: DOCUMENTATION
permalink: /docs/layouts/index.html
---
{% raw %}
# Layout reference

Every `.layout` file shipped by the suite, what it is for, and which script loads it. Each page lists the full widget tree with names, types, positions, sizes and default text — the names are what scripts look up with `FindAnyWidget`.

Visual mock-ups of these screens are kept in the Figma design file (see [Design file](../design.html)).

## Advanced Groups

| Layout | Purpose | Widgets | In use |
|---|---|---|---|
| [admin/ag_suite_config_editor.layout](advanced-groups/admin/ag_suite_config_editor.html) | Legacy AG config editor shell (fallback) | 32 | yes |
| [admin/config_pages/ag_config_page_0.layout](advanced-groups/admin/config_pages/ag_config_page_0.html) | Legacy config page 0 | 70 | yes |
| [admin/config_pages/ag_config_page_1.layout](advanced-groups/admin/config_pages/ag_config_page_1.html) | Legacy config page 1 | 67 | yes |
| [admin/config_pages/ag_config_page_2.layout](advanced-groups/admin/config_pages/ag_config_page_2.html) | Legacy config page 2 | 25 | yes |
| [admin/config_pages/ag_config_page_3.layout](advanced-groups/admin/config_pages/ag_config_page_3.html) | Legacy config page 3 | 40 | yes |
| [admin/config_pages/ag_config_page_4.layout](advanced-groups/admin/config_pages/ag_config_page_4.html) | Legacy config page 4 | 181 | yes |
| [admin/config_pages/ag_config_page_5.layout](advanced-groups/admin/config_pages/ag_config_page_5.html) | Legacy config page 5 | 49 | yes |
| [admin/config_pages/ag_config_page_6.layout](advanced-groups/admin/config_pages/ag_config_page_6.html) | Legacy config page 6 | 52 | yes |
| [admin/config_pages/ag_config_page_7.layout](advanced-groups/admin/config_pages/ag_config_page_7.html) | Legacy config page 7 | 34 | yes |
| [admin/config_pages/ag_config_page_8.layout](advanced-groups/admin/config_pages/ag_config_page_8.html) | Legacy config page 8 | 61 | yes |
| [admin/config_pages/ag_config_page_9.layout](advanced-groups/admin/config_pages/ag_config_page_9.html) | Legacy config page 9 | 61 | yes |
| [admin/lemmy_suite_admin.layout](advanced-groups/admin/lemmy_suite_admin.html) | Legacy suite admin hub (fallback) | 35 | yes |
| [helper/map_marker.layout](advanced-groups/helper/map_marker.html) | Map marker widget | 4 | yes |
| [hud/ag_chat_input.layout](advanced-groups/hud/ag_chat_input.html) | Chat input bar | 5 | yes |
| [hud/ag_chat_item.layout](advanced-groups/hud/ag_chat_item.html) | Chat message row | 7 | yes |
| [hud/ag_chat_root.layout](advanced-groups/hud/ag_chat_root.html) | Chat history box | 4 | yes |
| [hud/ag_main_menu.layout](advanced-groups/hud/ag_main_menu.html) | Advanced Groups main menu shell | 22 | yes |
| [hud/ag_map_legend.layout](advanced-groups/hud/ag_map_legend.html) | Map legend box | 4 | yes |
| [hud/ag_map_legend_row.layout](advanced-groups/hud/ag_map_legend_row.html) | Map legend row | 3 | yes |
| [hud/ag_marker_icon_button.layout](advanced-groups/hud/ag_marker_icon_button.html) | Marker icon button | 2 | yes |
| [hud/ag_marker_list_entry.layout](advanced-groups/hud/ag_marker_list_entry.html) | Marker list row | 8 | yes |
| [hud/ag_marker_list_header.layout](advanced-groups/hud/ag_marker_list_header.html) | Marker list section header | 6 | yes |
| [hud/ag_marker_zone_panel.layout](advanced-groups/hud/ag_marker_zone_panel.html) | Zone panel on the map | 24 | yes |
| [hud/ag_page_admin.layout](advanced-groups/hud/ag_page_admin.html) | Admin page | 90 | yes |
| [hud/ag_page_group.layout](advanced-groups/hud/ag_page_group.html) | Group page | 60 | yes |
| [hud/ag_page_info.layout](advanced-groups/hud/ag_page_info.html) | Info page | 39 | yes |
| [hud/ag_page_mailbox.layout](advanced-groups/hud/ag_page_mailbox.html) | Mailbox page | 43 | yes |
| [hud/ag_page_marker_popup.layout](advanced-groups/hud/ag_page_marker_popup.html) | Marker editor popup | 61 | yes |
| [hud/ag_page_markers.layout](advanced-groups/hud/ag_page_markers.html) | Markers page | 11 | yes |
| [hud/ag_page_public_groups.layout](advanced-groups/hud/ag_page_public_groups.html) | Public groups page | 31 | yes |
| [hud/ag_page_settings.layout](advanced-groups/hud/ag_page_settings.html) | Settings page | 352 | yes |
| [hud/ag_spawn_menu.layout](advanced-groups/hud/ag_spawn_menu.html) | Spawn selection menu | 16 | yes |
| [hud/ag_top_button.layout](advanced-groups/hud/ag_top_button.html) | Main menu tab button | 4 | yes |
| [hud/ag_zone_card_entry.layout](advanced-groups/hud/ag_zone_card_entry.html) | Zone card row | 3 | yes |
| [hud/ag_zone_card_header.layout](advanced-groups/hud/ag_zone_card_header.html) | Zone card header | 4 | yes |
| [hud/ag_zone_editor.layout](advanced-groups/hud/ag_zone_editor.html) | Zone Editor (admin) | 45 | yes |
| [hud/compass.layout](advanced-groups/hud/compass.html) | Compass bar | 8 | yes |
| [hud/hud_root.layout](advanced-groups/hud/hud_root.html) | HUD root | 4 | yes |
| [hud/infopanel.layout](advanced-groups/hud/infopanel.html) | Info panel | 3 | yes |
| [hud/marker_label.layout](advanced-groups/hud/marker_label.html) | 3D marker label | 4 | yes |
| [hud/minimap.layout](advanced-groups/hud/minimap.html) | Minimap | 5 | yes |
| [hud/minimap_blip.layout](advanced-groups/hud/minimap_blip.html) | Minimap blip | 3 | yes |
| [hud/playerlist.layout](advanced-groups/hud/playerlist.html) | Group player list | 4 | yes |
| [hud/playerlist_member_row.layout](advanced-groups/hud/playerlist_member_row.html) | Player list row | 7 | yes |
| [menu/invite_menu.layout](advanced-groups/menu/invite_menu.html) | Group invite prompt | 7 | yes |
| [suite/lsc_collection_row.layout](advanced-groups/suite/lsc_collection_row.html) | List header | 20 | yes |
| [suite/lsc_color_cell.layout](advanced-groups/suite/lsc_color_cell.html) | Colour swatch | 4 | yes |
| [suite/lsc_color_modal.layout](advanced-groups/suite/lsc_color_modal.html) | Colour picker | 29 | yes |
| [suite/lsc_console.layout](advanced-groups/suite/lsc_console.html) | Control Room window | 186 | yes |
| [suite/lsc_diff_row.layout](advanced-groups/suite/lsc_diff_row.html) | Review change row | 13 | yes |
| [suite/lsc_field_row.layout](advanced-groups/suite/lsc_field_row.html) | Setting row | 58 | yes |
| [suite/lsc_header_row.layout](advanced-groups/suite/lsc_header_row.html) | Section header | 4 | yes |
| [suite/lsc_history_row.layout](advanced-groups/suite/lsc_history_row.html) | Version history row | 19 | yes |
| [suite/lsc_item_row.layout](advanced-groups/suite/lsc_item_row.html) | Record row | 41 | yes |
| [suite/lsc_lines_row.layout](advanced-groups/suite/lsc_lines_row.html) | List setting row | 29 | yes |
| [suite/lsc_map_modal.layout](advanced-groups/suite/lsc_map_modal.html) | Map picker | 30 | yes |
| [suite/lsc_module_row.layout](advanced-groups/suite/lsc_module_row.html) | Module card / rail row | 7 | yes |
| [suite/lsc_note_row.layout](advanced-groups/suite/lsc_note_row.html) | Note row | 2 | yes |
| [suite/lsc_section_row.layout](advanced-groups/suite/lsc_section_row.html) | Section rail row | 6 | yes |

## Advanced Banking

| Layout | Purpose | Widgets | In use |
|---|---|---|---|
| [BankingMenu.layout](advanced-banking/BankingMenu.html) | Old banking menu (unused) | 41 | no |
| [BankingMenuTabbed.layout](advanced-banking/BankingMenuTabbed.html) | Banking menu (ATM) | 81 | yes |
| [ab_suite_config_editor.layout](advanced-banking/ab_suite_config_editor.html) | Legacy banking config editor (fallback) | 316 | yes |
| [lemmy_suite_admin.layout](advanced-banking/lemmy_suite_admin.html) | Legacy suite admin hub (fallback) | 35 | yes |

{% endraw %}
