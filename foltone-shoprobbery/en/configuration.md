---
title: "Configuration"
description: "Configuration guide for the foltone_shoprobbery script"
script: "foltone-shoprobbery"
section: "Shop Robbery"
order: 2
version: "1.0.0"
---

# Configuring foltone_shoprobbery

## Configuration File

All configuration is done in `config.lua`.

## Shop Positions

```lua
Config.Shops = {
    {
        coords = vector3(25.7, -1347.3, 29.5),
        robbable = true,
        blip = true,
    },
    -- Add as many shops as needed
}
```

Each shop can be set as robbable or not.

## Robbery Settings

```lua
Config.Robbery = {
    amount = {min = 500, max = 2000},
    requiredPolice = 2,
    cooldown = 1200, -- seconds (20 minutes)
    duration = 15000, -- robbery duration in ms
}
```

| Parameter | Description |
|-----------|-------------|
| `amount` | Money range obtained from the robbery |
| `requiredPolice` | Minimum number of police officers on duty |
| `cooldown` | Wait time between two robberies of the same shop |
| `duration` | Duration of the robbery progress bar |

## Cancellation Conditions

The robbery is automatically cancelled if:
- The player moves during the robbery
- The shopkeeper NPC dies

## Shop Items

```lua
Config.ShopItems = {
    { item = "bread", label = "Bread", price = 10 },
    { item = "water", label = "Water", price = 5 },
    -- Add your items here
}
```

## Police Notifications

```lua
Config.PoliceNotification = function(source, coords)
    -- Customize notification dispatch here
    -- Includes suspect photo and geolocation
end
```

Adapt this function for your dispatch system. The notification automatically includes a suspect photo and the GPS position of the shop.
