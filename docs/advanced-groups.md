---
layout: page
title: "Advanced Groups"
section: DOCUMENTATION
permalink: /docs/advanced-groups.html
---
{% raw %}
# Advanced Groups

Groups, squads, chat, markers and map tools for DayZ, plus territories, protected zones and spawn selection. Every server setting is listed in the [Advanced Groups settings reference](settings/advanced-groups.html); the screens are in the [layout reference](layouts/index.html#advanced-groups).

## For players

### The group menu (O)

Press **O** to open the group menu. Tabs along the top:

| Tab | What it is | Layout |
|---|---|---|
| Info | Server name, rules and guides, Discord/website/store links | `ag_page_info` |
| Group | Your group: create, rename, members, ranks, invite, kick, leave, subgroups, colour and tag | `ag_page_group` |
| Markers | The full map with group, private, server and event markers | `ag_page_markers` |
| Settings | Your own HUD, chat and colour settings (saved on your PC) | `ag_page_settings` |
| Public | Public service groups (Taxi, Medic...) you can join next to your own group | `ag_page_public_groups` |
| Mailbox | Messages between groups and staff | `ag_page_mailbox` |
| Admin / Zones | Staff only, see [For admins](#for-admins) | `ag_page_admin` |

### Groups and ranks

- One group per player. Ranks: **Member**, **Officer**, **Co-Leader**, **Leader**. The lowest rank that may invite, kick and promote is set by the server (*Group admin panel opens from rank*).
- **Inviting:** the server may require you to stand close to the player (*Invite in person only*). An invitation expires after a set time; the invited player gets an accept/decline prompt (`invite_menu`).
- **Cooldowns:** servers can make players wait before switching or rejoining groups, and count kicks as leaving.
- **Subgroups:** split a group into squads with their own chat channel.
- **Tiers:** admins can put a group in a tier (VIP, Admin...) that changes its member, subgroup and marker limits and its chat name colour.
- **Inactive groups** can be removed automatically after a number of days with nobody online.

### Chat

Advanced Groups replaces the vanilla chat.

| Channel | Who reads it |
|---|---|
| Global | Everyone (if the server allows global chat) |
| Group | Your group |
| Subgroup | Your squad (assign yourself to a subgroup first) |
| Vicinity | Players within the vicinity range |
| Server | Announcements and system messages (read only) |

- **Y** cycles the channel. **Enter** opens the input.
- Long messages wrap over several rows. **Page Up / Page Down** scroll; a *New messages below* hint shows when you scrolled up.
- Server announcements and system notices fade out and are not kept in the history.
- Coloured tags (ADMIN, VIP...) can be given to players by the server.
- `/reply <text>` answers the last player who mentioned you in global chat. `/votemute <name>` starts a vote mute (if enabled). `/chat ...` changes the chat box — see [Keybinds and chat commands](keybinds-and-commands.html).
- A word filter can replace bad words and mute the sender for a while.

### Map, markers and HUD

- **M** opens the map. Group markers are shared with your group; private markers are yours only. Markers can have an area circle with diagonal or cross-hatch lines (if the server allows circles).
- **T** pings the spot you look at for your group.
- **Server markers** (traders, danger areas, landmarks) and **event markers** (heli crashes, convoys...) are placed by the server.
- **K** cycles 3D markers: all → off → server only → group only → private only → events only.
- **B** toggles the GPS / minimap. **H** hides the whole HUD.
- The server may require items for the map, compass, minimap or seeing teammates (*Map, GPS and markers* settings).
- The **minimap** shows you as a direction arrow (the same icon as on the full map), turning with you.
- The **group list** (top left) shows the group tag in the group's colour, then one row per member: name, rank, health percent, a health bar (green → yellow → red) and a thin blood bar under it.
- HUD parts: compass bar (`compass`), minimap (`minimap`), group player list (`playerlist`), info panel (`infopanel`), 3D marker labels (`marker_label`).

### Territories and zones

- Building a **territory flagpole** claims land around it for your group. Others may be blocked from building and dismantling there; intruders who log in inside are moved out.
- **Safe zones** block all damage; **no-build zones** block building; **PvE / PvP zones** change damage rules locally.
- Zones are circles or polygons. On the map and minimap each one is drawn in its colour as an outline, with strike lines or with cross-hatching (the server picks per zone). A zone can carry a name and an icon in its middle — both optional.
- *Enter and leave notices* tell you when you cross a zone or territory border.

### Spawn selection

Fresh characters can be offered a map of spawn points — see [Spawn Selection](spawn-selection.html).

## For admins

### Opening the tools

- **U** opens the [Control Room](control-room.html) for every setting of the mod.
- In the Control Room, **GROUP MANAGER** opens the full group editor (admin page of the group menu). Zones and server markers are edited in their Control Room sections with the map picker.

### Staff permissions

Besides Control Room access, Advanced Groups has its own staff grants for the in-game admin pages:

| Grant | Allows |
|---|---|
| `status.view` | Server status page |
| `groups.view` | See every group |
| `groups.identity.edit` | Rename groups, change tier |
| `groups.members.manage` | Add/remove members, transfer leadership |
| `groups.join` | Join any group |
| `groups.delete` | Disband groups |
| `markers.group.manage` | Edit any group's markers |
| `markers.server.edit` | Place and edit server markers |
| `zones.view` / `zones.edit` | Zone Editor |
| `players.teleport` | Teleport to players and positions |
| `chat.mute` | Mute players |
| `config.*.edit` | Legacy config pages (general, chat, display, gps, info, integrations, tiers, events) |

Owners listed under *Owners* in the Control Room have every grant.

### What admins configure

All in the Control Room ([full reference](settings/advanced-groups.html)):

- **Groups** — size limits, invitations, cooldowns, cleanup, banned name words, **tiers**, **public service groups**.
- **Chat and moderation** — channels, announcements, vicinity range, word filter, mute system, **chat tags**.
- **Protection** — server-wide PvE, friendly fire, safe-zone rules, enter and leave notices.
- **Safe and no-build zones** — every zone in one list: type (safe, no-build, PvE, PvP, map area only, territory), circle or polygon (placed with the map picker), colour, map fill (outline, strike lines, cross-hatch), optional name and icon, friendly fire and priority.
- **Territories** — flag radius, spacing, limits, owner-only building and dismantling, login teleport, map display.
- **Map, GPS and markers** — item requirements, player circles, **map legend**, **server markers** (placed with the map picker), **marker icon styles**.
- **HUD defaults** — what new players see.
- **Discord webhooks** — group and chat events.
- **Server information** — links and **info pages**.
- **Event markers** — automatically mark world events by class name.
- **Owners** — full Advanced Groups admin rights.

### Logs

`LemmysSuite\Logs\AdvancedGroups\current.log` (events, reloads, admin checks) and `chat.log`. Discord webhooks can mirror group events and chat.

{% endraw %}
