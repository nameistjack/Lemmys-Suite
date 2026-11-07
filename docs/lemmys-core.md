---
layout: page
title: "Lemmy's Core"
section: DOCUMENTATION
permalink: /docs/lemmys-core.html
---
{% raw %}
# Lemmy's Core

Server-only hub of the suite and the **server-side dependency of Advanced Groups and Advanced Banking**. Load it with `-serverMod`; players never download it. Settings: [Lemmy's Core settings](settings/lemmys-core.html). Only **suite administrators** can open its page in the Control Room.

## What it does

- **Module registry.** Each module registers itself when its PBO loads. *Modules* switches decide which ones start with the server (stored in `General\modules.json`, applied after a restart).
- **Profile folder.** Creates and owns `$profile:LemmysSuite\` and migrates files from older versions once (see [Files and folders](files-and-folders.html)).
- **Control Room server.** Describes each module's settings, sends them to admins in chunks, validates every change again on the server, writes history snapshots, saves through each module's own loader, and hot-reloads the module.
- **Access control.** Suite administrators and staff editors (per-module), checked on every request.
- **Logging.** One log system for every module with levels (Trace → Security), rotation, optional copy into the server RPT and an in-memory live log.

## Access

| Role | Where | Can |
|---|---|---|
| Suite administrator | *Access → Suite administrators* (and `General\suite.json`) | Everything, including this page |
| Staff editor | *Access → Staff editors* | Only the modules listed (`AdvancedGroups`, `SpawnSystem`, `AdvancedBanking`, or `*` for all but Core) |

Keep at least one suite administrator, or nobody can open the Control Room.

## Logging levels

| Level | Writes |
|---|---|
| 0 Trace | Everything — only while chasing a problem |
| 1 Info | Normal operation (recommended) |
| 2 Warnings and above | |
| 3 Errors and above | |
| 4 Audit and security | Admin actions and refusals only |
| 5 Security only | Refused access only |

{% endraw %}
