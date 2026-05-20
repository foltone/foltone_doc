---
title: "Installation"
description: "Installation guide for foltone_blackmarket script"
script: "foltone-blackmarket"
section: "Blackmarket"
order: 1
version: "1.1.1"
---

# Installation

## Requirements

- **ox_lib** (required)
- **A framework** : ESX, QBCore, QBox or standalone
- **An inventory** : ox_inventory (recommended), qs-inventory, esx or qb-inventory
- **A target system** (optional but recommended) : ox_target, qb-target or qtarget

## Installation steps

### 1. Download the script

Place the `foltone_blackmarket` folder in your `resources/[foltone]/` directory.

### 2. Add to server.cfg

```cfg
ensure foltone_blackmarket
```

Make sure dependencies are started **before** this script :

```cfg
ensure ox_lib
ensure ox_inventory
ensure ox_target
ensure es_extended    # or qb-core / qbx_core
ensure foltone_blackmarket
```

### 3. Register inventory items

If you use **ox_inventory**, the items have already been added to `[OX]/ox_inventory/data/items.lua`:

- `bm_encrypted_phone` — burner phone revealing the van's location
- `bm_contact` — underground contact (optional, used with `Config.RequireContactItem`)

If you use another inventory, add these two items manually (see Configuration).

### 4. Configure the script

Edit `config.lua` to match your server (locale, framework, money, locations, items...). See the Configuration section.

### 5. Restart the server

Restart your server, or run in console :

```
refresh
ensure foltone_blackmarket
```

On startup the script displays its version. If a newer version is available, a yellow warning appears in the console.

## File structure

```
foltone_blackmarket/
├── bridge/           # Multi-framework abstraction (ESX/QB/QBox/standalone)
├── client/           # Client logic (van, ped, menu, phone, preview)
├── server/           # Server logic (spawn, transactions, version check)
├── src/              # RageUI library (in-game menu)
├── html/             # NUI menu (HTML/CSS alternative)
├── locales/          # Translations (fr / en / es)
├── config.lua        # Main configuration
├── trad.lua          # Translation system
└── fxmanifest.lua
```

## Common issues

| Issue | Solution |
|---|---|
| Interaction does not work | Check that ox_target / qb-target is started, or set `Config.TargetSystem = 'none'` |
| 3D weapons do not display | Recent GTA V build : verify `RequestWeaponAsset` works in console |
| Menu does not open | Check `Config.MenuType` (`'rageui'` or `'nui'`) |
| The van never spawns | Check `Config.SpawnLocations` is not empty |
| Encrypted phone has no effect | Verify the item is in your inventory's items list and `server.export` points to `foltone_blackmarket.useEncryptedPhone` |
