---
title: "Configuration"
description: "Elevator Builder script configuration guide"
script: "foltone-elevator-builder"
section: "foltone_elevator_builder"
order: 2
version: "1.0.0"
---

# Configuration — foltone_elevator_builder

All configuration is done in `Config.lua` at the root of the script. Some parameters can also be modified in-game via the admin menu's configuration panel.

## Language

```lua
Config.Locale = 'fr' -- 'fr', 'en' or 'es'
```

Three languages are included: French, English and Spanish. Translations are in the `locales/` folder. You can add your own languages by creating a new file.

## Marker

The marker indicates floor positions to players.

```lua
Config.marker_type = 20
Config.marker_red = 114
Config.marker_green = 204
Config.marker_blue = 114
Config.marker_alpha = 250
Config.marker_scaleX = 1.0
Config.marker_scaleY = 1.0
Config.marker_scaleZ = 1.0
```

| Parameter | Description |
|-----------|-------------|
| `marker_type` | GTA V marker type (see [FiveM wiki](https://docs.fivem.net/docs/game-references/markers/)) |
| `marker_red/green/blue` | Marker RGB color |
| `marker_alpha` | Opacity (0-255) |
| `marker_scaleX/Y/Z` | Marker size |

Advanced parameters are also available: `marker_dirX/Y/Z`, `marker_rotX/Y/Z`, `marker_bobUpAndDown`, `marker_faceCamera`, `marker_rotate`.

## Distances

```lua
Config.marker_render_distance = 10.0
Config.interaction_distance = 1.0
```

| Parameter | Description |
|-----------|-------------|
| `marker_render_distance` | Distance (in meters) at which the marker is displayed |
| `interaction_distance` | Distance at which the player can interact (E key or ox_target) |

## Target System (ox_target)

```lua
Config.use_target = false
```

| Value | Behavior |
|-------|----------|
| `false` | Interaction via **E key** (default behavior) |
| `true` | Interaction via **ox_target** (requires ox_target installed) |

> If ox_target is not detected, the script automatically falls back to E key interaction.

## Teleport Animation

```lua
Config.teleport_animation = true
Config.teleport_duration = 2000
Config.teleport_fade_duration = 500
```

| Parameter | Description |
|-----------|-------------|
| `teleport_animation` | Enable/disable black fade animation during teleportation |
| `teleport_duration` | Total transition duration in milliseconds |
| `teleport_fade_duration` | Black fade duration (in and out) in milliseconds |

When animation is enabled, the player sees:
1. Black fade out (doors closing)
2. Teleportation + wait (movement simulation)
3. Black fade in (doors opening)

## Sounds

```lua
Config.sounds_enabled = true
Config.sound_volume = 0.5
```

| Parameter | Description |
|-----------|-------------|
| `sounds_enabled` | Enable/disable sound effects |
| `sound_volume` | Sound volume (0.0 to 1.0) |

Sounds played:
- **Ding** — On floor arrival
- **Doors** — On panel open/close
- **Movement** — During floor transition

## In-Game Configuration Panel

All parameters above can also be modified **in-game** via the configuration panel accessible from the admin menu (`/fab` → Configuration button). Changes are applied immediately and broadcast to all connected clients.

## Command Customization

In `client/cl_editable.lua`, you can change the admin menu command:

```lua
RegisterCommand("fab", function(source, args)
    TriggerEvent("foltone_ascenseur:open_menu")
end)
```

Replace `"fab"` with your desired command name.
