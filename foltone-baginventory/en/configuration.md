---
title: "Configuration"
description: "Configuration guide for foltone_baginventory script"
script: "foltone-baginventory"
section: "Bag Inventory"
order: 2
version: "1.0.0"
---

# Configuration

All configuration is done in the `config.lua` file.

## Bag types

```lua
Config.BagTypes = {
    ['bag_small'] = {
        label = "Small Bag",
        model = 'prop_cs_heist_bag_01',
        weight = 10,       -- Maximum content weight (kg)
        slots = 5,         -- Number of slots
    },
    ['bag_medium'] = {
        label = "Medium Bag",
        model = 'prop_poly_bag_01',
        weight = 25,
        slots = 10,
    },
    ['bag_large'] = {
        label = "Large Bag",
        model = 'prop_michael_backpack',
        weight = 50,
        slots = 20,
    },
}
```

### Bag parameters

| Parameter | Type | Description |
|---|---|---|
| `label` | string | Display name |
| `model` | string | 3D model for ground placement |
| `weight` | number | Maximum weight capacity |
| `slots` | number | Number of available slots |

## Death behavior

```lua
Config.DropOnDeath = true    -- Bags drop on the ground when the player dies
Config.DropAllBags = true    -- Drop all bags (true) or only the equipped one (false)
```

## Ground placement

```lua
Config.PlaceDistance = 2.0   -- Bag placement distance
Config.PickupDistance = 2.0  -- Distance to pick up a bag
```

## Notifications

```lua
Config.Notification = function(msg)
    ESX.ShowNotification(msg)
end
```

## General settings

```lua
Config.Locale = 'en'              -- Language
Config.FoldBagItem = true         -- Allow folding the bag to store in inventory
Config.MaxBagsPerPlayer = 3       -- Max bags per player
```
