---
layout: page
title: "Spawn Selection settings"
section: DOCUMENTATION
permalink: /docs/settings/spawn-selection.html
---
{% raw %}
# Spawn Selection settings

Every setting the Control Room shows for this module, in the order it shows them. Values are applied live when you press **APPLY LIVE** unless the setting is tagged *restart*.

**Tags:** *careful* — asks for a note and is highlighted; *restart* — saved now, used after the next restart; *advanced* — hidden until SHOW ADVANCED; *read only* — shown for reference; *required* — cannot be empty.


## Spawn menu

When fresh characters get the spawn selection screen.

Section id: `general` · stored in `AGSpawnConfig`

| Setting | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **Spawn selection**  | `enabled` | On / off |  | `false` | Fresh characters choose where to spawn. |
| **Must choose**  | `forceSelection` | On / off |  | `true` | Players cannot close the menu without picking a point. |
| **Offer random spawn**  | `allowRandom` | On / off |  | `true` | Adds a "random" button that uses the normal game spawns. |
| **Random ignores cooldowns**  | `randomIgnoresCooldowns` | On / off |  | `true` | The random button stays usable while every point is on cooldown. |

### List: Spawn points

Each point is a named area on the map. Players spawn at one of its exact positions, or anywhere within the random radius when it has none.

List id: `points` · up to 100 spawn point records · record type `AGSpawnPoint`

| Field | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **Point id** *required* | `id` | Text |  | `""` | Short unique id, used for cooldown tracking. Changing it resets cooldowns for this point. |
| **Name** *required* | `name` | Text |  | `""` | Shown to players in the spawn menu. |
| **Available**  | `enabled` | On / off |  | `true` | Turn a point off without deleting it. |
| **Map position**  | `center` | Position (x y z) |  | `vector.Zero` | Centre of the area, also where the point is drawn on the spawn map. |
| **Random radius**  | `randomRadius` | Number | 0 – 5000 m | `100.0` | Used when the point has no exact positions below. |
| **Cooldown per player**  | `cooldownSeconds` | Whole number | 0 – 86400 seconds | `0` | How long a player waits before using this point again. 0 = no cooldown. |
| **Exact positions**  | `positions` | Positions (one per line) |  | `(empty)` | Optional. One X Y Z per line; a random one is picked each time. |


{% endraw %}
