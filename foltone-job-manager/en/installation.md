---
title: "Installation"
description: "Job Manager script installation guide"
script: "foltone-job-manager"
section: "Job Manager"
order: 1
version: "1.0.0"
---

# Installation — foltone_job_manager

## Requirements

- **ESX Legacy** or **QBCore** or **Standalone**
- **oxmysql** — MySQL library
- **esx_addonaccount** *(ESX only)* — For society account management

## Download

Download the script from your Tebex account and place the folder in your `resources/` directory.

## Server Configuration

Add to your `server.cfg`:

```ini
ensure oxmysql
ensure es_extended # or qb-core
ensure foltone_job_manager
```

> **Important**: `foltone_job_manager` must start **after** your framework (`es_extended` or `qb-core`) and `oxmysql`.

## Framework

The script supports 3 modes:

| Framework | Config value | Dependencies |
|-----------|-------------|--------------|
| ESX Legacy | `"esx"` | `es_extended`, `oxmysql`, `esx_addonaccount` |
| QBCore | `"qbcore"` | `qb-core`, `oxmysql`, `qb-banking` |
| Standalone | `"standalone"` | Manual configuration required |

Set the framework in `config.lua`:

```lua
Config.Framework = "esx" -- "esx", "qbcore" or "standalone"
```

## Verification

After restarting your server:

1. Connect with a character that has the **boss** grade for a configured job
2. Go to the society marker (position configured in `config.lua`)
3. Press **E** to open the management interface
4. The tablet interface should appear with tabs: Money, Employees, Salaries, Transfers
