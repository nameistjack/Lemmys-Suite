---
layout: page
title: "Installation"
section: DOCUMENTATION
permalink: /docs/getting-started.html
---
{% raw %}
# Installation

## Requirements

- DayZ server and client **1.30** or later.
- **Community Framework** (`@CF`) on server and client. All three mods use its RPC manager.
- A server started with `-profiles=<folder>`. The suite writes everything under that folder (see [Files and folders](files-and-folders.html)). Without it `$profile:` does not resolve and nothing can be saved.

## What goes where

| Mod | Folder / file | Server | Client | Notes |
|---|---|---|---|---|
| Lemmy's Core | `@Lemmys Core\addons\Lemmys_Core.pbo` | `-serverMod` (or the server `addons\` folder) | — | **Required on the server** by Advanced Groups and Advanced Banking. Server only: players never download it. |
| Advanced Groups | `@Advanced Groups by Lemmy Maverick\addons\AdvancedGroups.pbo` | `-mod` | `-mod` | Contains the Control Room window and the Spawn Selection module. |
| Advanced Banking | `@AdvancedBanking\addons\Advanced_Banking.pbo` | `-mod` | `-mod` | Contains the ATM model, the admin tablet and its own copy of the Control Room window (used only when Advanced Groups is absent). |

Sign every client PBO with your server key and put the `.bikey` in the server `keys\` folder. Re-sign after every repack: a stale `.bisign` makes clients fail signature checks.

## Load order

```
Server:  -mod=@CF;@Advanced Groups by Lemmy Maverick;@AdvancedBanking
         -serverMod=@Lemmys Core
Client:  -mod=@CF;@Advanced Groups by Lemmy Maverick;@AdvancedBanking
```

Use the folder names your mods actually have. `@CF` must load first. Never put Lemmy's Core on the client `-mod` line. Advanced Groups and Advanced Banking can be in either order. When both are loaded, Banking detects Advanced Groups (`#ifdef AdvancedGroups`) and uses its groups for group accounts, its map markers for robberies and its Control Room window.

## Mission template

`serverDZ.cfg` must point at a valid mission, for example:

```
class Missions { class DayZ { template = "dayzOffline.chernarusplus"; }; };
```

A wrong template leaves clients stuck on the loading screen. Some server panels rewrite `serverDZ.cfg` on start, so change it in the panel, not only in the file.

## First start

1. Start the server once. Lemmy's Core creates `$profile:LemmysSuite\` with `General`, `Configs`, `Data`, `Logs` and `LegacyBackups`.
2. Existing Advanced Groups and Advanced Banking files from older versions are copied into the new folders automatically. The originals are kept in `LegacyBackups\migration_<date>\` and the migration is recorded in `General\migration_state.json`, so it runs only once.
3. Stop the server and add your SteamID64 to `adminSteamIds` in `General\suite.json`:

   ```json
   { "adminSteamIds": ["7656119XXXXXXXXXX"] }
   ```

4. Start the server, join, and open the Control Room (see [Control Room](control-room.html#opening-it)). From now on everything — including more administrators — is set in game.

## Updating

1. Stop the server.
2. Replace the PBOs (and re-sign the client ones).
3. Start the server. Config files are upgraded in place when a module raises its config version; the previous file is backed up next to it as `*_backup_<date>.json`.

## Uninstalling a module

Turn it off in **Control Room → Lemmy's Core → Modules** and restart, or remove its PBO. Its files under `LemmysSuite\` are left untouched.

{% endraw %}
