---
title: "Usage"
description: "Usage guide for foltone_ammunation script"
script: "foltone-ammunation"
section: "Ammunation"
order: 3
version: "1.0.0"
---

# Usage

## Buying weapons

1. Go to an Ammu-Nation store (icon on the map).
2. Approach the shopkeeper NPC.
3. Press the interaction key to open the RageUI menu.
4. Browse aisles (handguns, rifles, ammunition, etc.).
5. Select an item and confirm the purchase.

### Weapon license

Some weapons require a license. If you don't have one:

- The menu will offer to purchase a license at the configured price.
- Once obtained, restricted weapons become available.
- The license is permanent (unless revoked by an administrator).

## Robbery

### Requirements

- A minimum number of police officers must be on duty (configurable).
- The cooldown between robberies must have elapsed.
- You must be near the NPC.

### How it works

1. Approach the NPC and select the robbery option.
2. A progress bar will appear during the robbery.
3. Stay near the NPC -- moving away cancels the robbery.
4. Do not kill the NPC -- their death cancels the robbery.
5. Once completed, you receive a random amount (within the configured range).

### Alerts

During a robbery:
- On-duty police officers receive an alert with your photo and the store location.
- A temporary blip appears on the police map.

## Commands

No player commands are needed. All interaction is done via the RageUI menu near the NPC.

## Permissions

| Action | Requirement |
|---|---|
| Buy unrestricted weapons | None |
| Buy restricted weapons | Weapon license required |
| Rob the store | Minimum police count reached |
