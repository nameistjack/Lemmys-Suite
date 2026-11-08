---
layout: page
title: Herosper Keycards Remastered
section: COMPANION MOD
permalink: /keycards/
---

# Herosper Keycards Remastered

A standalone remaster of the Workshop mod **Herosper Keycards** (`2886051760`): Herosper's doors, keycards and crates in one mod. It makes keycard doors work on DayZ 1.30 and turns every keycard door into a raid. It does not need Lemmy's Core, Advanced Groups or Advanced Banking.

<div class="video-embed">
  <iframe src="https://www.youtube-nocookie.com/embed/{{ site.links.video_keycards }}" title="Herosper Keycards Remastered" loading="lazy" allow="accelerometer; clipboard-write; encrypted-media; gyroscope; picture-in-picture; fullscreen" allowfullscreen></iframe>
</div>

<p class="page-links"><a class="button primary" href="{{ site.links.workshop_keycards }}" target="_blank" rel="noreferrer">Steam Workshop</a> <a class="button secondary" href="{{ site.links.discord }}" target="_blank" rel="noreferrer">Discord support</a></p>

Standalone: it already contains [Herosper Keycards]({{ site.links.workshop_herosper }}), which Herosper released for anyone to update and publish. Don't load the original alongside it.

The full guide — every editor field, the placement keys, files and troubleshooting — is in the [documentation]({{ site.baseurl }}/docs/herosper-keycards-remastered.html).

## What a raid looks like

1. A player swipes the right keycard and the door opens for its **auto close** time.
2. AI defenders spawn in waves around the door or at spawn points you placed — on the navigation mesh, so never inside walls, and on the floor you placed them on.
3. The **reward crate** appears once every defender is dead (or straight away, if you switch *crate after AI defeated* off). It is filled from the door's **loot table**.
4. If the door locks before the defenders are dead, the raid fails: defenders are removed and no crate appears.
5. Server-wide messages, Discord posts and `KCR_Raids.log` record the unlock, each wave, the result and the looting. Doors can have a **name** that is used in all of them.

## Colour doors and keycards

Besides Herosper's T1–T7, Remastered adds **Yellow, Blue, Orange, White, Pink and Teal**: each as a sliding door, a vault and a matching keycard that opens both. Each has its own card and door texture; swap in your own by replacing the `.paa` files. Details in the [documentation]({{ site.baseurl }}/docs/herosper-keycards-remastered.html#doors-and-keycards).

## The raid editor

Press **Numpad 6** in game. Only admins in `$profile:KeyCardSystem/EditorAdmins.json` get an answer.

- **Keycards** — by default each Herosper card opens its own tier (ASW1 → T1 … ASW7 → T7). Per door you can list any item classes instead (cards from other mods, keys, custom items) and choose whether the card is used up.
- **Doors** — door class, position, rotation, scale, auto close, name; crate class, position and loot table; AI classes (search and add), waves, timing, spawn points and cooldown. Saving spawns or moves the door live.
- **Loot tables** — search every item, add it, set min and max quantity and chance per entry.
- **Settings** — Discord webhook, shared with KeyCardSystem's own `config.json`.

Placing objects: aim with the crosshair, **arrow keys** fine-move (Shift faster), **L** back to the crosshair, **Q / E** rotate, **Page Up / Down** height, **Numpad − / +** scale, **left click** place, **Backspace** cancel. Spawn points are shown as barrels.

## Install

```text
-mod=@CF;@HerosperKeycards_Remastered
```

Load it on server and client. Remove `@HerosperKeycards` and any older `@HerosperKeycards_130_Fix`: this mod already contains them, and existing door configs keep working. Start once, then add your SteamID64 to `EditorAdmins.json`.

## Credits

Original mod, models, textures and keycard system by **Herosper**, released for anyone to update and publish on the Workshop. Thank you!
