---
layout: page
title: "Advanced Groups settings"
section: DOCUMENTATION
permalink: /docs/settings/advanced-groups.html
---
{% raw %}
# Advanced Groups settings

Every setting the Control Room shows for this module, in the order it shows them. Values are applied live when you press **APPLY LIVE** unless the setting is tagged *restart*.

**Tags:** *careful* — asks for a note and is highlighted; *restart* — saved now, used after the next restart; *advanced* — hidden until SHOW ADVANCED; *read only* — shown for reference; *required* — cannot be empty.


## Groups

Size limits, invitations and housekeeping for player groups.

Section id: `groups` · stored in `AGServerConfig`

| Setting | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **Members per group**  | `maxGroupSize` | Whole number | 1 – 100 members | `20` | Largest group allowed when the group has no tier. Tiers below can raise or lower this per group. |
| **Subgroups per group**  | `maxSubgroups` | Whole number | 0 – 20 subgroups | `5` | How many squads a group may split into. |
| **Shared markers per group**  | `maxMarkersPerGroup` | Whole number | 0 – 100 markers | `10` | Map markers a group can keep at the same time. |
| **Invitation expires after**  | `inviteTimeoutSeconds` | Whole number | 10 – 3600 seconds | `120` | An unanswered invitation is withdrawn after this long. |
| **Group admin panel opens from rank**  | `adminMenuMinRank` | Choice | 0 = Member<br>1 = Officer<br>2 = Co-Leader<br>3 = Leader | `AGRank.LEADER` | Lowest rank that can manage the group (invite, kick, promote). |
| **Death markers stay private**  | `deathMarkerPrivate` | On / off |  | `false` | When on, a player's death marker is saved to their own private markers instead of the group's. |
| **Show last position of offline members**  | `showOfflinePositions` | On / off |  | `false` | Members can see where an offline teammate logged out. |
| **Delete inactive groups after**  | `inactiveGroupCleanupDays` | Whole number | 0 – 3650 days | `30` | Groups with no member online for this many days are removed. 0 keeps groups forever. |
| **Cleanup check interval** *advanced* | `groupCleanupIntervalSeconds` | Number | 30 – 86400 seconds | `300.0` | How often the server looks for inactive groups. |
| **Wait before switching groups**  | `groupHopCooldownMinutes` | Whole number | 0 – 10080 minutes | `0` | After leaving a group, a player waits this long before joining or creating another one. 0 = off. |
| **Wait before rejoining**  | `groupRejoinCooldownMinutes` | Whole number | 0 – 10080 minutes | `0` | After leaving, a player waits this long before rejoining the same group. 0 = off. |
| **Kicks count as leaving**  | `groupHopCountsKicks` | On / off |  | `false` | Kicked players also get the waiting time above. |
| **Invite cooldown**  | `inviteCooldownSeconds` | Whole number | 0 – 3600 seconds | `30` | How long before the same player can be invited again by the same person. |
| **Invite in person only**  | `inviteMaxDistance` | Number | 0 – 1000 m | `0` | Players must stand this close to invite someone. 0 = invite from anywhere. |
| **Banned words in group names**  | `bannedGroupWords` | List (one per line) |  | `(empty)` | Group names and tags containing any of these are refused. One per line, case-insensitive. |

### List: Group tiers

Tiers override the limits above for groups an admin assigns to them (for example VIP or Admin).

List id: `categories` · up to 50 tier records · record type `AGGroupCategory`

| Field | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **Tier name** *required* | `categoryName` | Text |  | `"Default"` | Shown to admins and used to assign groups to this tier. |
| **Tier colour**  | `displayColor` | Colour (RRGGBB) |  | `"FFFFFF"` | Colour of the tier label. |
| **Chat name colour**  | `playerNameColor` | Colour (RRGGBB) |  | `"FFD778"` | Colour of member names in chat for groups in this tier. |
| **Members per group**  | `maxGroupSize` | Whole number | 1 – 100 members | `20` | Replaces the global member limit for this tier. |
| **Subgroups**  | `maxSubgroups` | Whole number | 0 – 20 subgroups | `5` | Replaces the global subgroup limit. |
| **Shared markers**  | `maxMarkersPerGroup` | Whole number | 0 – 100 markers | `10` | Replaces the global marker limit. |
| **Ignore invitation cap**  | `bypassInviteCap` | On / off |  | `false` | Groups in this tier can invite past the member limit. |
| **List in admin tools**  | `showOnAdminMenu` | On / off |  | `true` | Show this tier in the admin group tools. |


### List: Public service groups

Groups any player can join next to their own group, such as Taxi or Medic. Members are kept when you edit a group.

List id: `publicGroups` · up to 30 service group records · record type `AGPublicServiceGroup`

| Field | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **Name** *required* | `name` | Text |  | `""` | Shown in the public groups list. |
| **Description**  | `description` | Text |  | `""` | One line telling players what the group is for. |
| **Colour**  | `color` | Colour (RRGGBB) |  | `"FFFFFF"` | Colour of the group name. |


## Chat and moderation

Channels, announcements and the word filter.

Section id: `chat` · stored in `AGServerConfig`

| Setting | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **Global chat**  | `allowGlobalChat` | On / off |  | `true` | Players can write to everyone on the server. |
| **Vicinity chat range**  | `vicinityRange` | Number | 1 – 1000 m | `100.0` | Players within this distance receive vicinity messages. |
| **Announce joins**  | `announcePlayerJoin` | On / off |  | `true` | Post a chat line when a player connects. |
| **Announce leaves**  | `announcePlayerLeave` | On / off |  | `true` | Post a chat line when a player disconnects. |
| **Mute system**  | `enableMuteSystem` | On / off |  | `true` | Admins can mute players in chat. |
| **Word filter**  | `enableBadWordFilter` | On / off |  | `false` | Mask the words below in chat messages. |
| **Filtered words**  | `badWords` | List (one per line) |  | `(empty)` | One word per line. Matching is case-insensitive. |
| **Mute for filtered words**  | `badWordMuteMinutes` | Whole number | 0 – 10080 minutes | `0` | Writing a filtered word mutes the player this long and the message is not sent. 0 = only mask the word. |
| **Drop messages with filtered words**  | `badWordBlockMessage` | On / off |  | `false` | Messages with a filtered word are not sent at all, even without a mute. |
| **Slow mode: global**  | `chatSlowGlobalSeconds` | Whole number | 0 – 600 seconds | `0` | Pause between messages per player. 0 = off. Admins are exempt. |
| **Slow mode: vicinity**  | `chatSlowVicinitySeconds` | Whole number | 0 – 600 seconds | `0` | Pause between messages per player. 0 = off. |
| **Slow mode: group and subgroup**  | `chatSlowGroupSeconds` | Whole number | 0 – 600 seconds | `0` | Pause between messages per player. 0 = off. |
| **Lock global chat**  | `chatLockGlobal` | On / off |  | `false` | Only admins can write in global chat while this is on. |
| **Lock vicinity chat**  | `chatLockVicinity` | On / off |  | `false` | Only admins can write in vicinity chat while this is on. |
| **Mute votes**  | `enableMuteVotes` | On / off |  | `false` | Players can type /votemute <name> to vote a player into a temporary mute. |
| **Players needed for a vote**  | `muteVoteMinPlayers` | Whole number | 2 – 200 players | `5` | Votes cannot start with fewer players online. |
| **Votes needed**  | `muteVotePercent` | Whole number | 1 – 100 % | `50` | Share of online players that must agree. |
| **Vote mute length**  | `muteVoteMinutes` | Whole number | 1 – 1440 minutes | `15` | How long a vote mute lasts. |
| **Vote time window**  | `muteVoteWindowSeconds` | Whole number | 30 – 1800 seconds | `120` | Votes older than this no longer count. |

### List: Chat tags

Give specific players a coloured tag in front of their name, such as ADMIN or VIP.

List id: `chatIdentities` · up to 200 tag records · record type `AGChatIdentity`

| Field | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **SteamID64** *required* | `steamId` | SteamID64 |  | `""` | The player who gets the tag. |
| **Tag text** *required* | `displayTag` | Text |  | `"ADMIN"` | Shown in brackets before the name. |
| **Tag colour**  | `color` | Colour (RRGGBB) |  | `"FF4444"` | Colour of the tag. |


## Protection

Damage rules. The zones themselves are in [Safe and no-build zones](#safe-and-no-build-zones).

Section id: `protection` · stored in `AGServerConfig`

| Setting | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **Server-wide PvE** *careful* | `enablePvPProtection` | On / off |  | `false` | Blocks ALL player-versus-player damage everywhere. Damage from AI, animals and the environment still applies. |
| **Block friendly fire**  | `blockGroupFriendlyFire` | On / off |  | `true` | Members of the same group cannot damage each other. |
| **No shooting out of safe zones**  | `safeZoneBlockOutgoing` | On / off |  | `true` | Players standing in a safe zone cannot hurt players outside it. |
| **Enter and leave notices**  | `zoneEnterMessages` | On / off |  | `true` | Tell players when they enter or leave a named zone or a territory. |

## Safe and no-build zones

Every protected or marked area, as a circle or a polygon. Pick the zone type, then the shape. (The older separate *Safe zones* and *No-build zones* lists are moved into this list automatically on every start.)

Section id: `areas` · stored in `AGServerConfig`

### List: Zones (circle or polygon)

Circle: set the centre and radius. Polygon: click ADD ON MAP and click the corners. *Map area only* plus an icon works as a polygon server marker.

List id: `zones` · up to 200 zone records · record type `AGZoneDefinition`

| Field | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **Name** *optional* | `name` | Text |  | `""` | Shown on the map and in enter/leave notices. Leave empty for no label. |
| **Active**  | `enabled` | On / off |  | `true` | Off keeps the zone but ignores it. |
| **Zone type**  | `type` | Choice | 0 = Safe zone<br>1 = No-build zone<br>2 = PvE zone<br>3 = PvP zone<br>4 = Map area only<br>5 = Territory | `AGZoneType.VISUAL` | What the zone does. |
| **Shape**  | `shape` | Choice | 0 = Circle<br>1 = Polygon | `AGZoneShape.CIRCLE` | Circle uses centre and radius. Polygon uses the corner points. |
| **Centre**  | `center` | Position (x y z) |  | `vector.Zero` | Circle centre. Polygons use it for the map label. |
| **Radius**  | `radius` | Number | 1 – 20000 m | `100.0` | Circle radius. |
| **Polygon corners**  | `vertices` | Positions (one per line) |  | `(empty)` | One corner per line, in order around the area. At least 3. Use ADD ON MAP and click around the area. |
| **Colour**  | `color` | Colour (RRGGBB) |  | `"FFFFFF"` | Colour of the outline and strike lines on the map. |
| **Map fill**  | `strikeStyle` | Choice | 0 = Default for the zone type<br>1 = Outline only<br>2 = Strike lines<br>3 = Cross-hatch | `0` | How the inside of the zone is drawn on the map and minimap. The default is cross-hatching for safe zones, an outline for *Map area only*, and strike lines for every other type. |
| **Map icon** *optional* | `iconType` | Choice | None, or any marker type | `-1` (None) | Icon drawn in the middle of the zone. None draws only the name. |
| **Show on map**  | `showOnMap` | On / off |  | `true` | Players see this zone on the map. |
| **Friendly fire**  | `friendlyFire` | Choice | -1 = Server default<br>0 = Allowed<br>1 = Blocked within groups<br>2 = Blocked for everyone | `AGZoneFriendlyFire.INHERIT` | Damage between players inside this zone. |
| **Priority**  | `priority` | Whole number | -100 – 100 | `0` | Where zones overlap, the higher number wins. |
| **Owning group**  | `ownerGroup` | Text |  | `""` | Territory zones only: the group that owns it. |

Hatching keeps the same on-screen spacing at every zoom level and is anchored to the map grid, so it does not swim while you pan.

## Territories

Groups claim land by building a territory flagpole. Admins can also hand any zone of type Territory to a group in the Zone Editor.

Section id: `territories` · stored in `AGServerConfig`

| Setting | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **Territories on**  | `territoriesEnabled` | On / off |  | `false` | Building the pole of a territory flag claims the land around it for the builder's group. |
| **Territory radius**  | `territoryRadius` | Number | 10 – 1000 m | `60` | Land claimed around each flag. |
| **Distance to other groups**  | `territoryMinDistance` | Number | 0 – 5000 m | `150` | A new flag must be at least this far from another group's flag. |
| **Territories per group**  | `territoryMaxPerGroup` | Whole number | 0 – 50 flags | `1` | How many flags one group may hold. 0 = no limit. |
| **Only owners build inside**  | `territoryBuildOwnersOnly` | On / off |  | `true` | Players outside the owning group cannot build or place items in the territory. |
| **Only owners dismantle inside**  | `territoryDismantleOwnersOnly` | On / off |  | `true` | Outsiders cannot dismantle base parts. Raiding with tools or explosives still works. |
| **Move intruders out on login**  | `territoryLoginTeleport` | On / off |  | `false` | Players who log in inside another group's territory are placed just outside it. |
| **Show territories on the map**  | `territoryShowOnMap` | On / off |  | `true` | Draw every claimed territory in its group colour. |

## Map, GPS and markers

What players need to see positions, and how marker types look.

Section id: `map` · stored in `AGServerConfig`

| Setting | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **GPS item required**  | `gpsItemRequired` | On / off |  | `false` | Players need a GPS item to see the minimap and teammates. |
| **GPS only in vehicles**  | `gpsVehicleOnly` | On / off |  | `false` | The minimap only works while driving or flying. |
| **Vehicles count as GPS**  | `gpsInVehiclesBypassesItem` | On / off |  | `true` | Sitting in a vehicle works like carrying a GPS item. |
| **GPS items**  | `gpsItems` | List (one per line) |  | `(empty)` | Class names that count as a GPS, one per line. Empty = any item whose name contains GPS or compass. |
| **Map needs an item**  | `mapRequiredItems` | List (one per line) |  | `(empty)` | Class names, one per line (for example ChernarusMap). Players need one of them to open the map. Empty = no item needed. |
| **Compass needs an item**  | `compassRequiredItems` | List (one per line) |  | `(empty)` | Class names, one per line. The compass bar only shows with one of them. Empty = always shown. |
| **Players can draw circles**  | `playerMarkerCircles` | On / off |  | `true` | Group and private markers may have an area circle with optional strike lines. |
| **Largest player circle**  | `playerMarkerMaxRadius` | Number | 0 – 20000 m | `500` | Admins are not limited. 0 = no limit. |
| **Seeing teammates needs an item**  | `teammateRequiredItems` | List (one per line) |  | `(empty)` | Class names, one per line (for example a radio). Teammates only show on the map, minimap and in 3D with one of them. Empty = always. |

### List: Map legend

Rows shown in a legend box at the bottom right of the map.

List id: `mapLegend` · up to 30 legend row records · record type `AGMapLegendEntry`

| Field | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **Icon**  | `markerType` | Choice | Marker icons | `0` | Marker icon shown in the legend. |
| **Label** *required* | `label` | Text |  | `""` | What this icon means. |
| **Colour**  | `color` | Colour (RRGGBB) |  | `"FFFFFF"` | Icon tint. |


### List: Server markers

Markers every player sees: traders, danger areas, landmarks.

List id: `serverMarkers` · up to 200 marker records · record type `AGServerMarker`

| Field | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **Label** *required* | `label` | Text |  | `""` | Text shown next to the marker. |
| **Icon**  | `markerType` | Choice | Marker icons | `AGMarkerType.GENERIC` | Icon used on the map and in 3D. |
| **Position**  | `position` | Position (x y z) |  | `vector.Zero` | World position. Use "My position" while standing on the spot. |
| **Colour**  | `color` | Colour (RRGGBB) |  | `"FF0000"` | Marker colour. |
| **Visible on**  | `displayMode` | Choice | 0 = Map, minimap and 3D<br>1 = 3D only<br>2 = Map and minimap only<br>3 = Hidden from players | `AG_SVRMARKER_SHOW_ALL` | Where players can see this marker. |
| **Area circle radius**  | `circleRadius` | Number | 0 – 20000 m | `0` | Draws a circle around the marker. 0 draws no circle. |
| **Circle colour**  | `circleColor` | Colour (RRGGBB) |  | `""` | Leave empty to use the marker colour. |
| **Hatched circle**  | `drawStrikeLines` | On / off |  | `false` | Fill the circle with diagonal lines (good for danger areas). |
| **Hatch style**  | `strikeStyle` | Choice | 1 = Lines<br>2 = Cross-hatch | `2` | Single diagonal lines or a cross-hatch. |
| **Hatch colour**  | `strikeColor` | Colour (RRGGBB) |  | `""` | Leave empty to use the circle colour. |


### List: Marker icon styles

Default colour, size and visibility for every marker icon.

List id: `markerTypes` · up to 120 style records · record type `AGMarkerTypeConfig`

| Field | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **Icon**  | `markerType` | Choice | Marker icons | `AGMarkerType.GENERIC` | Which icon this style applies to. Each icon can have one style. |
| **Display name** *required* | `name` | Text |  | `"Generic"` | Name shown in marker pickers. |
| **Default colour**  | `color` | Colour (RRGGBB) |  | `"FFFFFF"` | Colour used when a player does not pick one. |
| **Icon size**  | `scale` | Number | 0.1 – 5 x | `1.0` | 1.0 is normal size. |
| **Show distance**  | `showRange` | On / off |  | `true` | Show the distance next to the 3D marker. |
| **On map**  | `showOnMap` | On / off |  | `true` | Draw on the full map. |
| **On minimap**  | `showOnMinimap` | On / off |  | `true` | Draw on the minimap. |
| **In 3D**  | `showIn3D` | On / off |  | `true` | Draw in the world. |
| **3D view distance**  | `max3DDistance` | Number | 0 – 20000 m | `0` | Hide the 3D marker beyond this distance. 0 uses the player's own setting. |


## HUD defaults

What new players see before they change their own settings.

Section id: `hud` · stored in `AGServerConfig`

| Setting | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **Compass**  | `defaultShowCompass` | On / off |  | `true` | Show the compass bar. |
| **Team list**  | `defaultShowPlayerlist` | On / off |  | `true` | Show the group member list. |
| **3D markers**  | `defaultShow3DMarkers` | On / off |  | `true` | Show markers in the world. |
| **Teammate names in 3D**  | `defaultShowPlayer3DName` | On / off |  | `true` | Show names above teammates. |
| **Teammate distance in 3D**  | `defaultShowPlayer3DDistance` | On / off |  | `true` | Show the distance to teammates. |
| **Teammate icon in 3D**  | `defaultShowPlayer3DIcon` | On / off |  | `true` | Show an icon above teammates. |
| **Name tags above players**  | `playerNameTagMode` | Choice | 0 = Everywhere<br>1 = Only inside safe zones<br>2 = Never | `0` | Where names float above other players. |
| **Icons above players**  | `playerNameIconMode` | Choice | 0 = Everywhere<br>1 = Only inside safe zones<br>2 = Never | `0` | Where player icons are shown. |
| **Group tags above players**  | `playerNameGroupTagMode` | Choice | 0 = Everywhere<br>1 = Only inside safe zones<br>2 = Never | `0` | Where group tags are shown. |
| **Teammate marker colour**  | `defaultPlayerMarkerColor` | Colour (RRGGBB) |  | `"00FFAA"` | Default colour for teammates. |
| **Compass colour**  | `defaultCompassColor` | Colour (RRGGBB) |  | `"FFFFFF"` | Default compass colour. |
| **Team list colour**  | `defaultPlayerlistColor` | Colour (RRGGBB) |  | `"FFFFFF"` | Default team list text colour. |

## Discord webhooks

Send group and chat events to Discord. Event-specific URLs fall back to the main URL when left empty. Saved URLs are never shown again.

Section id: `webhooks` · stored in `AGServerConfig`

| Setting | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **Send webhooks**  | `enableWebhooks` | On / off |  | `false` | Master switch for every webhook below. |
| **Log group events**  | `logGroupEvents` | On / off |  | `true` | Also write group events to the Advanced Groups log. |
| **Main webhook URL**  | `webhookUrl` | Secret (never shown back) |  | `""` | Used for every event without its own URL. |
| **Group created** *advanced* | `webhookUrlGroupCreated` | Secret (never shown back) |  | `""` |  |
| **Group disbanded** *advanced* | `webhookUrlGroupDisbanded` | Secret (never shown back) |  | `""` |  |
| **Member joined** *advanced* | `webhookUrlMemberJoined` | Secret (never shown back) |  | `""` |  |
| **Member left** *advanced* | `webhookUrlMemberLeft` | Secret (never shown back) |  | `""` |  |
| **Member kicked** *advanced* | `webhookUrlMemberKicked` | Secret (never shown back) |  | `""` |  |
| **Global chat** *advanced* | `webhookUrlChatGlobal` | Secret (never shown back) |  | `""` |  |
| **Vicinity chat** *advanced* | `webhookUrlChatVicinity` | Secret (never shown back) |  | `""` |  |
| **Group chat** *advanced* | `webhookUrlChatGroup` | Secret (never shown back) |  | `""` |  |
| **Subgroup chat** *advanced* | `webhookUrlChatSubgroup` | Secret (never shown back) |  | `""` |  |
| **Marker placed** *advanced* | `webhookUrlMarkerPlaced` | Secret (never shown back) |  | `""` |  |

## Server information

Links and pages on the Info tab of the group menu.

Section id: `info` · stored in `AGServerInfoConfig`

| Setting | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **Discord link**  | `discordLink` | Text |  |  | Invite link shown on the Info tab. |
| **Website link**  | `websiteLink` | Text |  |  | Shown on the Info tab. |
| **Donation link**  | `donateLink` | Text |  |  | Leave empty to hide the button. |

### List: Info pages

Rules and guides. Use new lines for paragraphs.

List id: `pages` · up to 30 page records · record type `AGServerInfoPage`

| Field | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **Title** *required* | `title` | Text |  |  | Tab title. |
| **Text**  | `content` | Long text |  |  | Page text. |


## Event markers

Automatically mark world events (heli crashes, convoys...) for every player.

Section id: `events` · stored in `AGEventMarkerConfig`

| Setting | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **Mark events**  | `enabled` | On / off |  | `false` | Turn automatic event markers on. |
| **Scan interval**  | `syncIntervalSeconds` | Number | 1 – 600 seconds | `15.0` | How often the server looks for event objects. |
| **Marker limit**  | `maxActiveMarkers` | Whole number | 0 – 1000 markers | `120` | Maximum event markers on the map at once. |

### List: Tracked events

Each entry marks every object of a class name.

List id: `entries` · up to 200 event records · record type `AGEventMarkerEntry`

| Field | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **Object class** *required* | `className` | Text |  | `""` | Exact class name of the event object, for example Wreck_Mi8_Crashed. |
| **Label** *required* | `label` | Text |  | `""` | Text on the marker. |
| **Icon**  | `markerType` | Choice | Marker icons | `AGMarkerType.STAR` | Marker icon. |
| **Colour**  | `color` | Colour (RRGGBB) |  | `"FFD700"` | Marker colour. |
| **Visible on**  | `displayMode` | Choice | 0 = Map, minimap and 3D<br>1 = 3D only<br>2 = Map and minimap only<br>3 = Hidden from players | `AG_SVRMARKER_SHOW_ALL` | Where players see the marker. |
| **Area circle radius**  | `circleRadius` | Number | 0 – 20000 m | `0` | 0 draws no circle. |
| **Circle colour**  | `circleColor` | Colour (RRGGBB) |  | `"FFD700"` |  |
| **Hatched circle**  | `drawStrikeLines` | On / off |  | `false` |  |
| **Hatch colour**  | `strikeColor` | Colour (RRGGBB) |  | `"FFD700"` |  |
| **Remove with the object**  | `removeWhenObjectDeleted` | On / off |  | `true` | Delete the marker when the event object despawns. |
| **Merge distance**  | `positionMergeDistance` | Number | 0 – 500 m | `8.0` | Objects closer than this share one marker. |


## Owners

Advanced Groups owner list. Owners have full Advanced Groups admin rights in game.

Section id: `owners` · stored in `AGServerConfig`

| Setting | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **Advanced Groups owners** *careful* | `adminIds` | List (one per line) |  | `(empty)` | SteamID64s, one per line. Separate from the Suite administrators on the Core page. |
| **Group storage folder** *advanced* *read only* | `storageDir` | Text |  | `"$profile:AdvancedGroups/groups/"` | Managed by Lemmy's Core storage. Shown for reference. |

{% endraw %}
