---
title: "Installation"
description: "Banking script installation guide"
script: "foltone-banking"
section: "Banking"
order: 1
version: "1.0.0"
---

# Installation — foltone_banking

## Requirements

- **ESX Legacy** or **QBCore** or **QBX** — Framework
- **oxmysql** — MySQL library

### Optional Dependencies

| Dependency | Purpose |
|---|---|
| `esx_addonaccount` | Society accounts (ESX only) |
| `qb-banking` | Society accounts (QBCore / QBX only) |
| `ox_target` | Target interaction mode |
| `qb-target` | Target interaction mode |
| `qtarget` | Target interaction mode |
| `ox_inventory` | Physical bank card as item |
| `lb-phone` | Phone notifications |
| `qs-smartphone` | Phone notifications |
| `gksphone` | Phone notifications |

## Download

Download the script from your [Tebex](https://foltone.tebex.io/) account and place the `foltone_banking` folder in your `resources/` directory.

## Server Configuration

Add to your `server.cfg`:

```ini
ensure oxmysql
ensure es_extended       # or qb-core / qbx_core
ensure esx_addonaccount  # ESX only, for society accounts
ensure foltone_banking
```

> **Important**: `foltone_banking` must start **after** your framework and `oxmysql`. If you use optional dependencies (ox_target, lb-phone, etc.), ensure them **before** `foltone_banking`.

## Framework

The script supports 3 frameworks:

| Framework | Config value | Required dependencies | Society dependency |
|---|---|---|---|
| ESX Legacy | `"esx"` | `es_extended`, `oxmysql` | `esx_addonaccount` |
| QBCore | `"qbcore"` | `qb-core`, `oxmysql` | `qb-banking` |
| QBX | `"qbx"` | `qbx_core`, `oxmysql` | `qb-banking` |

Set the framework in `config.lua`:

```lua
Config.Framework = "esx" -- "esx", "qbcore" or "qbx"
```

## Database Setup

### Fresh Install

Run the `sql/install.sql` file in your database. This creates all required tables:

- `foltone_banking_accounts` — Personal accounts
- `foltone_banking_transactions` — Personal transaction history
- `foltone_banking_cards` — Bank cards
- `foltone_banking_society_transactions` — Society transaction history
- `foltone_banking_joint_accounts` — Joint accounts
- `foltone_banking_joint_members` — Joint account members
- `foltone_banking_joint_transactions` — Joint transaction history
- `foltone_banking_savings` — Savings accounts
- `foltone_banking_savings_locks` — Fixed-term deposits
- `foltone_banking_crypto_holdings` — Crypto portfolios
- `foltone_banking_crypto_trades` — Crypto trade history

```sql
-- Import the full schema
SOURCE sql/install.sql;
```

### Updating from a Previous Version

If you are updating from an earlier version, run the appropriate migration files **in order**:

| Migration file | Adds |
|---|---|
| `sql/migrate_phase3.sql` | Credit score, account levels, interest, taxation columns |
| `sql/migrate_phase4.sql` | Joint accounts tables |
| `sql/migrate_phase5.sql` | Savings and crypto tables, extended transaction ENUM |

> **Warning**: Only run migration files that correspond to versions you have **not** yet installed. Running `install.sql` on a fresh server already includes everything.

## Verification

After restarting your server:

1. Check the server console for any errors related to `foltone_banking`
2. Connect with a character
3. Go to a **bank location** (a PED should be spawned at configured positions) or approach an **ATM**
4. Interact with the bank PED or ATM to open the banking interface
5. The NUI should appear with the dashboard showing your balance, IBAN, and available operations
