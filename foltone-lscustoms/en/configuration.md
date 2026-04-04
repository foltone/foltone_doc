---
title: "Configuration"
description: "Configuration guide for the foltone_lscustoms script"
script: "foltone-lscustoms"
section: "LS Customs"
order: 2
version: "1.0.0"
---

# Configuring foltone_lscustoms

## Configuration File

All configuration is done in `config.lua`.

## Menu Position

```lua
Config.MenuPosition = "right" -- "left" or "right"
```

## Modification Prices

### Paint

```lua
Config.Prices.Paint = {
    primary = 500,
    secondary = 500,
    pearlescent = 750,
    wheels = 300,
}
```

### Performance Upgrades

```lua
Config.Prices.Performance = {
    engine = 2500,
    brakes = 1500,
    transmission = 2000,
    suspension = 1200,
    turbo = 5000,
}
```

### Aesthetic Modifications

```lua
Config.Prices.Aesthetic = {
    spoiler = 800,
    bumper_front = 600,
    bumper_rear = 600,
    skirts = 500,
    exhaust = 400,
    grille = 350,
    hood = 700,
    roof = 500,
    wheels = 1000,
    xenon = 300,
    plate = 200,
    horn = 150,
    windows = 400,
}
```

### Repair and Cleaning

```lua
Config.Prices.Repair = 500
Config.Prices.Clean = 100
```

## NPC Towing Missions

```lua
Config.Towing = {
    reward = {min = 300, max = 800},
    cooldown = 300, -- seconds
    maxDistance = 500.0, -- max mission distance
}
```

## Invoice System

```lua
Config.Invoice = {
    enabled = true,
    maxAmount = 50000,
}
```

Allows players to send invoices to other players for completed work.
