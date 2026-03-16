---
title: "Usage"
description: "Usage guide for Foltone Garage"
script: "foltone-garage"
section: "Foltone Garage"
order: 3
version: "2.0.0"
---

# Usage — foltone_garage

## Overview

Foltone Garage is a complete garage system for FiveM. It allows players to store and retrieve their vehicles, manage impounded vehicles, and assign custom labels. The script supports cars, boats, planes and helicopters, with a dynamic-pricing pound system.

## Accessing a garage

The interface opens by interacting with the garage manager PED placed at the coordinates configured in `config_garage.lua`.

The interaction method depends on `Config.InteractionType`:

| Mode | How to interact |
|------|----------------|
| `ox_target` / `qb-target` / `interact` | Aim at the PED with the target cursor |
| `drawtext` | Approach the PED and press **E** |
| `marker` | Enter the marker and press **E** |

## NUI mode (HTML panel)

The NUI panel has **4 tabs**:

### Vehicles tab

Displays all vehicles stored in the current garage.

For each vehicle:
- **Model** and **label** (if set)
- **License plate**
- **Status** (available, out, impounded)
- **Retrieve button** — spawns the vehicle at the configured spawn position

> Only vehicles matching the garage type are displayed (cars, boats, planes or helicopters).

### Store tab

Allows storing the vehicle currently being driven.

1. Drive the vehicle close to the storage zone (`storeVeh`)
2. Open the garage interface
3. Click **Store**
4. The vehicle disappears and is marked as stored in the DB

> The storage distance is configurable per garage (`distanceStore`).

#### Service vehicles

For job garages with `serviceVehicles` defined, the Store tab also lists service vehicles that can be spawned directly.

### Pound tab

Displays the player's vehicles currently in the pound.

For each impounded vehicle:
- **Plate** and **model**
- **Retrieval price** calculated dynamically based on elapsed time
- **Retrieve button** — deducts the amount and spawns the vehicle

#### Price calculation

```
Price = basePrice + (hours_elapsed × pricePerHour)
Price = max(minPrice, min(maxPrice, Price))
```

Example with default settings (basePrice 500, pricePerHour 100):
- After 2h: 500 + 200 = **$700**
- After 10h: 500 + 1000 = **$1500** (capped at maxPrice if exceeded)

### Label tab

> Available in `Config.MenuType = "nui"` mode only.

Allows assigning a custom name to one of the player's vehicles.

1. Select a vehicle from the list
2. Type the desired label (30 characters maximum)
3. Click **Save**

The label replaces the model name in the Vehicles tab.

---

## RageUI mode (classic menu)

The RageUI mode provides **3 sub-menus** accessible from a main menu:

| Sub-menu | NUI equivalent |
|----------|---------------|
| Vehicles | Vehicles tab |
| Store | Store tab |
| Pound | Pound tab |

> Custom vehicle labels are not available in RageUI mode.

---

## Job garages

Garages with `job`, `job2` or `annyJob` defined are restricted to players with the matching job.

| Parameter | Behavior |
|-----------|---------|
| `job = "ambulance"` | Exclusive access for players with the `ambulance` job |
| `job2 = "famillies"` | Access via the `famillies` gang / secondary job |
| `annyJob = "police"` | Access for any grade of the `police` job |

Service vehicles (if configured) are only accessible to job members.

---

## Pound system

Vehicles can be impounded manually by an administrator or via other compatible scripts.

A player can retrieve their vehicle from any pound of the correct type (car, boat, plane or helicopter).

The price automatically increases over time. Once paid, the vehicle is made available and spawns at the pound's configured spawn position.

---

## Vehicle types

| Type | Description |
|------|-------------|
| `car` | Cars, motorcycles and ground vehicles |
| `boat` | Boats and watercraft |
| `plane` | Planes and jets |
| `heli` | Helicopters |

Each type has its own list of garages and pounds configured in `config_garage.lua`.
