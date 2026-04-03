---
title: "Installation"
description: "Vintner script installation"
script: "foltone-vigneron"
section: "Vigneron"
order: 1
version: "2.0.0"
---

# Installation — foltone_vigneron

## Requirements

- **ESX Legacy** — Server framework
- **ox_lib** — Notifications, inputs, progress bars
- **oxmysql** — MySQL library
- **skinchanger** — Locker / outfits
- **esx_society** — Society management

### Optional

- **ox_inventory** — Stash storage (auto-fallback to esx_addoninventory)
- **ox_target** — 3D interactions (auto-fallback to markers + E key)
- **esx_billing** — Player billing

## Server configuration

```ini
ensure oxmysql
ensure es_extended
ensure ox_lib
ensure esx_society
ensure skinchanger
ensure foltone_vigneron
```

> `foltone_vigneron` must start **after** `es_extended`, `ox_lib` and `oxmysql`.

## Database

If using **esx_addoninventory**, run `foltone_vigneron.sql`. With **ox_inventory**, stashes are created automatically.

## Verification

1. Join with a character having job `vigne`
2. Check the "Vigneron" blip on the map
3. Server console: `[Foltone Vigneron] v2.0.0 chargee`
