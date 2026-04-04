---
title: "Usage"
description: "Usage guide for the foltone_gruppe6 script"
script: "foltone-gruppe6"
section: "Gruppe6"
order: 3
version: "1.0.0"
---

# Using foltone_gruppe6

## Dual System: Job + Robbery

This script offers two independent mechanics depending on the player's role.

---

## Job System (Gruppe6 Employees)

### Clocking In

1. Go to the service point with the `gruppe6` job
2. Open the RageUI menu
3. Select **Clock In** to put on the uniform

### Missions

1. Once on duty, accept a mission from the menu
2. Get into the armored vehicle at the indicated point
3. Follow the GPS waypoints to complete the delivery / collection
4. Return to the depot to validate the mission and receive your reward

### Clocking Out

Return to the service point and select **Clock Out** to remove the uniform.

---

## Robbery System (Criminals)

### Requirements

- A minimum number of police officers must be on duty (configurable)
- The player must have the explosive item in their inventory
- The cooldown from the last robbery must have elapsed

### Procedure

1. Go near the armored van
2. Interact to start the robbery
3. Use the explosive on the rear door of the van
4. Collect the money inside
5. Escape before the police arrive

### Notifications

- Police receive an automatic alert when the robbery is triggered
- A cooldown timer prevents repeating the robbery immediately

---

## Commands

No server commands are needed. All interaction is done through the RageUI menu and in-game interaction points.
