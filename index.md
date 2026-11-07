---
layout: home
title: Overview
---

Lemmy's Suite is three DayZ mods that share one profile folder and one in-game admin console, the **Control Room**. Every config they use can be changed in game, while the server runs.

<div class="mod-grid">
  <a href="{{ site.baseurl }}/core/"><b>Lemmy's Core</b><span>Server-only. Profile folder, migration from the old folders, module switches and the Control Room console.</span></a>
  <a href="{{ site.baseurl }}/groups/"><b>Advanced Groups</b><span>Groups, ranks, map and minimap, markers, chat, safe and no-build zones, territories, spawn selection and the group manager.</span></a>
  <a href="{{ site.baseurl }}/banking/"><b>Advanced Banking</b><span>Personal and group accounts, ATMs, transfers with fees and limits, paychecks, interest, VIP tiers and ATM robberies.</span></a>
  <a href="{{ site.baseurl }}/keycards/"><b>Herosper Keycards Remastered</b><span>Companion mod. Keycard door raids: reward crates, loot tables, AI defence waves and an in-game raid editor.</span></a>
</div>

## Get the mods

<div class="workshop-row">
  <a href="{{ site.links.workshop_core }}" target="_blank" rel="noreferrer"><small>STEAM WORKSHOP</small><b>Lemmy's Core</b><span>Server only</span></a>
  <a href="{{ site.links.workshop_groups }}" target="_blank" rel="noreferrer"><small>STEAM WORKSHOP</small><b>Advanced Groups</b><span>Server + client</span></a>
  <a href="{{ site.links.workshop_banking }}" target="_blank" rel="noreferrer"><small>STEAM WORKSHOP</small><b>Advanced Banking</b><span>Server + client</span></a>
  <a href="{{ site.links.workshop_keycards }}" target="_blank" rel="noreferrer"><small>STEAM WORKSHOP</small><b>Herosper Keycards Remastered</b><span>Companion mod</span></a>
  <a href="{{ site.links.discord }}" target="_blank" rel="noreferrer"><small>SUPPORT</small><b>Discord</b><span>Help, bug reports, updates</span></a>
</div>

## Walkthrough

<div class="video-embed">
  <iframe src="https://www.youtube-nocookie.com/embed/{{ site.links.video_suite }}" title="Lemmy's Suite walkthrough" loading="lazy" allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture; fullscreen" allowfullscreen></iframe>
</div>

## How the pieces fit

- **Community Framework is required.** Banking talks to the server only through CF named RPCs. Groups and Core also list it in `requiredAddons`.
- **Lemmy's Core is the server-side dependency of Groups and Banking.** Load it with `-serverMod`; players never download it. It owns `$profile:LemmysSuite/`, moves files from the old `$profile:AdvancedGroups/` and `$profile:Advanced_Banking/` folders once, and runs the Control Room, version history, staff access and logging.
- **Banking does not need Groups.** If Groups is loaded, group accounts, rank permissions, group opening costs and the robbery map marker switch on. Without Groups, personal banking works as before.
- **Nothing depends on Trader, Expansion, VPP or another map or group mod.** Banking can import balances and currency classes from an existing TraderPlus bank, but TraderPlus does not need to be installed.

## Where to start

1. [Setup]({{ site.baseurl }}/setup/) covers the install order, keys, launch parameters and the files each mod creates.
2. The pages for each mod list every setting with its default, and what to check after a change.
3. The [documentation]({{ site.baseurl }}/docs/) has the player and admin guides, the Control Room, every setting, the layout reference and troubleshooting.
4. [API]({{ site.baseurl }}/api/) is for other mod authors: the stable server-side calls, with examples.
5. [Changes]({{ site.baseurl }}/changelog/) lists what changed in each build. Untested entries say so.

## What this site is not

It doesn't include game source, server configs, packed PBOs or keys. For bug reports, include the server RPT, the `LemmysSuite/Logs` folder and which build you run. "It's broken" is not enough to reproduce anything.
