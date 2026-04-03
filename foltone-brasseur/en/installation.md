---
title: "Installation"
description: "Brewer script installation"
script: "foltone-brasseur"
section: "Brasseur"
order: 1
version: "2.0.0"
---

# Installation — foltone_brasseur

## Requirements

Same as Vigneron: ESX Legacy, ox_lib, oxmysql, skinchanger, esx_society. Optional: ox_inventory, ox_target, esx_billing.

## Server configuration

```ini
ensure foltone_brasseur
```

## Database

Run `foltone_brasseur.sql` to create required tables (job, grades, items, storage).

## Verification

Console: `[Foltone Brasseur] v2.0.0 chargee`
