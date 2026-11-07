---
layout: page
title: "Architecture"
section: DOCUMENTATION
permalink: /docs/architecture.html
---
{% raw %}
# Architecture

## Pieces

```
            CLIENT (player PC)                                   SERVER
┌──────────────────────────────────────┐        ┌───────────────────────────────────────────┐
│ Advanced Groups (AdvancedGroups.pbo) │        │ Lemmy's Core (Lemmys_Core.pbo, server only)│
│  · group menu, chat, HUD, markers    │        │  · module registry      LMSModuleRegistry  │
│  · Control Room window  (LSC*)       │◄──────►│  · Control Room service LMSConfigService   │
│    LSCClient / LSCDraft / LSCConsole │  CF    │  · providers  LMSProviderGroups/Banking/   │
│                                      │  RPC   │               Spawn/Core                   │
│ Advanced Banking (Advanced_Banking)  │        │  · history, audit, logging, migration      │
│  · ATM menu (IABMenuComplete)        │◄──────►│ Advanced Groups server  AGServerManager... │
│  · copy of the Control Room window   │        │ Advanced Banking server IABBankService...  │
└──────────────────────────────────────┘        └───────────────────────────────────────────┘
```

- **Lemmy's Core** never runs on clients. The Control Room *window* therefore ships in the client mods: Advanced Groups has it, and Advanced Banking carries an identical copy guarded by `#ifndef AdvancedGroups`, so a Banking-only server still has it and a server running both never defines it twice.
- Each module keeps its own loader and validation. Core talks to a module only through its **provider** (`LMSConfigProvider`): describe the settings, load, read/write values, build lists, validate, persist, activate.

## Control Room data flow

1. **Hello** — the client asks for the catalog. Core checks access and returns the modules this player may edit (`LMSDocKind.CATALOG`).
2. **Open** — when a module is entered, the client sends the schema hash it already has; Core sends the **schema** only if it changed, then the current **state** (all values and list records).
3. **Draft** — every edit is kept client-side in `LSCDraft` (values, lists, undo/redo, errors). Nothing is sent while editing.
4. **Apply** — the client sends a **patch**: changed keys and full replacement lists, plus the base revision.
5. **Server apply** (`LMSConfigService.ApplyPatch`):
   - rejects the patch if another admin applied first (base revision differs);
   - validates every value with `LMSValueCodec`, then module rules with `provider.Validate`;
   - snapshots the current files into `History\`;
   - writes values through `LMSReflect` (by member name) or the provider's custom readers/writers, rebuilds lists from fresh records, carrying hidden members over with `LMSCarry`;
   - `provider.Persist()` saves through the module's own loader and reads the file back to verify;
   - `provider.Activate()` hot-reloads the module;
   - bumps the revision, writes the audit line, sends the new state to the editor and a *changed* notice to other open editors.
6. Documents larger than one RPC are split into chunks (`LMSChunk` / `LSCChunk`) and reassembled.

## Client ↔ server namespaces

| Namespace | Used by |
|---|---|
| Control Room (Core ↔ `LSCClient`) | Hello, Open, Close, Up (patch chunks), history and restore |
| `AdvancedBanking` | Snapshot, terminal info, cash operations, transfers, history, admin and ATM operations, robbery |
| Advanced Groups (integer RPC ids, `AGRPCs`) | 112 group, chat, marker, zone, mailbox and admin RPCs; admin RPCs pass through `AGAdminPermissions.CanUseAdminRPC` |

## Script layers

| Layer | Advanced Groups | Advanced Banking | Lemmy's Core |
|---|---|---|---|
| 3_Game | config models, enums, structs, wire formats | models (`IABConfig`, accounts, ATM positions), suite extras | wire formats, logger, profile paths |
| 4_World | HUD, client state, config loader, zones, territories | ATM entity, admin tablet, storage, currency | provider base, schema builder, reflection, registry, migration |
| 5_Mission | menus, pages, chat, RPC managers, server services, Control Room window | ATM menu, RPC manager, bank service, Control Room copy | Control Room service, providers, bootstrap |

## UI theme

The Control Room uses the **Arctic Glass** palette (`LSCTheme`), mirrored in the [design file](design.html):

| Token | Colour | Used for |
|---|---|---|
| Surface | `#0C2530` 86% | window background |
| Raised | `#133442` 90% | rows, cards |
| Nested | `#0E2A36` 95% | records inside lists |
| Selected | `#12424F` | selected rail row |
| Inset | `#061117` | edit boxes |
| Accent | `#39E7FF` | cyan accents, current record |
| Modified | `#FF8A1F` | pending edits |
| Error | `#FF4D62` | invalid values, careful tags |
| Success | `#53F2A1` | applied, connected |
| Warning | `#FFD166` | restart tags, conflicts |
| Text / Muted / Faint | `#DEE5E8` / `#A3B1B8` / `#5E7079` | text levels |

{% endraw %}
