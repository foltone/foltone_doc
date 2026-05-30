---
title: "Installation"
description: "Tattoo shop script installation guide"
script: "foltone-tattooshop"
section: "Tattoo Shop"
order: 1
version: "1.0.0"
---

# Installation

## Requirements

- **Framework**: ESX Legacy, QBCore, or QBX
- **Database**: oxmysql
- **FiveM**: Latest recommended artifacts

## Database Setup

The script stores player tattoos in a dedicated column. You need to add a `tattoos` column of type `LONGTEXT` to your player table.

### ESX Legacy

```sql
ALTER TABLE users ADD COLUMN tattoos LONGTEXT DEFAULT NULL;
```

### QBCore / QBX

```sql
ALTER TABLE players ADD COLUMN tattoos LONGTEXT DEFAULT NULL;
```

## Framework Configuration

In your `config.lua`, set the framework you are using:

```lua
Config.Framework = "esx"     -- For ESX Legacy
Config.Framework = "qbcore"  -- For QBCore
Config.Framework = "qbx"     -- For QBX
```

## Server Configuration

Add the following to your `server.cfg`, respecting the load order:

```cfg
ensure oxmysql
ensure es_extended   # or qb-core / qbx-core depending on your framework
ensure foltone_tattooshop
```

Make sure `oxmysql` and your framework resource are started **before** `foltone_tattooshop`.

## Tattoo Shop Locations

The script comes with **6 pre-configured tattoo shop locations**, each with a map blip. These positions can be customized in `config.lua` under `Config.TattooShopPositions`.
