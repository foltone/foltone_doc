---
title: "Configuration"
description: "Configuration guide for the foltone_unicornjob script"
script: "foltone-unicornjob"
section: "Unicorn Job"
order: 2
version: "1.0.0"
---

# Configuration

All configurable settings are located in the `shared/` folder.

## General settings

### Job name

```lua
Config.JobName = 'unicorn'
Config.SocietyName = 'society_unicorn'
```

### Map blip

```lua
Config.Blip = {
    enabled = true,
    coords = vector3(x, y, z),
    sprite = 93,
    scale = 0.8,
    color = 27,
    label = "Unicorn"
}
```

## Bar service

Configure the items available at the bar:

```lua
Config.BarItems = {
    { item = 'beer', label = 'Beer', price = 10 },
    { item = 'wine', label = 'Wine', price = 15 },
    { item = 'cocktail', label = 'Cocktail', price = 25 },
    { item = 'whiskey', label = 'Whiskey', price = 30 },
    { item = 'water', label = 'Water', price = 5 }
}
```

Each item must exist in your database `items` table.

## Farming system

Configure farming points for ingredients:

```lua
Config.FarmingPoints = {
    {
        coords = vector3(x, y, z),
        item = 'hops',
        label = 'Hops',
        amount = 1,
        time = 5000,
        animation = { dict = "anim@dict", name = "anim_name" }
    },
    {
        coords = vector3(x, y, z),
        item = 'grape',
        label = 'Grape',
        amount = 1,
        time = 5000
    }
}
```

## Boss menu

```lua
Config.BossMenu = {
    coords = vector3(x, y, z),
    grade = 'boss'
}
```

Boss menu features:
- Employee management (hire, fire, promote)
- Salary management per grade
- Outfit management per grade
- Society storage and bank account

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
        { model = 'speedo', label = 'Speedo', grade = 0 }
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
    blip = true,
    farming = true,
    barService = true
}
```
