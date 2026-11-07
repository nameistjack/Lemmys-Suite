---
layout: page
title: "Lemmy's Core settings"
section: DOCUMENTATION
permalink: /docs/settings/lemmys-core.html
---
{% raw %}
# Lemmy's Core settings

Every setting the Control Room shows for this module, in the order it shows them. Values are applied live when you press **APPLY LIVE** unless the setting is tagged *restart*.

**Tags:** *careful* — asks for a note and is highlighted; *restart* — saved now, used after the next restart; *advanced* — hidden until SHOW ADVANCED; *read only* — shown for reference; *required* — cannot be empty.


## Access

Who can open the Control Room and what they may change.

Section id: `access` · stored in `LMSCoreSettings`

| Setting | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **Suite administrators** *careful* | `adminSteamIds` | List (one per line) |  | `(empty)` | SteamID64s with full access to every module and to this page. One per line. Keep at least one, or nobody can open the Control Room. |

### List: Staff editors

Staff who may edit only the modules listed for them. They never see this Core page.

List id: `editors` · up to 100 editor records · record type `LMSModuleEditor`

| Field | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **SteamID64** *required* | `steamId` | SteamID64 |  |  | The staff member's 17 digit SteamID64. |
| **Name / note**  | `note` | Text |  |  | Who this is, so other admins recognise the entry. |
| **Allowed modules**  | `modules` | List (one per line) |  | `(empty)` | Module ids, one per line: AdvancedGroups, SpawnSystem, AdvancedBanking - or * for all modules except Core. |


## Logging

How much the suite writes to its log files under LemmysSuite/Logs.

Section id: `logging` · stored in `LMSCoreSettings`

| Setting | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **Log detail**  | `minimumLogLevel` | Choice | 0 = Trace - everything<br>1 = Info - normal<br>2 = Warnings and above<br>3 = Errors and above<br>4 = Audit and security only<br>5 = Security only | `LMSLogLevel.INFO` | Lower levels write more. Info is right for a live server; use Trace only while chasing a problem. |
| **Log files to keep**  | `retainedLogFiles` | Whole number | 1 – 365 files | `14` | How many rotated log files are kept before the oldest is removed. |
| **Copy suite logs to the server RPT**  | `mirrorLogsToRPT` | On / off |  | `true` | Also print suite log lines into the normal server RPT file. |
| **Live admin log**  | `enableLiveAdminLog` | On / off |  | `true` | Keep recent log lines in memory so admins can read them in game. |

## Modules

Turn whole modules on or off. Changes here apply after the next server restart.

Section id: `modules` · stored in `LMSCoreSettings`

| Setting | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **descriptor.displayName** *restart* | `"enabled_" + descriptor.moduleId` | On / off |  |  | Start " + descriptor.displayName + " with the server. |

{% endraw %}
