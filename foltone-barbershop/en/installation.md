---
title: "Installation"
description: "Barbershop script installation guide"
script: "foltone-barbershop"
section: "Barbershop"
order: 1
version: "1.0.0"
---

# Installation

## Requirements

- **Framework**: ESX Legacy, QBCore, or QBX
- **Database**: oxmysql
- **Appearance resource** (QBCore/QBX only): `illenium-appearance`, `fivem-appearance`, or `qb-clothing`

No additional SQL file is required. The barbershop does not store its own data in the database — it relies on your appearance resource to save and load player looks.

## Framework Configuration

In `config.lua`, set your framework:

```lua
Config.Framework = "esx"       -- For ESX Legacy
Config.Framework = "qbcore"    -- For QBCore
Config.Framework = "qbx"       -- For QBX
```

## Appearance Resource (QBCore / QBX)

If you are using QBCore or QBX, you must specify which appearance resource handles skin saving and loading:

```lua
Config.AppearanceResource = "illenium-appearance"   -- or "fivem-appearance" or "qb-clothing"
```

This setting is not used on ESX, which handles appearance through its own skin system.

## server.cfg

Make sure your framework and dependencies start before the barbershop:

```cfg
ensure oxmysql
ensure es_extended          # or qb-core / qbx-core
ensure illenium-appearance  # QBCore/QBX only — adapt to your appearance resource
ensure foltone_barbershop
```

## Barbershop Locations

The script comes with **7 barbershop locations** preconfigured across the map. Each location has a map blip (sprite 71) and 3–4 barber chairs. You can add, remove, or move locations in `Config.Positions` (see the Configuration page for details).

## Escrow & Editable Files

The following files are **not escrowed** and can be freely modified:

- `config.lua` — all settings
- `locales/*.lua` — translation strings
- `client/cl_editable.lua` — client-side editable logic
- `server/sv_editable.lua` — server-side editable logic
