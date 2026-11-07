---
layout: page
title: "Files and folders"
section: DOCUMENTATION
permalink: /docs/files-and-folders.html
---
{% raw %}
# Files and folders

Everything lives under `$profile:LemmysSuite\` (the folder given with `-profiles=` on the server command line). All JSON files are written through a temporary file and read back before they replace the original, so a crash during a save never leaves a half-written file.

```
LemmysSuite\
├─ General\
│  ├─ suite.json              Core settings: administrators, staff editors, logging
│  ├─ modules.json            Which modules start with the server
│  ├─ staff_access.json       Advanced Groups staff grants (legacy, still read)
│  └─ migration_state.json    Journal of the one-time import from older versions
├─ Configs\
│  ├─ AdvancedGroups\
│  │  ├─ server_config.json   Groups, chat, protection, zones, territories, map, HUD, webhooks, owners
│  │  ├─ server_info.json     Info tab: links and pages
│  │  └─ event_markers.json   Tracked world events (heli crashes, convoys...)
│  ├─ AdvancedBanking\        Banking configuration (accounts, limits, fees, ATMs, robbery, VIP...)
│  └─ SpawnSystem\
│     └─ spawn_config.json    Spawn menu and spawn points
├─ Data\
│  ├─ AdvancedGroups\
│  │  ├─ groups\              One file per group
│  │  ├─ groups_index.json
│  │  ├─ private_markers\     One file per player
│  │  └─ event_runtime_markers.json
│  ├─ AdvancedBanking\
│  │  └─ accounts\
│  │     ├─ personal\         One file per player account
│  │     └─ groups\           One file per group account
│  └─ SpawnSystem\
│     └─ zone_cooldowns.json
├─ History\
│  ├─ <Module>\index.json     List of saved versions
│  └─ <Module>\<date>_<rev>__<file>.json   Copy of every config file before each Control Room apply
├─ Logs\
│  ├─ suite.log, core.log
│  ├─ AdvancedGroups\current.log, chat.log
│  ├─ AdvancedBanking\
│  └─ SpawnSystem\current.log
└─ LegacyBackups\
   └─ migration_<date>\       Untouched copies of the files found before the first migration
```

## Which files can I edit by hand?

You don't need to: every setting in `Configs\` is editable in the Control Room. If you do edit by hand, stop the server first. Files in `Data\` are runtime data (groups, balances, markers); edit them only with the server stopped and a backup made.

## History and restore

Before every apply the Control Room copies the module's config files into `History\<Module>\`. **Version history** in the Control Room lists these copies and can restore any of them live. Restoring is itself recorded, so it can be undone the same way.

## Logs

| File | Contents |
|---|---|
| `Logs\suite.log` | Every suite message, all modules |
| `Logs\core.log` | Control Room: hellos, catalog, applies, list rebuilds, security refusals |
| `Logs\AdvancedGroups\current.log` | Group events, config reloads, zone and marker service |
| `Logs\AdvancedGroups\chat.log` | Chat (all channels) |
| `Logs\AdvancedBanking\` | Transactions and admin actions (audit) |

How much is written is set in **Lemmy's Core → Logging**.

{% endraw %}
