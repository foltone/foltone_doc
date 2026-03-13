---
title: "Configuration"
description: "Props Storage script configuration guide"
script: "foltone-props-storage"
section: "foltone_props_storage"
order: 2
version: "1.0.0"
---

# Configuration — foltone_props_storage

All configuration is done in `config.lua` at the root of the script.

## Language

```lua
Config.Locale = "fr" -- "fr" or "en"
```

Translations are in the `locales/` folder. You can add your own languages by creating a new file (e.g., `locales/de.lua`).

## Inventory

```lua
Config.useOxInventory = GetResourceState("ox_inventory") ~= "missing"
```

The script automatically detects if **ox_inventory** is installed:
- **With ox_inventory**: uses the native stash system + ox_target for interaction
- **Without ox_inventory**: uses the built-in RageUI menu + E key to interact

## Database Saving

```lua
Config.saveToDBWithInterval = true
Config.saveToDBInterval = 60 * 1000 -- 1 minute
```

| Option | Description |
|--------|-------------|
| `saveToDBWithInterval = true` | Periodic saving (recommended for high player count servers) |
| `saveToDBWithInterval = false` | Save on every action (deposit/withdraw) |

> **Note**: When `useOxInventory` is enabled, `saveToDBWithInterval` is forced to `true`.

## Interaction Distance

```lua
Config.distance = 2.5
```

Maximum distance (in meters) at which a player can interact with a storage.

## Forbidden PIN Codes

```lua
Config.forbidenPIN = {
    0000, 1111, 2222, 3333, 4444,
    5555, 6666, 7777, 8888, 9999,
    1234,
}
```

Players won't be able to use these PIN codes. The PIN must be at least 4 digits.

## Storage Types

```lua
Config.propsList = {
    ["p_v_43_safe_s"] = {
        capacity = 50000,      -- Weight capacity
        itemName = "big_safe", -- Required ESX item name
        itemLabel = "Large Safe",
    },
    ["prop_ld_int_safe_01"] = {
        capacity = 30000,
        itemName = "safe",
        itemLabel = "Safe",
    },
}
```

You can add as many storage types as you want. Each entry uses the **GTA model name** as the key.

### Adding a New Storage Type

1. Find the GTA V prop model name you want
2. Add an entry in `propsList`:

```lua
["model_name"] = {
    capacity = 40000,
    itemName = "my_safe",
    itemLabel = "My Custom Safe",
},
```

3. Don't forget to add the corresponding item in your ESX database

## Boss Grades

```lua
Config.bossGrades = {
    ["boss"] = true,
    ["underboss"] = true,
    ["capodecina"] = true,
    ["consigliere"] = true,
    ["don"] = true,
}
```

Job grades that have special (boss) permissions.

## Weapon Weights

```lua
Config.defaultWeaponWeight = 3

Config.weaponWeight = {
    ["WEAPON_KNIFE"] = 2,
    ["WEAPON_PISTOL"] = 4,
    ["WEAPON_ASSAULTRIFLE"] = 8,
    ["WEAPON_RPG"] = 10,
    -- ... see config.lua for the full list
}
```

Unlisted weapons use `defaultWeaponWeight`. Over 40 weapons are preconfigured.

## Notifications

```lua
Config.Notification = function(text)
    SetNotificationTextEntry("STRING")
    AddTextComponentString(text)
    DrawNotification(false, true)
end
```

Replace this function with your preferred notification system (e.g., okokNotify, ox_lib notify, etc.).

## Help Text

```lua
Config.DisplayHelpText = function(text)
    SetTextComponentFormat("STRING")
    AddTextComponentString(text)
    DisplayHelpTextFromStringLabel(0, 0, 1, -1)
end
```

Customize the help text display (shown when a player is near a storage).

## Discord Webhook

In `server/sv_editable.lua`, configure your Discord webhook for logging:

```lua
PerformHttpRequest("https://discord.com/api/webhooks/YOUR_ID/YOUR_TOKEN", ...)
```

All actions (placement, opening, deposit, withdraw, deletion) are logged to Discord.
