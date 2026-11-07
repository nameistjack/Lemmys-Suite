---
layout: page
title: "Lemmy's Suite — Documentation"
section: DOCUMENTATION
permalink: /docs/index.html
---
{% raw %}
# Lemmy's Suite — Documentation

Lemmy's Suite is a modular set of DayZ server mods built around one in-game admin tool, the **Control Room**. Server owners install only the modules they want; every setting of every module is edited live in game, without editing JSON files or restarting the server.

| Mod | Runs on | What it does |
|---|---|---|
| **Lemmy's Core** | Server only | The hub. It finds the installed modules, owns the shared profile folder, runs the Control Room server side (settings, validation, live apply, version history, audit log) and controls who may edit what. |
| **Advanced Groups** | Server + client | Groups and squads, a full chat replacement, map/minimap/3D markers, HUD, compass, territories, safe/no-build/polygon zones, spawn selection, mailbox, public service groups — and the Control Room window players see. |
| **Advanced Banking** | Server + client | Bank accounts at ATMs: personal and group accounts, transfers with fees, paychecks, interest, activity pay, ATM robbery with PvE defence waves, cash pools, VIP tiers, money drops and a TraderPlus import. |

**Lemmy's Core is the server-side dependency of Advanced Groups and Advanced Banking.** Load it on the server with `-serverMod`; players never download it. The Control Room, the shared profile folder, version history, staff access and logging all come from it.

## Contents

**Getting started**
- [Installation](getting-started.html) — requirements, load order, keys, first administrator
- [Files and folders](files-and-folders.html) — everything the suite writes under the server profile

**Using the suite**
- [Control Room](control-room.html) — the admin console: modules, sections, lists, map picker, world placement, colour picker, review, apply, history
- [Advanced Groups](advanced-groups.html) — player and admin guide
- [Spawn Selection](spawn-selection.html)
- [Advanced Banking](advanced-banking.html) — player and admin guide
- [Lemmy's Core](lemmys-core.html) — access, staff editors, logging, modules
- [Keybinds and chat commands](keybinds-and-commands.html)

**Companion mod**
- [Herosper Keycards Remastered](herosper-keycards-remastered.html) — keycard door raids: reward crates, loot tables, AI defence waves and an in-game raid editor

**Reference**
- Settings, every field with type, range, default and description:
  [Advanced Groups](settings/advanced-groups.html) · [Advanced Banking](settings/advanced-banking.html) · [Spawn Selection](settings/spawn-selection.html) · [Lemmy's Core](settings/lemmys-core.html)
- [Layout reference](layouts/index.html) — every `.layout` file with its full widget tree and the script that loads it
- [Design file](design.html) — the Figma mock-ups of every screen
- [Architecture](architecture.html) — how the pieces talk to each other
- [Developer API](developer-api.html) — Advanced Groups public API and adding a module to the Control Room
- [Troubleshooting](troubleshooting.html)

## Version

This documentation describes **0.5.0-beta** of all three mods, updated 7 November 2026. What changed is listed in the site's *Changes* page.

{% endraw %}
