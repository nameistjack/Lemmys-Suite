---
layout: page
title: Advanced Groups
section: CLIENT + SERVER MOD
permalink: /groups/
---

# Advanced Groups

<p class="page-links"><a class="button primary" href="{{ site.links.workshop_groups }}" target="_blank" rel="noreferrer">Steam Workshop</a> <a class="button secondary" href="{{ site.links.discord }}" target="_blank" rel="noreferrer">Discord support</a></p>

Advanced Groups is the large one. It replaces the vanilla chat and map and adds groups with ranks, a minimap, compass, 3D markers, zones, territories, an optional spawn selector and a group manager for admins. Players need it too, so it goes in `-mod`; the server also needs [Lemmy's Core]({{ site.baseurl }}/core/) as a `-serverMod`. The full player and admin guide is in the [documentation]({{ site.baseurl }}/docs/advanced-groups.html), every setting in the [settings reference]({{ site.baseurl }}/docs/settings/advanced-groups.html).

## Default keys

All keys can be rebound under **Controls → Advanced Groups**.

| Key | Action |
|---|---|
| O | Group menu |
| M | Map |
| H | Toggle the HUD (compass, minimap, player list) |
| Y | Cycle chat channel (Tab also works while typing) |
| T | Ping the spot you are looking at |
| B | Toggle GPS / minimap |
| K | Toggle 3D markers |
| U | Admin mode, which also opens the Control Room for suite admins |

## HUD

- **Minimap** (B): you are the same direction arrow as on the full map, turning with you.
- **Group list** (top left): the group tag in the group's colour, then one row per member with name, rank, health percent, a health bar (green → yellow → red) and a thin blood bar.
- **Compass bar**, **3D markers** (K cycles all / off / server / group / private / events) and an info panel. **H** hides the whole HUD.

## Groups

- Ranks run from member up to leader. Invite, kick, promote and subgroups are limited by rank. `adminMenuMinRank` sets the lowest rank that sees the group admin tools.
- **Tiers** (`categories`) override the member, subgroup and marker limits for groups an admin assigns, for example a VIP tier with 20 markers.
- **Group hopping:** `groupHopCooldownMinutes` makes a player wait after leaving before they can join or create another group. `groupRejoinCooldownMinutes` does the same for rejoining the old group. With `groupHopCountsKicks` on, being kicked also counts as leaving.
- **Invites:** `inviteCooldownSeconds` stops one player spamming invites at another. `inviteMaxDistance` above 0 means invites only work in person.
- `bannedGroupWords` blocks group names and tags containing any of the words.
- **Public services** (Taxi, Medic and so on) are separate from private groups. A player can be in both. Only owners in `adminIds` can manage them.

## Markers

Double-click the map to place a marker, double-click an existing one to edit it, and drag a marker to move it.

The popup has:

- **Icon and colour**: 82 icons, RGB sliders.
- **Visible on**: map, 3D or both.
- **Private**: only you see it, even inside a group.
- **Area row**:
  - **My position** puts the marker where you stand. On an existing marker it moves the marker there when you confirm.
  - **Radius** draws a circle. Players are capped at `playerMarkerMaxRadius` (default 500 m) and admins are not. `playerMarkerCircles: false` hides the radius for players.
  - **Strike** cycles between none, lines and cross-hatch.
  - **Lines** cycles the hatch colour: circle colour, red, orange, yellow, white or black.
- **Server marker** (admin mode only): everyone sees it, and it is saved in the server config.
- **Teleport here** shows only for staff with `players.teleport`.

Event markers (heli crashes, convoys and so on) are configured by class name in `event_markers.json`. See the [event marker docs]({{ site.baseurl }}/docs/reference/EVENT_MARKER_CONFIG.html).

**Awareness items.** Each list is empty by default, which means no item is needed:

| Setting | Needs an item for |
|---|---|
| `mapRequiredItems` | opening the map (for example `ChernarusMap`) |
| `compassRequiredItems` | the compass bar |
| `teammateRequiredItems` | seeing teammates on the map, minimap and in 3D (for example a radio) |
| `gpsItems` | counting as a GPS; empty means any item whose name contains GPS or compass |

The **map legend** (`mapLegend`) adds a key in the bottom right of the map: an icon, a label and a colour per row.

## Chat

Channels are Global, Vicinity (`vicinityRange`, default 100 m), Group and Subgroup. There is also a receive-only Server channel for notices.

**For players:**

- Long messages wrap onto extra lines. You can drag the scrollbar while chat is open.
- Page Up/Down scroll a page and the mouse wheel scrolls three lines. If you scrolled up and something new arrives, a "New messages below" line appears instead of yanking you down.
- A channel hidden in Settings keeps its messages; turn it back on and they are still there.
- `@Full Player Name` in Global notifies that player. `/reply message` answers the last person who mentioned you.
- Chat box layout commands (only you see these):

```text
/chat size 10-24       text size
/chat width 900        box width
/chat height 240       box height
/chat pos 20 200       distance from the left and bottom edges
/chat fade 45          seconds before a line fades, 0 = never
/chat time             show or hide the time stamps
/chat reset            back to defaults
```

**Moderation:**

| Setting | Effect |
|---|---|
| `chatSlowGlobalSeconds`, `chatSlowVicinitySeconds`, `chatSlowGroupSeconds` | wait between messages per player; admins are exempt |
| `chatLockGlobal`, `chatLockVicinity` | only admins can write there |
| `enableBadWordFilter`, `badWords` | whole-word filter, starter list in seven languages |
| `badWordMuteMinutes` | above 0, a filtered word mutes the writer and the message is dropped |
| `enableMuteVotes` and the `muteVote*` settings | `/votemute Player Name` starts or joins a vote; the defaults need 5 players online and 50% agreeing for a 15 minute mute |

Mutes and vote state are kept in `moderation.json` and survive restarts.

## Zones

There are six zone types. Each can be a circle or a polygon of up to 64 points.

| Type | Rule | Map hatch |
|---|---|---|
| Safe zone | Nobody inside takes damage from anything. With `safeZoneBlockOutgoing` (default on), nobody inside can hurt players outside | cross-hatch |
| No-build | No building, deploying or placing | lines |
| PvE | No player-versus-player damage | lines |
| PvP | Player damage allowed even with server-wide PvE on | lines |
| Territory | Belongs to the group named in **Owner group** (see below) | lines |
| Visual | Only drawn, no rules | outline |

**Team damage per zone:** Inherit, Allow, Block group or Block all. Where zones overlap, the one with the higher **priority** wins.

**How zones look.** Each zone is drawn on the map and minimap in its colour. **Map fill** picks an outline, strike lines or cross-hatch; *Default* uses the hatch in the table above. **Name** and **map icon** are both optional — a zone with an icon and no rules (*Map area only*) works as a polygon server marker. Hatching keeps the same spacing on screen at every zoom level and does not swim while you pan.

**Editing zones.** Control Room → Advanced Groups → **Safe and no-build zones**. **+ ADD** a zone, pick its type and shape, then:

- **Circle:** **PICK ON MAP** for the centre and type the radius.
- **Polygon:** **ADD ON MAP** on *Polygon corners* and click around the area. Every click adds a numbered corner; **UNDO POINT** removes the last one. At least 3 corners.
- Every other zone is drawn in grey while you place, so overlaps are visible. **APPLY LIVE** sends it to every player at once.

The older Admin → Zones editor and the separate *Safe zones* / *No-build zones* lists are gone; old entries are moved into the one zone list automatically.

With `zoneEnterMessages` on, players get "Entering Safe zone: Green Mountain" and "Leaving ..." notices.

## Territories

Territories are off until `territoriesEnabled` is turned on in the Control Room (**Advanced Groups → Territories**).

- Building the **pole** of a vanilla territory flag claims a circle of `territoryRadius` (default 60 m) for the builder's group. The group gets a notice, and the territory shows on everyone's map and minimap in the group colour.
- A new flag must be `territoryMinDistance` (default 150 m) away from other groups' flags. `territoryMaxPerGroup` limits flags per group (default 1, 0 = unlimited). The flag kit's hologram turns red where a claim isn't allowed.
- `territoryBuildOwnersOnly`: outsiders can't build or place items inside.
- `territoryDismantleOwnersOnly`: outsiders can't dismantle base parts. Raiding with tools or explosives is not affected.
- `territoryLoginTeleport`: a player who logs in inside someone else's territory is moved 15 m past the edge and told why. Admins are never moved.
- **Losing a claim:** the server checks claims every minute. If the flagpole is gone (dismantled, destroyed or deleted) or the group is disbanded, the claim is released and the group is told. For the first three minutes after a restart nothing is released, so persistence has time to load the flags.
- **Admin territories:** create a zone of type **Territory** and type the group name into **Owner group**. These follow the same build rules but don't need a flag.
- Claims are saved in `territories.json` next to the groups folder.

Players see "Entering your territory" or "Entering territory of Wolves" as they cross the line.

## Spawn selection

Spawn selection is off by default. It opens a location picker for fresh characters only; living characters are never moved. Points have a radius, an optional list of exact positions and a cooldown. The packed coordinates are Chernarus examples, so set your own before enabling it on another map. See the [spawn module notes]({{ site.baseurl }}/docs/reference/SPAWN_MODULE.html).

## Admin tools

- **Group manager** (Control Room → Advanced Groups → **GROUP MANAGER**): every group, its members, markers and colour, plus rename, join, kick, change rank, tier, leader transfer, disband, teleport, and delete or move markers.
- **Staff roles** give single permissions instead of full admin. The full list is in [Admin access]({{ site.baseurl }}/docs/reference/ADMIN_ACCESS.html). The ones people ask about most are `zones.edit`, `players.teleport` and `markers.server.edit`.
- The suite administrators in `LemmysSuite/General/suite.json` and the Advanced Groups **Owners** list have every grant.

## Settings added in this build

These are all editable in the Control Room. Defaults are shown.

| Setting | Default | |
|---|---|---|
| `playerMarkerCircles` | `true` | players may draw marker circles |
| `playerMarkerMaxRadius` | `500` | metres, 0 = no cap |
| `safeZoneBlockOutgoing` | `true` | no shooting out of safe zones |
| `zoneEnterMessages` | `true` | enter and leave notices |
| `territoriesEnabled` | `false` | |
| `territoryRadius` | `60` | |
| `territoryMinDistance` | `150` | |
| `territoryMaxPerGroup` | `1` | |
| `territoryBuildOwnersOnly` | `true` | |
| `territoryDismantleOwnersOnly` | `true` | |
| `territoryLoginTeleport` | `false` | |
| `territoryShowOnMap` | `true` | |
| zone `strikeStyle` | `0` | map fill: 0 default for the type, 1 outline, 2 strike lines, 3 cross-hatch |
| zone `iconType` | `-1` | optional icon in the middle of the zone, -1 = none |
| zone `name` | `""` | optional; empty draws no label |
