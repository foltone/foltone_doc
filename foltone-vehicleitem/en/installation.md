---
title: "Installation"
description: "Installation guide for the foltone_vehicleitem script"
script: "foltone-vehicleitem"
section: "Vehicle Item"
order: 1
version: "1.0.0"
---

# Installation

## Prerequisites

Before installing `foltone_vehicleitem`, make sure the following resources are installed:

- **es_extended** (ESX Framework)
- **oxmysql** (database)

## Installation steps

### 1. File transfer

Place the `foltone_vehicleitem` folder in your `resources/` directory:

```
resources/
  [esx]/
  [foltone]/
    foltone_vehicleitem/
      client/
      server/
      shared/
      fxmanifest.lua
```

### 2. SQL import

Run the provided SQL file to add vehicle items to your database:

```sql
SOURCE install.sql;
```

This will add the required items (e.g., `bmx_item`, etc.) to your `items` table.

### 3. server.cfg configuration

Add the resource to your `server.cfg` **after** its dependencies:

```cfg
ensure es_extended
ensure oxmysql
ensure foltone_vehicleitem
```

### 4. Item verification

Make sure each vehicle configured in the script has a matching item in the `items` database table.

## Verification

1. Start the server
2. Connect in-game
3. Check that the shop is accessible (if configured)
4. Test purchasing and spawning a vehicle from inventory

## Important notes

- This script does **not** require esx_society or esx_addonaccount.
- Configuration files (`shared/`) can be freely modified.
- The script is compatible with standard ESX inventories.
