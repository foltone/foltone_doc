---
title: "Configuration"
description: "Configuration guide for the foltone_vehicleitem script"
script: "foltone-vehicleitem"
section: "Vehicle Item"
order: 2
version: "1.0.0"
---

# Configuration

All configurable settings are located in the `shared/` folder.

## Vehicle list

Configure the vehicles available for purchase:

```lua
Config.Vehicles = {
    {
        model = 'bmx',
        label = 'BMX',
        item = 'bmx_item',
        price = 500
    },
    {
        model = 'cruiser',
        label = 'Cruiser',
        item = 'cruiser_item',
        price = 800
    },
    {
        model = 'scorcher',
        label = 'Scorcher',
        item = 'scorcher_item',
        price = 1000
    }
}
```

### Vehicle parameters

| Parameter | Type   | Description                                    |
|-----------|--------|------------------------------------------------|
| `model`   | string | GTA model name (spawn name)                    |
| `label`   | string | Display name in the menu                       |
| `item`    | string | Item name in the database                      |
| `price`   | number | Purchase price in dollars                      |

Each `item` must match an entry in your database `items` table.

## Shop position

```lua
Config.Shop = {
    coords = vector3(x, y, z),
    heading = 0.0,
    blip = {
        enabled = true,
        sprite = 226,
        scale = 0.8,
        color = 3,
        label = "Vehicles"
    },
    ped = {
        model = 's_m_y_shop_mid',
        heading = 0.0
    }
}
```

## Spawn settings

```lua
Config.Spawn = {
    offset = vector3(2.0, 0.0, 0.0), -- offset from the player
    deleteOnStore = true -- delete the vehicle when stored
}
```

### Spawn options

- `offset`: relative position from the player where the vehicle spawns.
- `deleteOnStore`: if `true`, the vehicle is deleted from the world when the player stores it (converts back to item).

## Miscellaneous settings

```lua
Config.UseRageUI = true -- use RageUI for menus
Config.Locale = 'en' -- default language
```
