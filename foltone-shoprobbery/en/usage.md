---
title: "Usage"
description: "Usage guide for the foltone_shoprobbery script"
script: "foltone-shoprobbery"
section: "Shop Robbery"
order: 3
version: "1.0.0"
---

# Using foltone_shoprobbery

## Overview

This script combines a shop system and a robbery system. Players can buy items from convenience stores or rob them for money. Same system as the ammunation robbery but adapted for shops.

---

## Shop (Purchasing Items)

### Buying Items

1. Go to a convenience store
2. Approach the shopkeeper NPC
3. Open the RageUI menu
4. Browse the available items
5. Select and confirm your purchase

Items and their prices are configurable in the config file.

---

## Robbery

### Prerequisites

- A minimum number of police officers must be on duty
- The shop cooldown must have elapsed
- The shopkeeper NPC must be alive

### Robbery Procedure

1. Approach the shopkeeper NPC in a convenience store
2. Select the robbery option from the menu
3. A progress bar appears - **do not move**
4. Wait for the progress to complete to collect the money

### Automatic Cancellation

The robbery is **immediately cancelled** if:
- You move during the progress bar
- The shopkeeper NPC dies (do not kill them)

### Police Alerts

When a robbery is triggered:
- All on-duty police officers receive an alert
- The alert includes a **suspect photo**
- The alert includes the **geolocation** of the shop
- The exact position is marked on the police map

### Cooldown

After a successful robbery, the shop enters cooldown. No other robbery can take place in that shop until the timer expires.

---

## Commands

No commands needed. All interaction is done through the RageUI menu and interaction points.
