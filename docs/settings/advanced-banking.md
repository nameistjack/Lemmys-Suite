---
layout: page
title: "Advanced Banking settings"
section: DOCUMENTATION
permalink: /docs/settings/advanced-banking.html
---
{% raw %}
# Advanced Banking settings

Every setting the Control Room shows for this module, in the order it shows them. Values are applied live when you press **APPLY LIVE** unless the setting is tagged *restart*.

**Tags:** *careful* — asks for a note and is highlighted; *restart* — saved now, used after the next restart; *advanced* — hidden until SHOW ADVANCED; *read only* — shown for reference; *required* — cannot be empty.


## Accounts

Starting money and the most an account can hold.

Section id: `accounts` · stored in `IABConfig`

| Setting | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **Banking open** *careful* | `enabled` | On / off |  | `true` | When off, every ATM refuses service. Balances are kept. |
| **Personal starting balance**  | `personalStartBalance` | Whole number | 0 – 2000000000 money | `100000` | Money in a new player's account. |
| **Personal account limit**  | `personalMaximumBalance` | Whole number | 0 – 2000000000 money | `999999999` | A personal account can never hold more than this. |
| **Group starting balance**  | `groupStartBalance` | Whole number | 0 – 2000000000 money | `0` | Money in a newly opened group account. |
| **Group account limit**  | `groupMaximumBalance` | Whole number | 0 – 2000000000 money | `999999999` | A group account can never hold more than this. |
| **Members needed for a group account**  | `groupMinimumMembers` | Whole number | 1 – 100 members | `1` | Smaller groups cannot use a shared account. |
| **Who may deposit to the group**  | `groupDepositMinimumRank` | Choice | 0 = Member<br>1 = Officer<br>2 = Co-Leader<br>3 = Leader | `0` | Lowest group rank allowed to pay in. |
| **Who may withdraw from the group**  | `groupWithdrawMinimumRank` | Choice | 0 = Member<br>1 = Officer<br>2 = Co-Leader<br>3 = Leader | `1` | Lowest group rank allowed to take money out. |
| **Who may send group money**  | `groupTransferMinimumRank` | Choice | 0 = Member<br>1 = Officer<br>2 = Co-Leader<br>3 = Leader | `2` | Lowest group rank allowed to transfer from the group account. |
| **Group account opening cost**  | `groupOpeningCost` | Whole number | 0 – 2000000000 money | `0` | The group leader pays this from their personal account to open the group account. 0 = groups get an account automatically. |
| **Extra group limit per member**  | `groupBalancePerMember` | Whole number | 0 – 2000000000 money | `0` | Added to the group account limit for every member, so bigger groups can save more. 0 = off. |

## Limits

Per transaction and per day caps that slow down abuse.

Section id: `limits` · stored in `IABConfig`

| Setting | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **Smallest transaction**  | `minimumTransactionAmount` | Whole number | 1 – 2000000000 money | `1` | Deposits, withdrawals and transfers below this are refused. |
| **Largest transaction**  | `maximumTransactionAmount` | Whole number | 1 – 2000000000 money | `100000000` | A single operation can move at most this much. |
| **Daily deposit limit**  | `dailyDepositLimit` | Whole number | 0 – 2000000000 money | `50000000` | Per account, resets at midnight server time. |
| **Daily withdrawal limit**  | `dailyWithdrawalLimit` | Whole number | 0 – 2000000000 money | `25000000` | Per account, resets at midnight server time. |
| **Daily transfer limit**  | `dailyTransferLimit` | Whole number | 0 – 2000000000 money | `50000000` | Per account, resets at midnight server time. |
| **Pause between operations**  | `operationCooldownSeconds` | Whole number | 0 – 3600 seconds | `2` | Stops players from spamming the ATM. |
| **History entries kept** *advanced* | `transactionHistoryLimit` | Whole number | 1 – 5000 entries | `200` | Older account history is dropped. |
| **Duplicate-request memory** *advanced* | `processedRequestLimit` | Whole number | 16 – 10000 requests | `128` | How many recent request ids are remembered to block double submissions. |

## Transfers and fees

Sending money between players and groups.

Section id: `transfers` · stored in `IABConfig`

| Setting | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **Player to player transfers**  | `allowPlayerTransfers` | On / off |  | `true` | Players can send money to other players. |
| **Group transfers**  | `allowGroupTransfers` | On / off |  | `true` | Groups can send money from their shared account. |
| **Flat fee**  | `transferFlatFee` | Whole number | 0 – 2000000000 money | `100` | Charged on every transfer. |
| **Percentage fee**  | `transferPercentFee` | Number | 0 – 100 % | `2.5` | Charged on top of the flat fee, as a share of the amount sent. |

## Paychecks and interest

Money the server pays out on a schedule.

Section id: `income` · stored in `IABConfig`

| Setting | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **Activity pay**  | `enablePaychecks` | On / off |  | `false` | Players are paid for time spent online. Only minutes actually on the server count. |
| **Activity pay amount**  | `paycheckAmount` | Whole number | 0 – 2000000000 money | `0` | First payout of a session, paid into the personal account. |
| **Pay every**  | `paycheckIntervalMinutes` | Whole number | 1 – 1440 minutes | `30` | Online minutes needed for each payout. |
| **Raise per payout**  | `paycheckIncrement` | Whole number | 0 – 2000000000 money | `0` | Each payout in a row pays this much more than the last. 0 keeps every payout the same. |
| **Highest payout**  | `paycheckMaximumAmount` | Whole number | 0 – 2000000000 money | `0` | The raise stops here. 0 = no cap. VIP bonus and pay events are added on top. |
| **Raise resets on logout**  | `paycheckResetOnLogout` | On / off |  | `true` | On: the raise starts over each session. Off: players keep their raise between sessions. |
| **Interest**  | `enableInterest` | On / off |  | `false` | Accounts earn a percentage of their balance. |
| **Interest rate**  | `interestPercent` | Number | 0 – 100 % | `0.0` | Paid each interval on the current balance. |
| **Interest every**  | `interestIntervalMinutes` | Whole number | 1 – 10080 minutes | `1440` | Time between interest payments. |
| **Interest cap**  | `interestMaximumPayment` | Whole number | 0 – 2000000000 money | `100000` | Largest single interest payment. |
| **Paycheck event size**  | `paycheckEventPercent` | Whole number | 0 – 1000 % | `100` | Paychecks are paid at this percentage while an event runs. 200 = double pay. |
| **Paycheck event ends**  | `paycheckEventEnds` | Text |  | `""` | Server time as YYYY-MM-DD HH:MM, for example 2026-11-08 23:59. Leave empty for no event. |

## ATM robbery

Players can break into ATMs for a cash reward.

Section id: `robbery` · stored in `IABConfig`

| Setting | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **ATM robbery**  | `enableATMRobbery` | On / off |  | `false` | Allow the robbery action on ATMs. |
| **Cooldown per ATM**  | `robberyCooldownMinutes` | Whole number | 0 – 10080 minutes | `120` | An ATM cannot be robbed again for this long. |
| **Robbery duration** *read only* | `robberyDurationSeconds` | Whole number | 1 – 3600 seconds | `IAB_ATM_ROBBERY_ACTION_SECONDS` | Fixed in the mod so every client agrees on the action length. |
| **Smallest reward**  | `robberyMinimumReward` | Whole number | 0 – 2000000000 money | `5000` | Lowest cash payout. |
| **Largest reward**  | `robberyMaximumReward` | Whole number | 0 – 2000000000 money | `25000` | Highest cash payout. |
| **Pay out as cash**  | `robberyPaysCash` | On / off |  | `true` | The loot drops into the robber's inventory as money items, so it can be lost or taken. Off pays straight into their bank account. |
| **Announce robberies**  | `robberyAnnounce` | On / off |  | `true` | Every player gets a notification when a breach starts and when it finishes. |
| **Players needed online**  | `robberyMinimumPlayersOnline` | Whole number | 0 – 200 players | `0` | Robberies cannot start on an empty server. 0 = no minimum. |
| **Robberies at the same time**  | `robberyMaximumConcurrent` | Whole number | 1 – 50 robberies | `1` | How many ATMs can be breached at once across the map. |
| **Cooldown per robber**  | `robberyRobberCooldownMinutes` | Whole number | 0 – 10080 minutes | `60` | A player who robbed an ATM waits this long before the next one. |
| **Alarm radius**  | `robberyAlarmRadius` | Whole number | 0 – 5000 m | `300` | Players this close to a breached ATM are warned. 0 = no local alarm. |
| **Alarm sound** *advanced* | `robberyAlarmSoundSet` | Text |  | `""` | Optional sound set played at the ATM when a breach starts, for example from a sound mod you run. Empty = silent. |
| **Police (SteamID64)**  | `robberyPoliceSteamIds` | List (one per line) |  | `(empty)` | These players get a police alert with the ATM's location for every breach, wherever they are. One per line. |
| **Police groups**  | `robberyPoliceGroups` | List (one per line) |  | `(empty)` | Exact Advanced Groups names whose members also get the police alert. One per line. |
| **Mark robberies on the map**  | `robberyMapMarker` | On / off |  | `true` | Shows a red danger marker at the ATM while it is being robbed (needs Advanced Groups). |
| **ATM cash pools**  | `enableCashPools` | On / off |  | `false` | Each ATM holds the cash deposited at it; a robbery steals a share of that instead of a random amount. |
| **Pool refill per hour**  | `cashPoolTricklePerHour` | Whole number | 0 – 2000000000 money | `1000` | Cash added to every ATM's pool each hour, so quiet ATMs are still worth hitting. |
| **Share stolen**  | `cashPoolStealPercent` | Whole number | 1 – 100 % | `25` | Part of an ATM's pool a successful robbery takes. |
| **Most stolen per robbery**  | `cashPoolMaximumSteal` | Whole number | 0 – 2000000000 money | `50000` | Cap on a single robbery from the pool. 0 = no cap. |
| **ATM reach**  | `atmInteractionDistance` | Number | 1 – 20 m | `4.0` | How close a player must stand to use an ATM. |

## ATMs and currency

Where ATMs stand and which items count as money.

Section id: `terminals` · stored in `IABConfig`


### List: ATM placements

ATMs spawn here on every restart and are rebuilt immediately when you apply.

List id: `atmPositions` · up to 200 ATM records · record type `IABATMPosition`

| Field | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **Name** *required* | `name` | Text |  | `"Banking Terminal"` | Shown to admins and in logs. |
| **ATM active**  | `enabled` | On / off |  | `true` | Off removes this ATM from the map until you switch it on again. Its settings are kept. |
| **Position**  | `position` | Position (x y z) |  | `"0 0 0"` | Use PICK ON MAP, or MY POSITION in the map while standing on the spot. |
| **Rotation**  | `orientation` | Position (x y z) |  | `"0 0 0"` | Yaw Pitch Roll in degrees. Usually only the first number matters. |
| **Accepts deposits**  | `allowDeposit` | On / off |  | `true` | Players can pay cash into their account here. |
| **Pays out cash**  | `allowWithdraw` | On / off |  | `true` | Players can take cash out here. Turn off for remote, deposit-only terminals. |
| **Can be robbed**  | `canBeRobbed` | On / off |  | `true` | Off makes this terminal immune to the robbery action (for example in safe zones). |


### List: Currency items

Inventory items accepted as money and paid out on withdrawal, largest value first.

List id: `currencies` · up to 50 currency records · record type `IABCurrencyDefinition`

| Field | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **Item class** *required* | `classname` | Text |  | `""` | Exact item class name, for example MoneyRuble100. |
| **Value**  | `value` | Whole number | 1 – 2000000000 money | `0` | What one item is worth. |
| **Deposit only**  | `depositOnly` | On / off |  | `false` | Accepted at ATMs but never paid out. |


## Robbery defence (PvE)

Hostiles spawn in waves around an ATM while it is being robbed.

Section id: `defence` · stored in `IABConfig`

| Setting | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **Defence waves**  | `robberyPvEWaves` | On / off |  | `false` | Spawn the creatures below around the ATM while a breach runs. |
| **What spawns**  | `robberyWaveClassnames` | List (one per line) |  | `(empty)` | Class names, one per line. Infected (for example ZmbM_PatrolNormal_Autumn) or AI from a mod you run. A random entry is picked for every spawn. |
| **First wave after**  | `robberyFirstWaveDelaySeconds` | Whole number | 0 – 3600 seconds | `10` | Time from the start of the breach to the first wave. |
| **Wave every**  | `robberyWaveIntervalSeconds` | Whole number | 10 – 3600 seconds | `60` | How often a new wave arrives while the breach runs. |
| **Wave size**  | `robberyWaveSize` | Whole number | 1 – 30 creatures | `4` | Creatures per wave. |
| **Most alive at once**  | `robberyWaveMaxAlive` | Whole number | 1 – 100 creatures | `12` | No new spawns while this many are still alive. |
| **Spawn distance from**  | `robberyWaveRadiusMin` | Whole number | 5 – 500 m | `25` | Closest spawn distance from the ATM. |
| **Spawn distance to**  | `robberyWaveRadiusMax` | Whole number | 5 – 1000 m | `60` | Farthest spawn distance from the ATM. |
| **Remove leftovers after**  | `robberyWaveCleanupMinutes` | Whole number | 0 – 120 minutes | `5` | Spawned creatures (alive or dead) are removed this long after the breach ends. 0 = immediately. |

## VIP tiers

Perks for donators, supporters or staff, granted by SteamID64.

Section id: `vip` · stored in `IABConfig`


### List: VIP tiers

A player in several tiers gets the first one in this list.

List id: `vipTiers` · up to 50 tier records · record type `IABVipTier`

| Field | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **Tier name** *required* | `name` | Text |  | `"VIP"` | Shown to the player at the ATM, for example Gold. |
| **Members**  | `steamIds` | List (one per line) |  | `(empty)` | SteamID64s in this tier, one per line. |
| **Extra account limit**  | `bonusMaximumBalance` | Whole number | 0 – 2000000000 money | `0` | Added to the personal account limit. |
| **Extra paycheck**  | `bonusPaycheck` | Whole number | 0 – 2000000000 money | `0` | Added to every paycheck before an event multiplier. |
| **No transfer fees**  | `feeFree` | On / off |  | `false` | Transfers from this player's personal account are free. |


## Import from TraderPlus

Move player bank balances from TraderPlus. Keep TraderPlus's files in $profile:TraderPlus while you import.

Section id: `migration` · stored in `IABConfig`

| Setting | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **Import balances now** *careful* | `importTraderPlusBalances` | On / off |  | `false` | Reads TraderPlusBankDatabase once. Each balance is ADDED to the player's account the first time they connect. Switches itself off; players are never paid twice. |
| **Also import currency items**  | `importTraderPlusCurrencies` | On / off |  | `true` | Adds TraderPlus currency items that are not in the list above yet. |

## Admins and audit

Who manages banking in game, and the Discord audit feed.

Section id: `security` · stored in `IABConfig`

| Setting | Key | Type | Range / options | Default | What it does |
|---|---|---|---|---|---|
| **Banking administrators** *careful* | `adminSteamIds` | List (one per line) |  | `(empty)` | SteamID64s that can use the banking admin page and tablet. One per line. |
| **Discord audit feed**  | `enableDiscordWebhook` | On / off |  | `false` | Post admin and large transactions to Discord. |
| **Discord webhook URL**  | `discordWebhookUrl` | Secret (never shown back) |  | `""` | Saved URLs are never shown again. |

{% endraw %}
