---
title: "Usage"
description: "Elevator Builder script usage guide"
script: "foltone-elevator-builder"
section: "Elevator Builder"
order: 3
version: "1.1.0"
---

# Usage — foltone_elevator_builder

## Overview

Elevator Builder allows you to create and manage elevators in-game via a NUI interface. Elevators are composed of floors with a name and position. Players can teleport between floors using an interactive elevator panel.

## Admin Menu

### Opening the Menu

Type `/fab` in chat to open the admin NUI menu.

### Creating an Elevator

1. Open the admin menu (`/fab`)
2. Click **"Create an elevator"**
3. Set the **elevator name**
4. Choose the **number of floors** (1 to 20)
5. For each floor:
   - Click **"Set name"** and enter the name (e.g., "Ground Floor", "Floor 1", "Roof")
   - Click **"Set position"** — the menu closes, your current position is recorded
6. Customize the **elevator style** (panel accent color, scale, side, marker appearance)
7. Click **"Create the elevator"** to confirm

> Green preview markers appear during creation to verify positions.

### Editing an Elevator

1. Open the admin menu (`/fab`)
2. Click **"Edit an elevator"**
3. Select the elevator to edit
4. You can:
   - **Rename the elevator** — Click the rename button
   - **Edit a floor** — Select the floor, then change its name or position
   - **Delete a floor** — Select the floor, then click "Delete"
   - **Delete the elevator** — Removes the elevator and all its floors

### Customizing Elevator Style

During creation or editing, you can customize each elevator's appearance:

- **Panel accent color** (RGB) — the accent color of the elevator NUI panel
- **Panel scale** — size of the panel (0.7 to 1.3)
- **Panel side** — display on the left or right of the screen
- **Marker type, scale, color, alpha** — appearance of the floor markers
- **Marker bob/spin** — animation options

A live preview is displayed as you adjust the settings.

### Configuration Panel

From the admin menu, access the configuration panel to modify global settings in real-time:

- Marker color and type
- Render and interaction distances
- ox_target toggle
- Teleport animation (duration, fade)
- Sounds (toggle, volume)

Changes are applied immediately for all players.

## Player Usage

### Without ox_target (E key)

1. Walk up to an elevator marker (configurable distance, default 3.5m)
2. The text **"Press E to access the elevator"** appears
3. Press **E**
4. The elevator NUI panel opens, showing the current floor and available floors
5. Click on the desired floor to teleport

### With ox_target

1. Aim at an elevator point with ox_target
2. Click the elevator option
3. The panel opens — select your floor

### Closing the Panel

Press **Escape** or click the close button.

## Elevator Panel Interface

The panel displays:
- The **current floor** in real-time (digital indicator)
- The **list of available floors** with their names
- **Buttons** for each floor

The floor indicator updates automatically when the player moves between floor positions.

## Teleport Animation

When animation is enabled, the process is:
1. Door closing sound
2. Black fade out
3. Teleportation + movement sound
4. Black fade in + arrival ding
5. Door opening sound

## Data Storage

Elevators are saved in the `json/data.json` file. This file is automatically read/written by the server. Format:

```json
[
    {
        "label": "Main Elevator",
        "floors": [
            { "idEtage": 1, "name": "Ground Floor", "position": { "x": 0.0, "y": 0.0, "z": 0.0 } },
            { "idEtage": 2, "name": "Floor 1", "position": { "x": 0.0, "y": 0.0, "z": 10.0 } }
        ],
        "style": {
            "panel_accent_r": 255,
            "panel_accent_g": 180,
            "panel_accent_b": 0,
            "panel_scale": 1,
            "panel_side": "right",
            "marker_type": 25,
            "marker_scale": 0.8,
            "marker_red": 114,
            "marker_green": 204,
            "marker_blue": 114,
            "marker_alpha": 180,
            "marker_bob": false,
            "marker_spin": true
        }
    }
]
```

Each elevator stores its own `style` object containing panel and marker customization. If not specified, the global `Config.lua` defaults are used.

## Available Exports

The script exposes exports for integration with other scripts:

### openElevator

Opens the elevator panel for a specific elevator.

```lua
-- Opens elevator with ID 1
local success = exports['foltone-elevator-builder']:openElevator(1)
```

### teleportToFloor

Directly teleports the player to a specific floor.

```lua
-- Teleports to floor 2 of elevator 1
local success = exports['foltone-elevator-builder']:teleportToFloor(1, 2)
```

### getElevators

Gets the list of all elevators and their floors.

```lua
local elevators = exports['foltone-elevator-builder']:getElevators()
-- Returns: { { id = 1, label = "...", floors = { { idEtage = 1, name = "Ground Floor" }, ... } }, ... }
```

### getCurrentFloor

Gets the name of the closest floor to the player.

```lua
local floorName = exports['foltone-elevator-builder']:getCurrentFloor()
-- Returns: "Ground Floor" or nil if no floor nearby
```
