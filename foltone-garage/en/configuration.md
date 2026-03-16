---
title: "Configuration"
description: "Configuration guide for Foltone Garage"
script: "foltone-garage"
section: "Foltone Garage"
order: 2
version: "2.0.0"
---

# Configuration — foltone_garage

Configuration is split across two files: `Config.lua` (general options) and `config_garage.lua` (garages, pounds, service vehicles).

## Config.lua — General options

### Framework

```lua
Config.Framework = "esx" -- "esx", "qbcore" or "qbx"
```

| Value | Framework | Required dependencies |
|-------|-----------|----------------------|
| `"esx"` | ESX Legacy | `es_extended`, `oxmysql` |
| `"qbcore"` | QBCore | `qb-core`, `oxmysql` |
| `"qbx"` | QBX | `qbx_core`, `oxmysql` |

### Locale

```lua
Config.Locale = "en" -- "en" or "fr"
```

Translations are located in `locales/en.lua` and `locales/fr.lua`. You can add your own language by creating a new file.

### Menu type

```lua
Config.MenuType = "nui" -- "nui" or "rageui"
```

| Mode | Description |
|------|-------------|
| `"nui"` | Modern HTML panel with 4 tabs (vehicles, store, pound, label) |
| `"rageui"` | Classic RageUI menu with 3 sub-menus (vehicles, store, pound) |

> The `"rageui"` mode does not support custom vehicle labels.

### Interaction type

```lua
Config.InteractionType = "ox_target" -- 5 options available
```

| Mode | Description | Dependency |
|------|-------------|------------|
| `"ox_target"` | 3D target via ox_target | `ox_target` |
| `"qb-target"` | 3D target via qb-target | `qb-target` |
| `"interact"` | 3D target via interact | `interact` |
| `"drawtext"` | Help text on screen with E key | None |
| `"marker"` | Floor marker with E key | None |

### Interaction distance

```lua
Config.InteractionDistance = 2.5
```

Distance in meters to trigger interaction (drawtext and marker modes only).

### Draw text (drawtext mode)

```lua
Config.DrawText = {
    label = "interact_label", -- locale key
}
```

### Marker (marker mode)

```lua
Config.Marker = {
    type = 1,
    scale = vector3(1.0, 1.0, 0.5),
    color = { r = 59, g = 130, b = 246, a = 120 },
}
```

| Parameter | Description |
|-----------|-------------|
| `type` | GTA marker type (1 = cylinder) |
| `scale` | Marker dimensions |
| `color` | RGBA color of the marker |

### PED

```lua
Config.Ped = {
    model = "a_m_y_business_03",
    scenario = "WORLD_HUMAN_STAND_IMPATIENT",
}
```

| Parameter | Description |
|-----------|-------------|
| `model` | Garage manager PED model |
| `scenario` | PED animation (native GTA scenario) |

### Blip

```lua
Config.Blip = {
    enabled = true,
    sprite = 357,
    color = 3,
    scale = 0.7,
}
```

| Parameter | Description |
|-----------|-------------|
| `enabled` | Enable/disable map blips |
| `sprite` | GTA blip sprite ID |
| `color` | GTA blip color ID |
| `scale` | Blip size |

### Pound system

```lua
Config.Pound = {
    basePrice = 500,
    pricePerHour = 100,
    maxPrice = 5000,
    minPrice = 200,
}
```

| Parameter | Description |
|-----------|-------------|
| `basePrice` | Base price to retrieve an impounded vehicle |
| `pricePerHour` | Additional amount per hour spent in the pound |
| `maxPrice` | Maximum price cap for the pound fee |
| `minPrice` | Minimum guaranteed price (never goes below this) |

> The price is calculated dynamically based on the time elapsed since impoundment.

### Custom label

```lua
Config.Label = {
    maxLength = 30,
}
```

| Parameter | Description |
|-----------|-------------|
| `maxLength` | Maximum allowed length for a vehicle label |

---

## config_garage.lua — Garages and pounds

### Default garage names

```lua
ConfigGarage.defaultGarageCarName = "garage"
ConfigGarage.defaultGarageBoatName = "garage_bateau1"
ConfigGarage.defaultGaragePlaneName = "garage_plane1"
ConfigGarage.defaultGarageHeliName = "garage_heli1"
```

These names correspond to the garages where vehicles will be placed when stored from a garage with `saveGarage = false`.

### Garage entry structure

```lua
{
    garageName = "garage",           -- unique identifier (lowercase, no spaces)
    garageLabel = "Downtown Garage", -- label shown in the menu
    saveGarage = true,               -- save vehicles to this garage in DB
    job = nil,                       -- required job (exclusive access for this job)
    job2 = nil,                      -- secondary job (gang / alternative job)
    annyJob = nil,                   -- restrict access to ANY grade of this job
    -- maxVehicles = 10,             -- vehicle limit (optional, comment out for unlimited)
    distanceStore = 25.0,            -- storage radius in meters
    positionMenu = vector3(x, y, z), -- PED / interaction position
    spawnVehPositions = {
        vector4(x, y, z, heading),   -- vehicle spawn positions
    },
    storeVeh = vector3(x, y, z),     -- vehicle storage zone
}
```

| Parameter | Description |
|-----------|-------------|
| `garageName` | Unique garage identifier — must be unique if `saveGarage = true` |
| `garageLabel` | Name shown in the interface |
| `saveGarage` | If `true`, vehicles are associated with this garage in the DB |
| `job` | If set, only players with this job can access the garage |
| `job2` | Secondary job (useful for gangs or job duplicates) |
| `annyJob` | Restricts access to any grade of this job (police, ambulance...) |
| `maxVehicles` | Max number of vehicles (optional — comment out for unlimited) |
| `distanceStore` | Maximum distance to store a vehicle from `storeVeh` |
| `positionMenu` | PED / interaction point coordinates |
| `spawnVehPositions` | Array of spawn positions (heading included) |
| `storeVeh` | Vehicle storage point |

### Service vehicles

For job garages, you can define service vehicles accessible from the **Store** tab (or the corresponding sub-menu in RageUI):

```lua
serviceVehicles = {
    { model = "police",  label = "Police Cruiser" },
    { model = "police2", label = "Police Buffalo" },
},
```

> Service vehicles are only available to players with the required job. They are not saved to the database.

### Custom blip color per garage

```lua
blipColor = 38,
color = {r = 20, g = 100, b = 80},
```

| Parameter | Description |
|-----------|-------------|
| `blipColor` | GTA blip color for this specific garage |
| `color` | RGB color of the indicator in the NUI interface |

### Vehicle types

Vehicles are organized into 4 categories:

| Key | Description |
|-----|-------------|
| `"car"` | Cars and motorcycles |
| `"boat"` | Boats |
| `"plane"` | Planes |
| `"heli"` | Helicopters |

Each type can be enabled or disabled:

```lua
["car"] = {
    enable = true,
    positionGarageList = { ... },
},
```

### Adding a garage

Add an entry to the `positionGarageList` array of the desired type:

```lua
{
    garageName = "my_garage",
    garageLabel = "My New Garage",
    saveGarage = true,
    job = nil,
    job2 = nil,
    annyJob = nil,
    distanceStore = 25.0,
    positionMenu = vector3(x, y, z),
    spawnVehPositions = {
        vector4(x, y, z, 0.0),
    },
    storeVeh = vector3(x, y, z)
},
```

---

## Pounds (poundList)

```lua
ConfigGarage.poundList = {
    ["car"] = {
        ["pound_car_1"] = {
            label = "Davis Pound",
            positionMenu = vector3(x, y, z),
            spawnVehPositions = { vector4(x, y, z, heading) },
        },
    },
    ["boat"] = { ... },
    ["plane"] = { ... },
    ["heli"] = { ... },
}
```

| Parameter | Description |
|-----------|-------------|
| `label` | Pound name shown in the interface |
| `positionMenu` | PED / interaction point of the pound |
| `spawnVehPositions` | Spawn positions for retrieved vehicles |

### Adding a pound

Add an entry to the desired vehicle type array:

```lua
["pound_car_3"] = {
    label = "North Pound",
    positionMenu = vector3(x, y, z),
    spawnVehPositions = { vector4(x, y, z, 0.0) },
},
```

> The key must be unique per vehicle type (e.g. `"pound_car_3"`, `"pound_boat_2"`).
