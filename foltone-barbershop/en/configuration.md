---
title: "Configuration"
description: "Barbershop script configuration reference"
script: "foltone-barbershop"
section: "Barbershop"
order: 2
version: "1.2.0"
---

# Configuration

All settings are located in `config.lua`.

## General

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `Config.Framework` | string | `"esx"` | Framework to use: `"esx"`, `"qbcore"`, or `"qbx"` |
| `Config.Locale` | string | `"en"` | Language: `"en"` or `"fr"` |
| `Config.AutoUpdateCheck` | boolean | `true` | At startup, check whether a new version was published and print a notice in the server console |
| `Config.UpdateCheckURL` | string | *(official GitHub)* | URL of the remote `version.json` to compare against the local version |

## Interaction

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `Config.InteractionType` | string | `"ox_target_prop"` | Interaction method (see below) |
| `Config.InteractionDistance` | number | `1.5` | Distance for drawtext / marker interaction |
| `Config.ChairModels` | table | *(see below)* | List of barber chair prop models used by target systems |

### Supported Interaction Types

| Value | Description |
|-------|-------------|
| `"drawtext"` | On-screen text prompt (framework drawtext) |
| `"ox_target"` | ox_target on chair entity |
| `"ox_target_prop"` | ox_target on chair model |
| `"qb-target"` | qb-target on chair entity |
| `"qb-target_prop"` | qb-target on chair model |
| `"qtarget"` | qtarget on chair entity |
| `"qtarget_prop"` | qtarget on chair model |
| `"interact"` | interact on chair entity |
| `"interact_prop"` | interact on chair model |
| `"marker"` | 3D marker on each chair position |

### Default Chair Models

```lua
Config.ChairModels = {
    "v_serv_bs_barbchair3",
    "v_serv_bs_barbchair5",
    "v_serv_bs_barbchair2",
    "v_serv_bs_barbchair",
    "m25_2_int_01_barber_chair",
}
```

## UI / Menu

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `Config.MenuPosition` | string | `"right"` | Menu position on screen: `"left"` or `"right"` |
| `Config.MenuStyle` | string | `"glass"` | Menu visual style: `"glass"` or `"solid"` |
| `Config.UIColors` | table | *(see below)* | Accent colors for the NUI menu |

### UI Colors

```lua
Config.UIColors = {
    accent      = "#e74c3c",
    accentLight = "#ff6b5a",
    accentDim   = "#c0392b",
}
```

These three hex values control the main accent, light accent, and dim accent throughout the menu interface.

## Pricing

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `Config.Price` | number | `75` | Price charged for a haircut |

## Barber NPC

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `Config.BarberModel` | string | `"s_f_y_hooker_01"` | Ped model spawned as the barber NPC |

## Appearance Resource

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `Config.AppearanceResource` | string | `"illenium-appearance"` | Appearance resource used to save/load skin (QBCore/QBX only): `"illenium-appearance"`, `"fivem-appearance"`, or `"qb-clothing"` |

## Barbershop Locations — `Config.Positions`

Each entry in `Config.Positions` defines one barbershop:

```lua
{
    pos = vector3(x, y, z),                           -- Center position (used for blip placement)
    blip = { sprite = 71, color = 47, scale = 0.8, label = "Barber Shop" },
    chairs = {                                        -- List of chair positions
        vector4(x, y, z, heading),
        -- ...
    },
}
```

The script ships with **7 locations**, each with 3–4 chairs. You can freely add, remove, or relocate entries.

## Marker Settings

Only used when `Config.InteractionType = "marker"`:

```lua
Config.Marker = {
    type  = 1,
    scale = vector3(0.8, 0.8, 0.3),
    color = { r = 59, g = 130, b = 246, a = 120 },
}
```

## DrawText Settings

Only used when `Config.InteractionType = "drawtext"`:

```lua
Config.DrawText = {
    label = "interact_label",   -- Locale key used for the prompt text
}
```

## Notifications

The `Notification(source, message, type)` function in `config.lua` handles server-side notifications. It automatically dispatches to the correct framework event (ESX or QBCore/QBX). You can replace it with your own notification system.
