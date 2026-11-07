---
layout: page
title: "Spawn Selection"
section: DOCUMENTATION
permalink: /docs/spawn-selection.html
---
{% raw %}
# Spawn Selection

Ships inside the Advanced Groups PBO and shows in the Control Room as its own module, **Spawn Selection** (`SpawnSystem`). Settings: [Spawn Selection settings](settings/spawn-selection.html). Screen: [`ag_spawn_menu`](layouts/advanced-groups/hud/ag_spawn_menu.html).

## For players

When a fresh character spawns and the feature is on, a map opens with the allowed spawn points. Each point shows whether it is on cooldown. Pick one, or press **Random** for a normal game spawn (if offered). If the server forces a choice, the menu cannot be closed without picking.

## For admins

1. Control Room → **Spawn Selection** → *Spawn menu*: turn **Spawn selection** on and choose whether players must choose and whether a random spawn is offered.
2. *Spawn points* → **+ ADD SPAWN POINT**. The map picker opens on the new point: click where its *Map position* (the marker players see) should be.
3. Either set a **Random radius** around that position, or press **ADD ON MAP** on *Exact positions* and click each spot players may appear at — every click adds one position.
4. Set the point's id (used for cooldowns), name, whether it is available and the **Cooldown per player**, then **APPLY LIVE**.

Cooldowns are stored in `Data\SpawnSystem\zone_cooldowns.json` and survive restarts. Changing a point's id resets its cooldown.

{% endraw %}
