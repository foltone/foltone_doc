---
title: "Configuration"
description: "Configuration guide for the foltone_territories script"
script: "foltone-territories"
section: "Territories"
order: 2
version: "1.0.0"
---

# Configuring foltone_territories

## Configuration File

All configuration is done in `config.lua`.

## Zone Definitions

```lua
Config.Zones = {
    {
        name = "Grove Street",
        position = vector3(95.0, -1960.0, 21.0),
        width = 200.0,
        height = 200.0,
        rotation = 0.0,
        capturePoints = 100, -- points needed to capture
    },
    -- Add as many zones as needed
}
```

| Parameter | Description |
|-----------|-------------|
| `name` | Display name of the zone |
| `position` | Center coordinates of the zone |
| `width` | Zone width |
| `height` | Zone height |
| `rotation` | Zone rotation in degrees |
| `capturePoints` | Number of points needed to capture the zone |

## Drug List

```lua
Config.Drugs = {
    {
        item = "weed",
        label = "Weed",
        price = 50,
        capturePoints = 5,
        acceptRate = 0.6, -- 60% chance to accept
        rejectRate = 0.3, -- 30% chance to reject
        -- remaining 10% = call police
    },
    {
        item = "coke",
        label = "Cocaine",
        price = 120,
        capturePoints = 10,
        acceptRate = 0.4,
        rejectRate = 0.4,
    },
}
```

| Parameter | Description |
|-----------|-------------|
| `item` | Item name in inventory |
| `price` | NPC sale price |
| `capturePoints` | Capture points earned per sale |
| `acceptRate` | Probability the NPC accepts |
| `rejectRate` | Probability the NPC refuses |

The remaining probability (1 - acceptRate - rejectRate) is the chance the NPC calls the police.

## Police Jobs

```lua
Config.PoliceJobs = {"police", "fbi", "sheriff"}
```

List of jobs considered law enforcement for alerts.

## Blacklisted Peds

```lua
Config.BlacklistedPeds = {
    "s_m_y_cop_01",
    "s_f_y_cop_01",
    -- NPCs you cannot sell to
}
```

## Gang Jobs

```lua
Config.GangJobs = {"ballas", "vagos", "families", "lost"}
```

Only players with one of these jobs can participate in the territory system.
