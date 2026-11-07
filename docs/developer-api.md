---
layout: page
title: "Developer API"
section: DOCUMENTATION
permalink: /docs/developer-api.html
---
{% raw %}
# Developer API

## Advanced Groups public API

`AGPublicAPI` is a stable, server-side facade for other mods. Guard calls with `#ifdef AdvancedGroups` and check `AGPublicAPI.IsReady()` first.

| Method | Purpose |
|---|---|
| `GetAPIVersion()`, `SupportsAPIVersion(int)` | API version checks (current: 4) |
| `IsReady()` | Server manager initialised |
| `GetGroupForPlayer(steamId)`, `GetGroupById(groupId)`, `IsPlayerInGroup(steamId)` | Read-only group snapshots |
| `SendServerMessage(message, recipient = null)` | Server channel message to one player or everyone |
| `SendGlobalMessage(senderName, message, recipient = null)` | Global channel message |
| `SendGroupMessage(groupId, senderName, message)` | Group channel message |
| `PlaceGroupMarker(player, label, markerType, pos, ...)`, `PlacePrivateMarker(...)` | Markers for a player's group / private set; optional circle, colour, hatch |
| `IsSafeZone(pos)`, `IsNoBuildZone(pos)` | Zone tests |
| `GetTerritoryOwnerAt(pos, out groupId)` | Territory owner (flag claims and admin territory zones) |
| `CanBuildAt(player, pos)` | Same rules the build actions use |
| `PlaceAdminServerMarker(admin, ...)`, `PlaceServerMarker(label, markerType, pos, hexColor, ...)` | Server markers |
| `PlaceEventMarker(ownerId, ownerName, label, ...)`, `RemoveEventMarkers(ownerId, label)`, `FindEventMarker(ownerId, label)` | Temporary event markers owned by your mod |
| `SetGroupCategory(admin, groupId, categoryName)` | Put a group in a tier |
| `SetGroupColor(leaderOrOfficer, hexColor)` | Group colour |

Advanced Banking uses this API for group accounts, robbery map markers and police groups.

## Adding a module to the Control Room

A module becomes editable by registering a provider with Lemmy's Core. Subclass `LMSConfigProvider` (server side, `5_Mission`):

| Override | What to return / do |
|---|---|
| `ModuleId()`, `Title()`, `Summary()`, `Icon()`, `SortOrder()` | Catalog card |
| `IsAvailable()` | Usually `LMSModuleRegistry.IsEnabled("<id>")` |
| `Describe(LMSSchemaBuilder s)` | The settings: `Section`, `Toggle`, `Int`, `Float`, `Text`, `LongText`, `Secret`, `Color`, `SteamId`, `Position`, `Positions`, `Words`, `Choice`, `ChoiceList`, `Collection … EndCollection`, `RowText`, `.Flags(...)` |
| `Load(out error)` | Read your config through your own loader |
| `Target(sectionId)` / `DefaultTarget(sectionId)` | Object holding a section's values / a fresh default instance |
| `ItemCount`, `ItemAt`, `NewItem`, `ClearItems`, `AppendItem` | List access (`NewItem` must return through `Made(...)`) |
| `ReadCustom` / `WriteCustom` | Values that are not plain members (arrays, nested objects) |
| `Validate(LMSValidation)` | Cross-field rules; fail with `"collection#row.field"` keys |
| `Persist(out error)` | Save and verify |
| `Activate(LMSApplyContext)` | Hot-reload |
| `ConfigFiles(paths)` | Files to snapshot into history |

Plain members are read and written by name (`LMSReflect`), so field keys must match member names. Record lists are rebuilt from fresh objects on every apply; plain members not shown in the schema (ids, string lists) are carried over automatically.

### Field types and the console

| Builder | Console control |
|---|---|
| `Toggle` | ON/OFF |
| `Int`, `Float` | edit box with range and unit |
| `Text`, `SteamId`, `Secret` | edit box (secrets are never sent back) |
| `LongText`, `Words`, `Positions` | multi-line box; `Positions` gets ADD ON MAP, class-name lists get ADD CLASS |
| `Color` | hex box, swatch, colour picker |
| `Choice`, `ChoiceList` | choice list |
| `Position` | PICK ON MAP — or PLACE IN WORLD when the record also has a rotation field |
| Collection with float keys `x` and `z` | PICK ON MAP on both; `radius` / `circleRadius` draws circles; a `Positions` field draws polygons |

{% endraw %}
