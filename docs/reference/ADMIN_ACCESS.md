---
layout: page
title: "Admin access"
section: DOCUMENTATION
permalink: /docs/reference/ADMIN_ACCESS.html
---
{% raw %}
# Admin access

`server_config.json` → `adminIds` remains the full-owner list. An existing owner can open **Admin Config Studio → Staff Access** to create a role and assign one Steam64 ID to it. Roles and assignments are stored separately in `$profile:AdvancedGroups/staff_access.json`, with a revision check to reject stale saves. Removing an assignment does not remove an owner from `adminIds`.

Enter grant keys as a comma-separated list. Only recognized keys can be saved:

| Area | Grants |
| --- | --- |
| Command Center | `groups.view`, `groups.members.manage`, `groups.identity.edit`, `groups.delete`, `groups.join`, `markers.group.manage`, `markers.server.edit`, `players.teleport`, `chat.mute` |
| Zones | `zones.view`, `zones.edit` |
| Status | `status.view` |
| Config Studio | `config.general.edit`, `config.gps.edit`, `config.chat.edit`, `config.display.edit`, `config.info.edit`, `config.integrations.edit`, `config.events.edit`, `config.tiers.edit` |

The Config Studio hides unassigned sections. Staff saves send only the current section and the server checks its grant before applying the fields. Full config saves, the `adminIds` field, disk reloads, admin logs, and role administration remain owner-only. `zones.view` hides zone-editing controls; `zones.edit` permits changes. The server checks permissions independently of the UI.

`players.teleport` enables the map popup's TP action. `chat.mute` currently authorizes the moderation RPC for integrations; the Command Center does not yet have mute/unmute buttons.

For the chat filter, the default list includes common English profanity and equivalents in German, Spanish, French, Portuguese, Polish, and Russian. It is a starter list, not a linguistic or hate-speech classifier. The filter remains disabled until enabled in **Chat**, matches whole terms case-insensitively, and can be edited or cleared in-game. Migrating a pre-v13 config with a non-empty custom list preserves that list; an empty old list receives the starter list.

{% endraw %}
