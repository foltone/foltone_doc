---
title: "Installation"
description: "Installation guide for the foltone_tobaccojob script"
script: "foltone-tobaccojob"
section: "Tobacco Job"
order: 1
version: "1.0.0"
---

# Installation

## Prerequisites

Before installing `foltone_tobaccojob`, make sure the following resources are installed and running on your server:

- **es_extended** (ESX Framework)
- **oxmysql** (database)
- **esx_addonaccount** (society accounts)
- **esx_addoninventory** (society inventory)
- **esx_society** (society management)

## Installation steps

### 1. File transfer

Place the `foltone_tobaccojob` folder in your `resources/` directory:

```
resources/
  [esx]/
  [foltone]/
    foltone_tobaccojob/
      client/
      server/
      shared/
      fxmanifest.lua
```

### 2. SQL import

Run the provided SQL file in your database:

```sql
-- Import the install.sql file included with the resource
SOURCE install.sql;
```

This will create the required tables for the society, accounts, and inventories.

### 3. server.cfg configuration

Add the resource to your `server.cfg` **after** its dependencies:

```cfg
ensure es_extended
ensure oxmysql
ensure esx_addonaccount
ensure esx_addoninventory
ensure esx_society
ensure foltone_tobaccojob
```

### 4. Job setup

Make sure the `tobaccojob` job exists in your `jobs` and `job_grades` database tables. A sample SQL file is provided.

### 5. Item setup

Add the required items (tobacco leaves, cigarettes, etc.) to your `items` table if not already done by the installation SQL.

## Verification

1. Start your server
2. Connect in-game
3. Check that the blip appears on the map
4. Assign yourself the job via admin command or database

## Important notes

- This script is **escrow** protected (Tebex). Do not modify protected files.
- Configuration files (`shared/`) can be freely modified.
- If you encounter issues, check the server console for error messages.
