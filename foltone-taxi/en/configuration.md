---
title: "Configuration"
description: "Taxi script configuration"
script: "foltone-taxi"
section: "Taxi"
order: 2
version: "2.0.0"
---

# Configuration — foltone_taxi

## Mission system

```lua
Config.Missions = {
    timeToFind = { 10000, 20000 },
    pricePerMeter = { 0.3, 0.5 },
    percentForSociety = 0.30,
    requiredDamageToPenalty = 50,
    vehicleDamagePenalty = { 100, 200 },
    usePredefinedPositions = true,
    pedList = { ... },
    positionList = { ... },
}
```

## Exports

```lua
exports["foltone_taxi"]:startStopService()  -- Toggle service
exports["foltone_taxi"]:cancelMission()     -- Cancel current mission
```
