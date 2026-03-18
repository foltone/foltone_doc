---
title: "Usage"
description: "Usage guide for Foltone CCTV"
script: "foltone-cctv"
section: "Foltone CCTV"
order: 3
version: "1.0.0"
---

# Usage — foltone_cctv

## Overview

Foltone CCTV is a complete surveillance camera system for FiveM. Players can buy, place, and manage security cameras with real-time viewing, motion detection, job sharing, and screenshot capture. The script supports 5 camera types, each with unique props, optics, and pricing.

## Buying cameras

### Shop

Interact with the shop PED at configured positions to open the camera shop.

The shop displays all available camera types in a card grid:
- **Camera image** and model name
- **Description** and technical specs (FOV, zoom, etc.)
- **Price** and buy button

Each camera type gives a different inventory item when purchased.

### Access methods

| Mode | How to interact |
|------|----------------|
| `ox_target` | Aim at the PED with the target cursor |
| `drawtext` | Approach the PED and press **E** |
| `marker` | Enter the marker and press **E** |

## Placing cameras

1. Use the camera item from your inventory
2. The **placement HUD** appears (bottom-left) with instructions:
   - **Left click** — Place the camera
   - **Right click** — Cancel
   - **Scroll** — Rotate the camera
3. Aim at a wall or surface — the ghost camera snaps to the surface normal
4. The status indicator shows **READY** (green) or **TOO FAR** (red)
5. Click to confirm — a name input appears at the center of the screen
6. Enter a name and press **OK** — the camera is installed

> Cameras automatically orient against the wall surface. The rotation offset allows fine-tuning the viewing angle.

## Viewing cameras

### Tablet

Use the `cctv_tablet` item to open the surveillance panel. The player plays a tablet-holding animation with a prop.

### Computer terminals

Interact with fixed computer positions to open the panel. The player plays a typing animation.

### Monitoring stations

Interact with `prop_cctv_unit_01` stations at configured positions. Same functionality as tablets.

## Surveillance panel

The panel has **4 tabs**:

### Grid

Displays all accessible cameras in a grid view with:
- **Animated CCTV noise** preview per camera
- **Camera name** and status badges (ACTIVE, MOTION, JOB, SHARED)
- **REC indicator** and live timestamp
- **VIEW button** to enter the camera

### Management

Lists all cameras you own with controls:
- **Motion detection** toggle (on/off)
- **Assign to job** — shares the camera with all players of your current job
- **Rename** — change the camera display name
- **Delete** — permanently remove the camera

### Sharing

Share your cameras with specific players:
- Enter a **player server ID** to grant access
- **Revoke** access for any shared player
- Shared players can view your cameras but not manage them

### Captures

View and manage screenshots taken from cameras:
- Thumbnail preview (if `screenshot-basic` is configured)
- Camera name and capture timestamp
- **Delete** button to remove captures

## Camera view

When viewing a camera, the screen shows a CCTV overlay with visual effects:

### Controls

| Key | Action |
|-----|--------|
| **Mouse** | Rotate camera (pan/tilt) |
| **Scroll** | Zoom in/out |
| **N** | Toggle night vision |
| **E** | Take a screenshot |
| **Left/Right arrows** | Previous/next camera |
| **Backspace** | Return to the grid panel |
| **Escape** | Exit camera view |

### Visual effects

The camera view includes configurable effects:
- **Timecycle modifier** — GTA security camera filter (desaturation, contrast)
- **Vignette** — darkened edges
- **Film grain** — animated noise overlay
- **Scanline** — moving horizontal scan line
- **Corner markers** — targeting corners
- **Chromatic aberration** — subtle color fringing

> All effects are configurable in `Config.CameraEffect`. Set any value to `0.0` to disable it.

### Night vision

Press **N** to toggle night vision (green-tinted amplified view). Press again to return to normal CCTV view.

### Sound effects

The camera system plays native GTA sounds for:
- Opening/closing camera view
- Zooming in/out
- Rotating the camera
- Switching between cameras
- Taking screenshots
- Toggling night vision

## Job groups

Camera owners can assign cameras to their job group:

1. Open the **Management** tab
2. Click **ASSIGN TO JOB** on a camera
3. The camera is now accessible to **all players with the same job**
4. A yellow **JOB** badge appears on shared cameras in the grid
5. Click the job badge again to make the camera **private**

> Only the camera owner can assign/remove the job group. Job members can view but not manage.

## Camera destruction

Cameras can be destroyed by shooting or hitting them with configured weapons.

| Parameter | Effect |
|-----------|--------|
| `Config.DestructionHits` | Number of hits required (default: 3) |
| `Config.DestructionWeapons` | List of weapons that deal damage |

When destroyed:
- The camera prop is removed for all players
- The camera is deleted from the database
- The owner receives a notification

## Motion detection

When enabled on a camera:
- Detects players within the configured radius
- Sends a notification to the owner with camera name and time
- Also notifies players with shared access
- Respects the cooldown between alerts

## Adding camera types

To add a new camera type:

1. Add a new entry to `Config.CameraTypes` in `config.lua`
2. Create the corresponding inventory item in your inventory system
3. Optionally add an SVG image at `client/nui/img/cam_<id>.svg`
4. Use `/cctv_debug` in-game to calibrate the camera offset

The shop and placement system automatically pick up new types from the config.
