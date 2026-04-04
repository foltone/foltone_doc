---
title: "Usage"
description: "Usage guide for the foltone_territories script"
script: "foltone-territories"
section: "Territories"
order: 3
version: "1.0.0"
---

# Using foltone_territories

## Overview

This script allows gangs to capture territories by selling drugs to NPCs. Captured territories yield better sale prices. NPCs can accept, refuse, or call the police.

---

## Capture System

### How to Capture a Territory

1. Have a configured gang job
2. Go to a territory zone (visible on the map)
3. Approach an NPC in the zone
4. Open the RageUI menu to sell drugs
5. Each successful sale earns **capture points**
6. Accumulate enough points to capture the zone

### Progression

- Each drug type gives a different number of points
- Riskier drugs yield more points
- Progress is saved in the database
- When the threshold is reached, the territory is captured by your gang

---

## NPC Reactions

When you approach an NPC to sell, three reactions are possible:

### Accept
The NPC buys the drug. You receive money and capture points.

### Refuse
The NPC refuses the deal. Nothing happens, you keep your drugs.

### Call Police
The NPC refuses and **calls the police**. Law enforcement receives an alert with your position. Flee quickly.

The probability of each reaction is configurable per drug type.

---

## Benefits of Captured Territories

- **Better prices**: Drugs sell for more in a territory controlled by your gang
- **Zone control**: Your gang visually dominates the zone on the map

---

## Selling Drugs

1. Make sure you have drugs in your inventory
2. Approach an NPC (not on the blacklist)
3. Interact via the RageUI menu
4. Select the drug to sell
5. Wait for the NPC's reaction

### Blacklisted NPCs

Certain NPCs (police officers, etc.) cannot be targeted. They are defined in the configuration blacklist.

---

## Commands

No commands needed. All interaction is done through the RageUI menu and defined map zones.
