---
title: "Configuration"
description: "Race Builder configuration reference"
script: "foltone-racebuilder"
section: "foltone_racebuilder"
order: 2
version: "1.0.0"
---

# Configuration — foltone_racebuilder

All configuration is in `config.lua`. This file is not encrypted and can be freely edited.

## General Settings

| Option | Default | Description |
|--------|---------|-------------|
| `Config.Locale` | `"en"` | Language (`"en"` or `"fr"`) |
| `Config.Framework` | `"ESX"` | Framework: `"ESX"`, `"QBCore"` or `"standalone"` |
| `Config.Debug` | `true` | Enable debug prints in server console |
| `Config.AdminPermission` | `"admin"` | ACE permission for admin check (standalone mode) |
| `Config.InteractionDistance` | `3.0` | Distance to interact with NPC (E key fallback) |
| `Config.CountdownSeconds` | `2` | Countdown duration before race start |
| `Config.DefaultMaxPlayers` | `10` | Default max players per race |
| `Config.NpcModel` | `"csb_janitor"` | Ped model for race NPC |

## Map Blip

| Option | Default | Description |
|--------|---------|-------------|
| `Config.Blip.Sprite` | `315` | Blip icon on the map |
| `Config.Blip.Color` | `1` | Blip color |
| `Config.Blip.Scale` | `0.8` | Blip size |
| `Config.Blip.Display` | `2` | Blip display mode |

## Checkpoint Appearance

| Option | Default | Description |
|--------|---------|-------------|
| `Config.Checkpoint.Diameter` | `10.0` | Default checkpoint diameter (editable per checkpoint in editor) |
| `Config.Checkpoint.NearHeight` | `4.0` | Cylinder height |
| `Config.Checkpoint.Color` | `{r=45, g=110, b=185, a=200}` | Normal checkpoint color (RGBA) |
| `Config.Checkpoint.FinishColor` | `{r=53, g=154, b=71, a=255}` | Finish checkpoint color (RGBA) |
| `Config.Checkpoint.CylinderZOffset` | `0.05` | Ground cylinder Z offset |
| `Config.Checkpoint.IconZOffset` | `2.0` | Icon height above checkpoint |
| `Config.Checkpoint.IconSizeRatio` | `0.2` | Icon size = diameter × ratio |
| `Config.Checkpoint.IconType` | `2` | DrawMarker type for arrow (2 = arrow) |
| `Config.Checkpoint.FinishIconType` | `4` | DrawMarker type for finish (4 = checkered) |
| `Config.Checkpoint.ShowIconRing` | `true` | Show cylinder ring behind the icon |

## Checkpoint GPS Blip

| Option | Default | Description |
|--------|---------|-------------|
| `Config.CheckpointBlip.Sprite` | `854` | GPS blip sprite during race |
| `Config.CheckpointBlip.Color` | `3` | GPS blip color |
| `Config.CheckpointBlip.Scale` | `0.9` | GPS blip scale |

## Start Grid (Multiplayer)

| Option | Default | Description |
|--------|---------|-------------|
| `Config.StartGrid.Columns` | `2` | Grid columns (2 = F1 style side by side) |
| `Config.StartGrid.ColumnSpacing` | `3.5` | Lateral spacing between columns (meters) |
| `Config.StartGrid.RowSpacing` | `8.0` | Spacing between rows (meters) |
| `Config.StartGrid.StaggerOffset` | `4.0` | Right column stagger offset (meters) |
| `Config.StartGrid.PreviewSlots` | `10` | Slots shown in editor preview |

## Race Settings

| Option | Default | Description |
|--------|---------|-------------|
| `Config.Race.ExitVehicleTimeout` | `10` | Seconds before DQ if out of vehicle |
| `Config.Race.QuitKey` | `166` | Key to quit race (166 = F5) |

## Editor Controls

All editor controls use FiveM control IDs. Reference: https://docs.fivem.net/docs/game-references/controls/

| Option | Default | Key |
|--------|---------|-----|
| `Forward` | `32` | W |
| `Backward` | `33` | S |
| `StrafeLeft` | `34` | A |
| `StrafeRight` | `35` | D |
| `Up` | `22` | Space |
| `Down` | `36` | Ctrl |
| `Sprint` | `21` | Shift |
| `Place` | `24` | Left click |
| `GrabMove` | `25` | Right click |
| `Menu` | `191` | Enter |
| `DeleteLast` | `177` | Backspace |
| `RotateLeft` | `44` | Q |
| `RotateRight` | `46` | E |

## Notification System

Edit `Config.Notification` in `config.lua` to use your own notification system:

```lua
Config.Notification = function(message)
    -- Default: uses foltone_ultra_hud
    exports.foltone_ultra_hud:Notify(message)

    -- Example: native GTA notification
    -- SetNotificationTextEntry("STRING")
    -- AddTextComponentString(message)
    -- DrawNotification(false, false)

    -- Example: ox_lib
    -- lib.notify({ description = message })
end
```

## Framework Customization

Edit `client/cl_editable.lua` and `server/sv_editable.lua` to adapt to your framework. These files are not encrypted.

### sv_editable.lua

Contains admin check, player identifier, and player name functions. Customize these for your framework:

- `IsPlayerAdminServer(source)` — Returns true if the player is admin
- `GetPlayerIdentifierServer(source)` — Returns the player's unique identifier
- `GetPlayerNameServer(source)` — Returns the player's name
