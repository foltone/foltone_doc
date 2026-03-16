---
title: "Configuration"
description: "Ultra HUD configuration reference"
script: "foltone-ultra-hud"
section: "Ultra HUD"
order: 2
version: "1.0.0"
---

# Configuration — foltone_ultra_hud

All settings are in `config.lua`. Most of these can be overridden at runtime via the admin panel.

## Locale

```lua
Config.locale = "en" -- "en", "fr", etc.
```

Translation files are in `locales/en.lua`, `locales/fr.lua`. You can add your own language by creating a new file (e.g. `locales/de.lua`).

## General

| Option | Type | Default | Description |
|---|---|---|---|
| `disableMinimap` | boolean | `false` | Hide the GTA minimap entirely |
| `disableMinimapHealtharmour` | boolean | `true` | Hide the default GTA health/armour bars on the minimap |
| `disableNoMoney` | boolean | `true` | Hide money fields when balance is 0 |
| `disableArmour` | boolean | `true` | Auto-hide armour bar when value is 0 |
| `disableApnea` | boolean | `true` | Auto-hide apnea bar when full (not underwater) |
| `disableStamina` | boolean | `true` | Auto-hide stamina bar when full (not sprinting) |

## Visibility

Each HUD element can be individually toggled. These serve as defaults and can be overridden via the admin panel.

| Option | Type | Default | Description |
|---|---|---|---|
| `id` | boolean | `true` | Show player server ID |
| `job` | boolean | `true` | Show job name and grade |
| `job2` | boolean | `false` | Show second job / gang (ESX: job2, QB: gang) |
| `money` | boolean | `true` | Show cash (ESX: money, QB: cash) |
| `bank` | boolean | `true` | Show bank balance |
| `black_money` | boolean | `true` | Show dirty money (ESX: black_money, QB: crypto) |
| `position` | boolean | `true` | Show street name |
| `health` | boolean | `true` | Show health bar |
| `armour` | boolean | `true` | Show armour bar |
| `hunger` | boolean | `true` | Show hunger bar |
| `thirst` | boolean | `true` | Show thirst bar |
| `stamina` | boolean | `true` | Show stamina bar |
| `apnea` | boolean | `true` | Show apnea bar |
| `speedometer` | boolean | `true` | Show speedometer when in vehicle |

## Display

| Option | Type | Default | Description |
|---|---|---|---|
| `type_needs_display` | string | `"bar"` | Status display mode: `"bar"`, `"circle"`, `"square"`, `"hexagon"`, `"text"` |
| `shape_fill_mode` | string | `"stroke"` | Shape fill style: `"stroke"` (outline progress) or `"fill"` (bottom-to-top solid fill) |
| `metric` | string | `"kmh"` | Speed unit: `"kmh"` or `"mph"` |

## Default Colors

Colors are defined as RGBA arrays `{R, G, B, A}` with values from 0 to 255.

```lua
Config.colorText    = {255, 255, 255, 255}  -- White
Config.healthColor  = {53, 154, 71, 255}    -- Green
Config.armourColor  = {51, 131, 236, 255}   -- Blue
Config.hungerColor  = {245, 166, 35, 255}   -- Orange
Config.thirstColor  = {0, 168, 255, 255}    -- Cyan
Config.staminaColor = {245, 220, 63, 255}   -- Yellow
Config.apneaColor   = {123, 153, 229, 255}  -- Light blue
Config.fuelColor    = {255, 0, 0, 255}      -- Red
```

> All colors can be changed via the admin panel color pickers.

## Notifications

These serve as defaults. They can be overridden via the admin panel.

| Option | Type | Default | Description |
|---|---|---|---|
| `notifPosition` | string | `"top-center"` | Notification position on screen |
| `notifWidth` | number | `25` | Width in `vw` units (viewport width) |
| `notifScale` | number | `1.0` | Scale multiplier (0.5 to 2.0) |

Available positions: `"top-left"`, `"top-center"`, `"top-right"`, `"bottom-left"`, `"bottom-center"`, `"bottom-right"`

> When set to `bottom-left`, notifications automatically position above the GTA minimap and match its width (15vw).

## Admin Menu

| Option | Type | Default | Description |
|---|---|---|---|
| `adminCommand` | string | `"hudadmin"` | Chat command to open the admin panel |
| `adminGroups` | table | `{"admin", "superadmin", "god"}` | Framework groups allowed to access the panel |

For standalone, you can define a custom admin check:

```lua
Config.customAdminCheck = function(src)
    return IsPlayerAceAllowed(src, "admin")
end
```

Admin permission is checked in this order:
1. Framework group check (ESX group, QBCore permission)
2. ACE permission fallback (`command.<adminCommand>`)
