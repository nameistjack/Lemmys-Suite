---
layout: page
title: Lemmy's Core
section: SERVER MOD
permalink: /core/
---

# Lemmy's Core

Core is a small server-only PBO and the **server-side dependency of Advanced Groups and Advanced Banking**. Load it with `-serverMod`; players never download it. It does four jobs:

1. owns the `$profile:LemmysSuite` folder,
2. copies old Advanced Groups and Advanced Banking files into it once,
3. turns modules on and off,
4. runs the **Control Room**, the in-game config console for every module.

It requires Community Framework (`JM_CF_Scripts`) and nothing else.

## Folder layout

Core creates these folders on first start:

```text
$profile:LemmysSuite/
  General/
    suite.json            suite admins, staff editors, migration result
    modules.json          on/off switch per module
    staff_access.json
    migration_state.json  per-file migration journal
  Configs/
    AdvancedGroups/       server_config.json, server_info.json, event_markers.json
    AdvancedBanking/      config.json
    SpawnSystem/          spawn_config.json
  Data/
    AdvancedGroups/       groups/, private_markers/, moderation.json, territories.json
    AdvancedBanking/      accounts/personal/, accounts/groups/
    SpawnSystem/          zone_cooldowns.json
  Logs/                   one folder per module
  LegacyBackups/          timestamped copy of the old folders after migration
```

Don't edit these files while the server is running. Use the Control Room, or stop the server first.

## Moving from the old folders

You don't need to do anything. On the first boot with Core loaded:

- every known file from `$profile:AdvancedGroups/` and `$profile:Advanced_Banking/` is **copied**, never moved or deleted;
- each module then loads its copy with its own config class and validates it;
- only after validation does the module switch to the new path;
- once everything checks out, the old trees are archived under `LegacyBackups/` and `General/suite.json` gets `"profileState": "MIGRATED_SUCCESSFULLY"`.

If a module rejects a file, `migration_state.json` shows `VALIDATION_FAILED` for that file. The module keeps using the legacy file and the Core log says why. Group and account files are migrated one by one, so a single broken account file doesn't block the rest.

DayZ scripts can't rename or delete folders, so the old folders stay on disk. After migration they are never read again, and you can delete them yourself once you are happy.

## Turning modules off

`General/modules.json` has one entry per module: `AdvancedGroups`, `SpawnSystem` and `AdvancedBanking`. Set `enabled` to `false` and restart to keep the PBO loaded but not start the module. Spawn selection lives in the Advanced Groups PBO but has its own switch.

## Control Room

Admins open it with **U** (the Advanced Groups admin key) or **Numpad 9** (the Banking admin key). Both keys can be rebound in DayZ controls. The full guide — sections, lists, map picker, world placement, colour picker, review and history — is in the [Control Room documentation]({{ site.baseurl }}/docs/control-room.html).

Who gets in:

- **Suite administrators** (`adminSteamIds` in `suite.json`) can edit everything, including the Core page. On the first start the Groups `adminIds` list is imported, so existing admins keep access.
- **Staff editors** are a SteamID plus the module ids they may edit, or `*` for every module except Core.

How editing works:

- Changes are a **draft** until you press **APPLY LIVE** (or Ctrl+S). Drafts survive closing the console but not disconnecting.
- Ctrl+Z / Ctrl+Y undo and redo, including deleted list entries. Ctrl+F searches every label and description in the module.
- Settings marked **CAREFUL**, such as server-wide PvE or admin lists, always open the review screen and need a short note.
- Settings marked **RESTART** are saved immediately but only take effect after the next restart.
- If two admins edit at the same time, the second apply is refused until that admin's page is refreshed. Their pending edits are kept and conflicts are highlighted.
- Every apply keeps the replaced files under `LemmysSuite/History/<Module>/`, with the last 25 per module. **RESTORE** brings an old version back live, and a restore can itself be undone.
- Webhook URLs are never sent back to a client. The field stays empty: type a new URL to replace it, or press CLEAR to remove it.

Every apply goes to the audit log with the admin, the fields changed and the note.

## Adding your own module

The Control Room builds its pages from a description you write. The values are read and written straight into your config class, so you don't write any UI code. The full walkthrough with a complete provider example is on the [API page]({{ site.baseurl }}/api/#control-room-providers).

## Limits we hit and how we handled them

| Engine limit | What Core does |
|---|---|
| RPC strings and packets have a size limit | Config documents are sent in 480-byte UTF-8-safe pieces, 12 per RPC, checked by length and hash, with a 384 KB ceiling and a 30 s timeout |
| No general reflection | Each field is read and written through `EnScript.GetClassVar` / `SetClassVar` with a temporary of the exact type. Arrays and nested objects go through provider code |
| Clients can't see Core's classes | The wire format is duplicated client-side and matched by field name |
| Cached schemas can go stale after a restart | Revisions start from a random number on each boot and schemas are cached by hash |
