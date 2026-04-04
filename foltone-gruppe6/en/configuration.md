---
title: "Configuration"
description: "Configuration guide for the foltone_gruppe6 script"
script: "foltone-gruppe6"
section: "Gruppe6"
order: 2
version: "1.0.0"
---

# Configuring foltone_gruppe6

## Configuration File

All configuration is done in `config.lua` at the root of the script.

## Job Settings

### Job Grades

```lua
Config.JobGrades = {
    { name = "recruit", label = "Recruit", salary = 200 },
    { name = "agent", label = "Agent", salary = 350 },
    { name = "leader", label = "Team Leader", salary = 500 },
    { name = "boss", label = "Boss", salary = 700 },
}
```

### Mission Rewards

```lua
Config.MissionReward = {min = 500, max = 1500}
```

Set the reward range for each completed mission.

### Outfits

```lua
Config.Outfits = {
    male = { ... },
    female = { ... },
}
```

Configure outfit components (tshirt, torso, pants, shoes, etc.) for each gender.

### Vehicle

```lua
Config.VehicleModel = "stockade"
```

Armored vehicle model used for missions.

## Robbery Settings

### Police Requirement

```lua
Config.Robbery = {
    requiredPolice = 2,
    cooldown = 1800, -- in seconds (30 minutes)
    explosiveItem = "explosive", -- required item
    rewardMin = 5000,
    rewardMax = 15000,
}
```

| Parameter | Description |
|-----------|-------------|
| `requiredPolice` | Minimum number of police officers on duty |
| `cooldown` | Wait time between two robberies (seconds) |
| `explosiveItem` | Name of the explosive item required in inventory |
| `rewardMin` / `rewardMax` | Robbery reward range |

## Translation

Displayable texts are located in `locales/`. Add or modify files to support other languages.
