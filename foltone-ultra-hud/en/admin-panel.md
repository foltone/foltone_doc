---
title: "Admin Panel"
description: "Ultra HUD admin panel usage guide"
script: "foltone-ultra-hud"
section: "Ultra HUD"
order: 4
version: "1.0.0"
---

# Admin Panel — foltone_ultra_hud

The admin panel provides a full in-game configuration interface. Changes apply to **all players** on the server and persist across restarts.

## Opening the Panel

Type the admin command in chat (default: `/hudadmin`). You need admin permissions to access it.

### Permission Check Order

1. **Framework group** — ESX: `admin`, `superadmin`, `god` / QBCore: `admin`, `god` permission
2. **Custom groups** — Any group listed in `Config.adminGroups`
3. **ACE fallback** — `command.hudadmin` ACE permission

## Panel Sections

### Colors

Change the color of each HUD element using color pickers:

- Text, Health, Armour, Hunger, Thirst, Stamina, Apnea, Fuel

Colors apply to bars, circles, squares, hexagons, and their glow effects.

### Visibility

Toggle individual HUD elements on or off:

- ID, Job, Job 2/Gang, Money, Bank, Dirty Money, Position, Health, Armour, Hunger, Thirst, Stamina, Apnea, Speedometer

### Display

| Setting | Options | Description |
|---|---|---|
| Needs Display | Bar, Circle, Square, Hexagon, Text | Shape of status indicators |
| Shape Fill | Stroke, Fill | Stroke = outline progress, Fill = solid bottom-to-top fill |
| Speed Unit | KM/H, MPH | Speedometer unit |

### Size

Scale sliders for each HUD group (0.5x to 1.5x):

- Wallet, Position, Status, Speedometer

### Notifications

| Setting | Range | Description |
|---|---|---|
| Position | 6 positions | Where notifications appear on screen |
| Width | 15-40 vw | Notification container width |
| Scale | 0.5-2.0 | Notification scale multiplier |

## Preview Mode

Click **PREVIEW** to see all HUD elements with demo data while the panel stays open. Click **EXIT PREVIEW** to return.

## Arrange Mode

Click **ARRANGE** to enter drag-and-drop mode:

1. The admin panel closes and all HUD elements become draggable
2. Drag elements to reposition them anywhere on screen
3. Click **SAVE POSITIONS** to persist the layout for all players
4. Click **CANCEL** to discard changes
5. Click **RESET DEFAULT** to restore original positions

## Saving

Click **SAVE** to save all settings (colors, visibility, display, size, notifications) to `settings.json`. Changes are immediately broadcast to all connected players.

> Settings are stored server-side in `settings.json` in the resource folder. They persist across server restarts and apply to all players.
