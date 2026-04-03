---
title: "Configuración"
description: "Configuración del script Taxi"
script: "foltone-taxi"
section: "Taxi"
order: 2
version: "2.0.0"
---

# Configuración — foltone_taxi

## Sistema de misiones

```lua
Config.Missions = {
    timeToFind = { 10000, 20000 },
    pricePerMeter = { 0.3, 0.5 },
    percentForSociety = 0.30,
    requiredDamageToPenalty = 50,
    vehicleDamagePenalty = { 100, 200 },
    usePredefinedPositions = true,
}
```

## Exports

```lua
exports["foltone_taxi"]:startStopService()
exports["foltone_taxi"]:cancelMission()
```
