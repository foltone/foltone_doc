---
title: "Usage"
description: "Taxi script usage guide"
script: "foltone-taxi"
section: "Taxi"
order: 3
version: "2.0.0"
---

# Usage — foltone_taxi

## Mission system

1. **Activate**: F6 menu → Toggle service
2. **Wait**: Drive a taxi, a mission spawns after 10-20 seconds
3. **Pickup**: NPC appears at a pickup point (blip on map)
4. **Transport**: NPC enters vehicle, destination blip appears
5. **Dropoff**: Stop near destination (speed < 3 km/h), NPC exits
6. **Payment**: Distance-based payment, minus damage penalty if applicable

## Exports

```lua
exports["foltone_taxi"]:startStopService()
exports["foltone_taxi"]:cancelMission()
```

## Security

Rate limiting, $5000 cap per ride (anti-cheat), server-side job validation.
