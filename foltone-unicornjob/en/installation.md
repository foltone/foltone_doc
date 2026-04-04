---
title: "Installation"
description: "Installation guide for the foltone_unicornjob script"
script: "foltone-unicornjob"
section: "Unicorn Job"
order: 1
version: "1.0.0"
---

# Installation

## Prerequisites

Before installing `foltone_unicornjob`, make sure the following resources are installed and running:

- **es_extended** (ESX Framework)
- **oxmysql** (database)
- **esx_addonaccount** (society accounts)
- **esx_addoninventory** (society inventory)
- **esx_society** (society management)

## Installation steps

### 1. File transfer

Place the `foltone_unicornjob` folder in your `resources/` directory:

```
resources/
  [esx]/
  [foltone]/
    foltone_unicornjob/
      client/
      server/
      shared/
      fxmanifest.lua
```

### 2. SQL import

Run the provided SQL file in your database:

```sql
SOURCE install.sql;
```

This will create the tables for the Unicorn society, accounts, and associated inventories.

### 3. server.cfg configuration

Add the resource to your `server.cfg` **after** its dependencies:

```cfg
ensure es_extended
ensure oxmysql
ensure esx_addonaccount
ensure esx_addoninventory
ensure esx_society
ensure foltone_unicornjob
```

### 4. Job setup

Make sure the `unicorn` job exists in the `jobs` and `job_grades` tables. A sample SQL file is included with the resource.

### 5. Item setup

Add bar items (drinks, cocktails, etc.) to your `items` table if not already created by the installation SQL.

## Verification

1. Start the server
2. Connect in-game
3. Check for the Unicorn blip on the map
4. Assign yourself the job and test bar access

## Important notes

- Script is **escrow** protected (Tebex). Protected files cannot be modified.
- `shared/` files are fully configurable.
- Check the server console for errors if you encounter issues.
