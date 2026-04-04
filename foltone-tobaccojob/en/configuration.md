---
title: "Configuration"
description: "Configuration guide for the foltone_tobaccojob script"
script: "foltone-tobaccojob"
section: "Tobacco Job"
order: 2
version: "1.0.0"
---

# Configuration

All configurable settings are located in the `shared/` folder.

## General settings

### Job name

```lua
Config.JobName = 'tobaccojob'
Config.SocietyName = 'society_tobaccojob'
```

- `JobName`: must match the job name in the database.
- `SocietyName`: society account name used by esx_addonaccount.

### Map blip

```lua
Config.Blip = {
    enabled = true,
    coords = vector3(x, y, z),
    sprite = 365,
    scale = 0.8,
    color = 2,
    label = "Tobacco"
}
```

## Production pipeline

The script follows a 3-step pipeline: **Harvest -> Process -> Sell**.

### Harvest

```lua
Config.Harvest = {
    coords = vector3(x, y, z),
    item = 'tobacco_leaf',
    amount = 1,
    time = 5000, -- milliseconds
    animation = { dict = "anim@dict", name = "anim_name" }
}
```

### Processing

```lua
Config.Processing = {
    coords = vector3(x, y, z),
    recipes = {
        {
            input = { item = 'tobacco_leaf', amount = 3 },
            output = { item = 'cigarettes', amount = 1 },
            time = 8000
        }
    }
}
```

### Sell

```lua
Config.Sell = {
    coords = vector3(x, y, z),
    items = {
        { item = 'cigarettes', price = 50 }
    }
}
```

## Boss menu

```lua
Config.BossMenu = {
    coords = vector3(x, y, z),
    grade = 'boss' -- minimum grade to access the menu
}
```

The boss menu allows:
- Employee management (hire, fire, promote)
- Salary management per grade
- Outfit management per grade
- Access to society storage and bank account

## Storage and locker

```lua
Config.Storage = {
    coords = vector3(x, y, z),
    slots = 50,
    weight = 100000
}

Config.Locker = {
    coords = vector3(x, y, z)
}
```

## Garage

```lua
Config.Garage = {
    coords = vector3(x, y, z),
    spawnPoint = vector4(x, y, z, heading),
    vehicles = {
        { model = 'mule', label = 'Mule', grade = 0 }
    }
}
```

## Features toggle

```lua
Config.Features = {
    garage = true,
    locker = true,
    storage = true,
    bossMenu = true,
    blip = true
}
```

Disable any feature you don't need by setting its value to `false`.
