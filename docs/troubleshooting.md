---
layout: page
title: "Troubleshooting"
section: DOCUMENTATION
permalink: /docs/troubleshooting.html
---
{% raw %}
# Troubleshooting

| Problem | Cause and fix |
|---|---|
| Stuck on the loading screen | Invalid mission template in `serverDZ.cfg` (for example after a server panel rewrote it). Set `template = "dayzOffline.chernarusplus";` (or your map) in the panel. |
| `Can't compile "World"/"Mission" script module` | A PBO is out of date or mixed versions are loaded. Repack all three mods from the same source and re-sign the client PBOs. Note the file and line in the dialog when reporting. |
| Pressing U does nothing / "Access Denied" | Your SteamID64 is not a suite administrator or staff editor. Add it to `General\suite.json` (`adminSteamIds`) with the server stopped, or ask an administrator to add you in the Control Room. |
| A basic fallback editor opens instead of the Control Room | Lemmy's Core is not running on the server (not in `-serverMod` or `addons\`), or its module is disabled. Core is required. |
| `Can't find variable 'LSCClient'` (Advanced Banking, Mission module) | The Advanced Groups PBO was packed from an old source folder without the `SuiteConsole` scripts. Repack Advanced Groups from the current source. |
| No *Breach Banking Terminal* action at an ATM | Hands must be empty; scroll the mouse wheel to it and hold F. Robbery must be on and the ATM's *Can be robbed* on. |
| Breach finishes but pays nothing | Read the on-screen notice and `LemmysSuite\Logs\AdvancedBanking`. Builds before 7 November crashed when the breach started (`NULL pointer ... StartRobATM`); update. |
| "Bank server did not respond. Verify client and server use the same PBO." | The client's Advanced Banking PBO differs from the server's. Update the client mod. |
| A change says "not applied yet" after APPLY LIVE | The server refused it: the status line and the red text under the field say why. Fix the value and apply again. |
| "X changed this module…" conflict | Another admin applied first. Your edits are kept: check the refreshed values and apply again. |
| A setting tagged RESTART did nothing | It is saved; it takes effect after the next restart. |
| Settings went back to defaults | Restore the last good version from **Version history**. Every apply keeps a copy in `LemmysSuite\History\<Module>\`. |
| Map picker or colour picker does not open | The client PBO is missing `lsc_map_modal.layout` / `lsc_color_modal.layout`; repack the client mod. |
| Deposit/withdraw says "Enter an amount greater than zero" even with a number in the box | The amount boxes in `BankingMenuTabbed.layout` must use `style EditBox`. With `style Default` the box shows text but `GetText()` returns nothing, so no request is ever sent. This is fixed in current builds; repack the client PBO if you still see it. For any custom layout, keep every `EditBoxWidgetClass` on `style EditBox`. |
| ATMs missing after restart | Check *ATM placements*: the ATM must be **ATM active** and have a position. Applying rebuilds them immediately. |

## Logs to send with a bug report

- Server: `LemmysSuite\Logs\suite.log`, `core.log`, the module log, and the server `script_*.log` / `crash_*.log`.
- Client: `%LocalAppData%\DayZ\script_*.log` and `crash_*.log` from the same time.

{% endraw %}
