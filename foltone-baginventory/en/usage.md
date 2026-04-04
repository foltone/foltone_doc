---
title: "Usage"
description: "Usage guide for foltone_baginventory script"
script: "foltone-baginventory"
section: "Bag Inventory"
order: 3
version: "1.0.0"
---

# Usage

## Overview

The bag system allows players to carry additional items in bags that can be placed on the ground, filled, and picked up.

## Using a bag

### Deploy a bag

1. Open your inventory and use a bag item (e.g., "Small Bag").
2. The bag is deployed and appears on your back or in your hands.
3. You can now store items inside it.

### Open the bag menu

1. Press the interaction key while the bag is equipped.
2. The RageUI menu shows the bag contents.
3. You can add or remove items and weapons.

### Place a bag on the ground

1. Open the bag menu.
2. Select the "Place on ground" option.
3. The bag appears on the ground at your position as a 3D object.
4. Other players can interact with the placed bag.

### Pick up a bag

1. Approach a bag placed on the ground.
2. Press the interaction key.
3. The bag and its contents are added to your inventory.

### Fold a bag

If enabled in the configuration:

1. Open the bag menu.
2. Select "Fold bag".
3. The bag is stored in your inventory as a regular item.

## Death behavior

If `Config.DropOnDeath` is enabled:

- All your bags (or only the equipped one) drop on the ground when you die.
- Any player can pick up these bags.
- Contents are preserved.

## Limits

- Each bag has a maximum weight and slot count.
- The number of bags per player is limited (configurable).
- A bag cannot contain another bag.
