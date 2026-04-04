---
title: "Configuration"
description: "Configuration guide for foltone_ammunation script"
script: "foltone-ammunation"
section: "Ammunation"
order: 2
version: "1.0.0"
---

# Configuration

All configuration is done in the `config.lua` file.

## General settings

```lua
Config.Locale = 'en'           -- Language (fr, en, es)
Config.PedModel = 's_m_y_ammucity_01' -- Shopkeeper ped model
```

## Map blip

```lua
Config.AmmunationBlip = {
    sprite = 110,    -- Blip icon
    color = 1,       -- Color (1 = red)
    scale = 0.8      -- Blip size
}
```

## License system

```lua
Config.LicensePrice = 5000  -- Weapon license price ($)
```

Weapons requiring a license are flagged with `RequireLicense = true` in the aisle configuration.

## Aisles and products

```lua
Config.AisleProductList = {
    {
        label = "Handguns",
        RequireLicense = true,
        items = {
            { name = "WEAPON_PISTOL", label = "Pistol", price = 2500, type = "weapon" },
            { name = "WEAPON_COMBATPISTOL", label = "Combat Pistol", price = 3500, type = "weapon" },
        }
    },
    {
        label = "Ammunition",
        RequireLicense = false,
        items = {
            { name = "ammo_pistol", label = "Pistol Ammo", price = 100, type = "item" },
        }
    },
}
```

### Product parameters

| Parameter | Type | Description |
|---|---|---|
| `name` | string | Technical weapon/item name |
| `label` | string | Display name in menu |
| `price` | number | Sale price |
| `type` | string | `"weapon"` or `"item"` |

## Store locations

```lua
Config.AmmunationsList = {
    vector4(-662.18, -935.3, 21.83, 174.89),
    vector4(810.25, -2157.6, 29.62, 0.72),
    -- Add more positions...
}
```

## Robbery settings

```lua
Config.RobberyMinPolice = 2       -- Minimum police officers online
Config.RobberyCooldown = 1800     -- Cooldown between robberies (seconds)
Config.RobberyMinAmount = 5000    -- Minimum robbery payout
Config.RobberyMaxAmount = 15000   -- Maximum robbery payout
Config.RobberyDistance = 3.0      -- Max distance before cancellation
```

> The robbery is cancelled if the player moves too far from the NPC or if the NPC dies.

## Notifications

```lua
Config.Notification = function(msg)
    -- Customize your notification system
    ESX.ShowNotification(msg)
end

Config.DisplayHelpText = function(msg)
    -- Contextual help text
    SetTextComponentFormat("STRING")
    AddTextComponentString(msg)
    DisplayHelpTextFromStringLabel(0, 0, 1, -1)
end
```

## Police alerts

During a robbery, police officers receive:
- Suspect photo (mugshot)
- Store geolocation
- Audio notification
