---
title: "Usage"
description: "Vintner script usage guide"
script: "foltone-vigneron"
section: "Vigneron"
order: 3
version: "2.0.0"
---

# Usage — foltone_vigneron

## Going on duty

Press **F6** → **Toggle duty**. An announcement is sent to all players.

## Production pipeline

1. **Harvest**: Gather grapes at harvest points
2. **Transform**: Process grapes into juice/wine
3. **Sell**: Sell products (money split between player and society)

Each step uses ox_lib progress bars with animations, cancellable anytime.

## F6 Menu

Duty toggle, GPS waypoints, billing, announcements.

## Storage, Locker, Garage, Boss Menu

Standard job features. See French documentation for details.

## Editable files (escrow-excluded)

- `client/cl_editable.lua`: `OnVehicleSpawned()`, `SendBill()`
- `server/sv_editable.lua`: `OnHarvestComplete()`, `OnTransformComplete()`, `OnSellComplete()`

## Security

Rate limiting, server-side job validation, anti-cheat on sell amounts, optional Discord logs.
