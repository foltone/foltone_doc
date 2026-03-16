---
title: "Installation"
description: "Installation guide for Foltone Garage"
script: "foltone-garage"
section: "Foltone Garage"
order: 1
version: "2.0.0"
---

# Installation — foltone_garage

## Requirements

- **ESX Legacy**, **QBCore**, or **QBX** — FiveM framework
- **oxmysql** — MySQL library

### Optional dependencies

| Dependency | Purpose | Required for |
|-----------|---------|-------------|
| `ox_target` | 3D target interaction | If `Config.InteractionType = "ox_target"` |
| `qb-target` | 3D target interaction | If `Config.InteractionType = "qb-target"` |
| `interact` | 3D target interaction | If `Config.InteractionType = "interact"` |

## Download

Download the script from your Tebex account and place the `foltone_garage` folder in your `resources/` directory.

## Server configuration

Add to your `server.cfg`:

```ini
ensure oxmysql
ensure es_extended      # or qb-core / qbx_core
ensure foltone_garage
```

> **Important**: `foltone_garage` must start **after** your framework (`es_extended`, `qb-core` or `qbx_core`) and `oxmysql`.

## Framework

The script supports 3 frameworks:

| Framework | Config value | Dependencies |
|-----------|-------------|-------------|
| ESX Legacy | `"esx"` | `es_extended`, `oxmysql` |
| QBCore | `"qbcore"` | `qb-core`, `oxmysql` |
| QBX | `"qbx"` | `qbx_core`, `oxmysql` |

Set the framework in `Config.lua`:

```lua
Config.Framework = "esx" -- "esx", "qbcore" or "qbx"
```

## Database

### Fresh installation

Execute the `sql/install.sql` file in your MySQL database:

```bash
mysql -u root -p your_database < sql/install.sql
```

You can also copy the file contents and run it in phpMyAdmin or HeidiSQL.

### Updating from an existing installation

If you are updating from a previous version (before v2.0.0), run the migration file:

| File | Content |
|------|---------|
| `sql/migrate_pound_time.sql` | Adds the `pound_time` column to existing vehicles |

> **Important**: Only run `migrate_pound_time.sql` if you have an existing installation. Do not run it on a fresh database.

## Verification

After restarting the server:

1. Connect to the server with a character
2. Go to a garage position configured in `config_garage.lua`
3. Interact with the PED (or marker depending on your configuration)
4. The NUI interface should appear with the Vehicles, Store, Pound and Label tabs
