---
layout: page
title: "Advanced Banking"
section: DOCUMENTATION
permalink: /docs/advanced-banking.html
---
{% raw %}
# Advanced Banking

Bank accounts used at ATMs placed around the map. Every server setting is listed in the [Advanced Banking settings reference](settings/advanced-banking.html); the ATM screen is [`BankingMenuTabbed`](layouts/advanced-banking/BankingMenuTabbed.html).

## For players

### Using an ATM

Walk up to an ATM and use it. The menu has two tabs (three for admins):

**Banking**
- **Personal Account / Group Account** — switch between your own account and your group's shared account (needs Advanced Groups). If the group has no account yet and the server charges an opening cost, the leader opens it here.
- **Bank balance** shows `balance / account limit`; **Cash on hand** is the money items in your inventory.
- Type an amount and press **Deposit** or **Withdraw**. **DEPOSIT ALL CASH** pays in every money item you carry; **WITHDRAW ALL** takes out as much as the account and your inventory allow.
- **Close Empty Group Account** removes a group account with a zero balance.

**Transfers**
- Send money to an online player or, from the account directory, to an offline player or a group. A flat fee plus a percentage is charged (VIP tiers can be fee-free).
- The history list shows your last transactions page by page.

Rules the server may set: smallest and largest transaction, daily deposit/withdrawal/transfer limits, a short pause between operations, deposit-only or no-cash ATMs, and which group ranks may deposit, withdraw or send group money.

### Money

Money items (for example ruble notes) are accepted at the value the server sets; withdrawals pay out the largest notes first. Some items can be deposit-only.

### Income

- **Activity pay:** while you are online you receive a paycheck every set number of minutes. It can grow by a fixed amount with each payout up to a maximum, and reset when you log out.
- **Interest:** balances can earn interest on a schedule, up to a cap.
- **Paycheck events:** admins can run a temporary bonus on all paychecks.

### Robbing an ATM

If robbery is on, look at an ATM with empty hands, scroll the mouse wheel to **Breach Banking Terminal** and **hold F** until the bar is full (3 minutes by default). Letting go, walking away, dying or logging out cancels it. The result — the reward, or why the breach was refused (cooldown, robbery off, protected ATM, too far away) — appears as an on-screen notice.

The breach takes a set time; nearby players hear an alarm, police (SteamIDs or whole groups) get the ATM's location, and a danger marker can appear on the map. With **defence waves** on, infected or AI spawn around the ATM in waves while the breach runs. A successful breach pays a random reward — or, with **cash pools** on, a share of the cash deposited at that ATM. Each ATM and each robber has a cooldown, and some ATMs can be immune (for example in safe zones).

## For admins

### Opening the tools

- **Numpad 9**, or the admin button in the ATM menu, opens the [Control Room](control-room.html) on Advanced Banking.
- The ATM menu's **Admin** tab (banking administrators only) handles accounts and money:
  - Search accounts by player or group name; online players are listed first and marked `[ONLINE]`, group accounts `[GROUP]`.
  - **Credit / Debit / Set** a balance, **Freeze / Unfreeze**, **Archive / Restore** — each needs an audit reason (3+ characters) and is logged.
  - **Money drop:** send or remove the same amount on *online players*, *all player accounts* or *all accounts including groups*. Removing asks for a second click within 5 seconds.
  - Double-click an account to see its audited history.
- The **admin tablet** item (`AdvancedBanking_AdminTablet`) opens the banking admin page away from an ATM.

### Placing ATMs

Control Room → Advanced Banking → **ATMs and currency** → *ATM placements*:

1. **+ ADD ATM** — the Control Room closes and a see-through ATM follows your crosshair ([world placement](control-room.html#world-placement)). Q/E rotate, Page Up/Down adjust height, left click places, Backspace cancels.
2. Name it and set its rules:
   - **ATM active** — off removes it from the map but keeps its settings.
   - **Accepts deposits / Pays out cash** — for example a deposit-only terminal.
   - **Can be robbed** — off makes it immune to robbery.
3. **APPLY LIVE**. ATMs are rebuilt immediately.

To move an ATM later, open its record and press **PLACE IN WORLD** on *Position*; **MY HEADING** on *Rotation* turns it to face your direction.

### What admins configure

All in the Control Room ([full reference](settings/advanced-banking.html)): accounts and limits, transfers and fees, paychecks/interest/activity pay, ATM robbery and cash pools, ATM placements and currency items, robbery defence waves (creature class names via **ADD CLASS**), VIP tiers, TraderPlus import, and the banking administrators and Discord audit feed.

### Importing from TraderPlus

Keep TraderPlus's files in `$profile:TraderPlus`, then in *Import from TraderPlus* switch on **Import balances now** (and optionally currency items) and apply. Balances are added to the matching player accounts; the import is logged.

### Audit

Every admin action and large transaction is written to the banking log and, if enabled, to the Discord audit webhook.

{% endraw %}
