---
layout: page
title: "Advanced Groups chat integration"
section: DOCUMENTATION
permalink: /docs/reference/CHAT_API.html
---
{% raw %}
# Advanced Groups chat integration

Advanced Groups provides a server-originated `[Server]` channel. Clients cannot select or submit this channel; the server rejects it in the player-chat RPC. The channel is shown by the Advanced Groups chat HUD independently of the player's Global/Group/Vicinity filters.

Advanced Groups' own personal feedback and group notifications also use this channel. The legacy notification RPC remains receive-only compatibility and is displayed in chat if another producer sends it.

## Server announcements

In a mod's `5_Mission` server script:

```c
if (AGPublicAPI.SupportsAPIVersion(3)) {
	AGPublicAPI.SendServerMessage("Restart in 10 minutes.");
	AGPublicAPI.SendServerMessage("Your event begins now.", targetPlayer);
}
```

The optional `PlayerBase` targets one online player. Without it, the message goes to all connected players. The API returns `false` if called client-side, with an empty message, or with an invalid target. Messages are normalized to one line and limited to 256 characters. No client RPC is exposed for sending `[Server]` messages.

Other server-only helpers are `AGPublicAPI.SendGlobalMessage(senderName, message, optionalTargetPlayer)` and `AGPublicAPI.SendGroupMessage(groupId, senderName, message)`. These are for trusted mod scripts, not untrusted client input. Group delivery uses Advanced Groups' current online roster. API version 3 adds these methods; version-2 marker integrations remain compatible.

## Player-message hook

Another mod can extend the server-side player-chat pipeline without replacing the Advanced Groups RPC:

```c
modded class AGChatHandler {
	override bool BeforePlayerMessage(PlayerIdentity sender, int channel, inout string message) {
		if (!super.BeforePlayerMessage(sender, channel, message)) return false;
		// Inspect, change, or consume a command here.
		return true;
	}

	override void AfterPlayerMessage(PlayerIdentity sender, int channel, string message) {
		super.AfterPlayerMessage(sender, channel, message);
		// This receives the filtered text after it has been relayed.
	}
}
```

`BeforePlayerMessage` runs after identity/channel/group and mute checks. Returning `false` consumes the message. Advanced Groups normalizes and length-limits modified text, then applies its bad-word filter. Player-originated messages remain restricted to Global, Group, Subgroup, and Vicinity. Server messages are not fed back through these player hooks.

## Join/leave messages

`server_config.json` has `announcePlayerJoin` and `announcePlayerLeave` (both default `true`). They send one `[Server]` line per connection/disconnection and do not rely on group membership. Existing group online/offline notices are separate messages, also delivered via `[Server]`. Existing configs migrate to version 12 with both announcements enabled; server owners can set either field to `false` and reload the config to disable it.

{% endraw %}
