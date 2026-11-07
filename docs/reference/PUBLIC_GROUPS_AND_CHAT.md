---
layout: page
title: "Public service groups and Global chat"
section: DOCUMENTATION
permalink: /docs/reference/PUBLIC_GROUPS_AND_CHAT.html
---
{% raw %}
# Public service groups and Global chat

Public service groups are a server-owned directory, independent of private groups. A player can remain in a private group and be assigned to Taxi, Medic, Helper, Admins, or another service at the same time. The initial four services are examples; they have no assigned members until an owner adds Steam64 IDs.

Open **Services** in the Advanced Groups menu to see each service and its currently online members. The directory refreshes while a player is viewing it; **Refresh** requests it immediately. Only Steam64 IDs in `adminIds` can create, edit, delete, or assign a service. The server validates every change and saves it to `server_config.json` under `publicGroups`. Staff roles do not grant access to this directory.

In **Config Studio → Chat**, create a tag by entering a Steam64 ID, tag text, and hex color, then selecting **Add tag** and **Save Chat**. Select an existing entry to update or delete it. Each Steam64 ID may have one chat tag. In **Group Tiers**, the separate player-name color has a live preview; the tier's badge color remains independent.

In Global chat, type `@Full Player Name` to mention an online player by their exact current display name. A match notifies that player. The most recently mentioned player can answer in Global chat with `/reply message`; this posts a public `@Full Player Name message`, not a private message. A reply target is held in server memory and disappears on recipient disconnect or server restart. There is no click-to-reply widget yet, and avatars and emoji rendering are not part of this version.

{% endraw %}
