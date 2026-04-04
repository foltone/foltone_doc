---
title: "Usage"
description: "Usage guide for the foltone_vehicleitem script"
script: "foltone-vehicleitem"
section: "Vehicle Item"
order: 3
version: "1.0.0"
---

# Usage

## Overview

The Vehicle Item script lets players purchase vehicles as inventory items. Players can then spawn these vehicles from their inventory and store them back at any time.

## Purchasing a vehicle

1. Go to the vehicle shop (marked by a blip on the map if enabled).
2. Interact with the vendor NPC to open the purchase menu (RageUI).
3. Browse the list of available vehicles with their prices.
4. Select the desired vehicle.
5. If you have enough money, the vehicle is added to your inventory as an item.

## Using a vehicle

### Spawning a vehicle

1. Open your inventory.
2. Use the vehicle item (e.g., "BMX").
3. The vehicle spawns near your character.
4. The item is removed from your inventory.

### Storing a vehicle

1. Approach your spawned vehicle.
2. Use the interaction to store the vehicle.
3. The vehicle disappears from the world and returns to your inventory as an item.

## Typical use cases

### Bikes and small vehicles

The system is ideal for bikes (BMX, Cruiser, Scorcher) that players want to carry around easily.

### Temporary vehicles

Allows giving vehicles as rewards in the form of tradeable items between players.

### Player trading

Vehicle items can be traded or sold between players like any other inventory item.

## Tips

- Make sure you have enough inventory space before purchasing.
- Only one vehicle can be spawned at a time per item.
- If you disconnect with a spawned vehicle, it will be deleted. Remember to store it first.
- Vehicle items are compatible with standard drop and trade systems.
