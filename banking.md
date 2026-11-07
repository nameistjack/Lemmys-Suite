---
layout: page
title: Advanced Banking
section: CLIENT + SERVER MOD
permalink: /banking/
---

# Advanced Banking

<p class="page-links"><a class="button primary" href="{{ site.links.workshop_banking }}" target="_blank" rel="noreferrer">Steam Workshop</a> <a class="button secondary" href="{{ site.links.discord }}" target="_blank" rel="noreferrer">Discord support</a></p>

Advanced Banking needs [Lemmy's Core]({{ site.baseurl }}/core/) on the server (`-serverMod`). The full guide is in the [documentation]({{ site.baseurl }}/docs/advanced-banking.html), every setting in the [settings reference]({{ site.baseurl }}/docs/settings/advanced-banking.html).

Advanced Banking gives players a personal bank account and, with Advanced Groups loaded, a shared group account. Players use it at ATMs placed in the world. The ATM model ships inside the PBO, so it needs no other model mod. Money moves as real ruble items: depositing takes them out of your inventory and withdrawing puts them back in.

The server decides everything. The client never sends a balance, a fee, a rank or an "I am allowed" flag.

## For players

- Walk up to an ATM (within `atmInteractionDistance`, default 4 m) and use it.
- **Deposit** and **Withdraw** take digits only. **Deposit all** and **Withdraw all** do what they say. The balance is shown as `current / maximum`.
- **Transfers** go to online players, to anyone in the offline directory search, or between your personal and group accounts. The fee is shown before you confirm.
- **History** is paged and keeps the last `transactionHistoryLimit` (default 200) entries per account.
- **Group account:** whether you can deposit, withdraw or transfer depends on your rank in the group. If the server charges for opening one, the leader sees an **Open group account** button with the price.

## ATMs

- **Placing ATMs:** Control Room → Advanced Banking → *ATMs and currency* → **+ ADD ATM**. A see-through ATM follows your crosshair: Q / E rotate, Page Up / Page Down height, **left click** places, Backspace cancels. Name it, set its switches and **APPLY LIVE** — it appears at once, no restart. To move one later, open its record and press **PLACE IN WORLD**.
- **Per-ATM switches:** `allowDeposit`, `allowWithdraw` and `canBeRobbed`. This gives you a deposit-only ATM in a safe zone, or a withdraw-only one at a trader.
- The admin tablet (`AdvancedBanking_AdminTablet`) opens the banking admin page away from an ATM.

## Limits and fees

| Setting | Default |
|---|---|
| `personalStartBalance` | 100000 |
| `personalMaximumBalance` / `groupMaximumBalance` | 999999999 |
| `minimumTransactionAmount` / `maximumTransactionAmount` | 1 / 100000000 |
| `dailyDepositLimit` / `dailyWithdrawalLimit` / `dailyTransferLimit` | 50M / 25M / 50M |
| `operationCooldownSeconds` | 2 |
| `transferFlatFee` + `transferPercentFee` | 100 + 2.5% |
| `groupDepositMinimumRank` / `groupWithdrawMinimumRank` / `groupTransferMinimumRank` | 0 / 1 / 2 |
| `groupMinimumMembers` | 1 |
| `groupOpeningCost` | 0, the account opens on its own |
| `groupBalancePerMember` | 0; above 0 the group's maximum grows with each member |

Every request carries a request id. If the same request arrives twice, for example after a lag spike or a double-click, the second copy is refused.

## VIP tiers

`vipTiers` is a list of tiers. Each tier has:

| Field | Meaning |
|---|---|
| `name` | shown on the player's banking screen |
| `steamIds` | SteamID64s in the tier |
| `bonusMaximumBalance` | added to the personal balance cap |
| `bonusPaycheck` | added to every paycheck |
| `feeFree` | transfers from this player cost no fee |

Tiers are checked by SteamID64, which is saved on the account the first time the player uses an ATM, so they also apply while the player is offline. A player listed in two tiers gets the first one in the list.

## Paychecks and interest

- `enablePaychecks`, `paycheckAmount`, `paycheckIntervalMinutes` pay online players on a timer.
- **Double pay weekend:** `paycheckEventPercent` (for example `200`) multiplies paychecks until `paycheckEventEnds`, a date and time such as `2026-11-08 23:59` (server time, `YYYY-MM-DD HH:MM`). After that time the bonus stops on its own.
- `enableInterest`, `interestPercent`, `interestIntervalMinutes`, `interestMaximumPayment` cover interest. The maximum payment keeps large balances from running away.

## ATM robbery

This is off until `enableATMRobbery` is turned on, and each ATM still needs `canBeRobbed`.

1. With empty hands, a player looks at the ATM, scrolls the mouse wheel to **Breach Banking Terminal** and **holds F** for `robberyDurationSeconds` (180 s by default), staying alive, connected and close to it. The result — the reward, or why the breach was refused — shows as an on-screen notice.
2. **Alarm.** Everyone within `robberyAlarmRadius` (default 300 m) hears it. `robberyAlarmSoundSet` is empty by default; set it to a sound set your server has.
3. **Police.** Online players listed in `robberyPoliceSteamIds` (SteamID64), or in an Advanced Groups group whose name is in `robberyPoliceGroups`, get a direct alert. With Advanced Groups loaded, `robberyMapMarker` also puts a red 75 m circle on everyone's map until the robbery ends.
4. **If the robber dies, disconnects or walks away**, the robbery is announced as abandoned. It does not carry on: the next robber starts from zero.
5. **PvE waves** (`robberyPvEWaves`). AI from `robberyWaveClassnames` spawns around the ATM:
   - the first wave comes after `robberyFirstWaveDelaySeconds`, then one every `robberyWaveIntervalSeconds`;
   - each wave has `robberyWaveSize` AI, with at most `robberyWaveMaxAlive` alive at once;
   - they spawn between `robberyWaveRadiusMin` and `robberyWaveRadiusMax` metres out;
   - leftovers are cleaned up after `robberyWaveCleanupMinutes`.
6. **Reward.** A random amount between `robberyMinimumReward` and `robberyMaximumReward`, paid as cash in hand (`robberyPaysCash`) or to the account.

There are cooldowns per ATM (`robberyCooldownMinutes`) and per robber (`robberyRobberCooldownMinutes`), plus a minimum player count and a limit on robberies running at once.

**Cash pools** (`enableCashPools`). Each ATM holds real money: deposits fill it, withdrawals drain it, and it trickles up by `cashPoolTricklePerHour`. A robbery then steals `cashPoolStealPercent` of what is inside, up to `cashPoolMaximumSteal`, instead of a random reward. An ATM nobody uses is not worth robbing.

## Importing from TraderPlus

You don't need TraderPlus installed, only its old files.

- `importTraderPlusCurrencies` reads the currency classes and values from `$profile:TraderPlus/TraderPlusConfig/TraderPlusGeneralConfig.json` once and merges any that are missing.
- `importTraderPlusBalances` reads every account in `$profile:TraderPlus/TraderPlusBankDatabase/`. The money is held in an import ledger and paid into the player's account the first time they use an ATM. Each SteamID can be imported only once, so restarting with the switch still on doesn't pay anyone twice.

## Admin console

The admin page (Numpad 9, or the ATM's admin action) gives you:

- account search, economy totals and paged history per account;
- credit, debit, set balance, freeze, unfreeze, archive and restore. Each needs a reason and goes to the append-only audit log;
- optional Discord webhook for the audit log, with a dead-letter file if Discord is down.

## Files

| File | Where |
|---|---|
| Config | `LemmysSuite/Configs/AdvancedBanking/config.json`, or `$profile:Advanced_Banking/config.json` without Core |
| Accounts | `LemmysSuite/Data/AdvancedBanking/accounts/personal/` and `accounts/groups/` |
| Robbery state, import ledger | next to the accounts |
| Audit log | `LemmysSuite/Logs/AdvancedBanking/` |

Every account save is written to a temp file and checked before it replaces the real one. A transfer between two accounts is saved as a pair, so you can't end up with one side saved and the other not.
