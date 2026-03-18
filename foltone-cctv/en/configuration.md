---
title: "Configuration"
description: "Configuration guide for Foltone CCTV"
script: "foltone-cctv"
section: "Foltone CCTV"
order: 2
version: "1.0.0"
---

# Configuration — foltone_cctv

All configuration is in the `config.lua` file.

## Framework & Locale

```lua
Config.Framework = "esx"       -- "esx", "qbcore" or "qbx"
Config.Locale = "en"           -- "en" or "fr"
Config.InteractionType = "ox_target" -- "ox_target", "drawtext" or "marker"
Config.Debug = false
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `Framework` | string | Server framework |
| `Locale` | string | Language for notifications and UI |
| `InteractionType` | string | Interaction method for NPCs and stations |
| `Debug` | boolean | Enable debug prints in console |

## Items

```lua
Config.TabletItem = "cctv_tablet"
Config.StationItem = "cctv_station"
Config.StationProp = "prop_cctv_unit_01"
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `TabletItem` | string | Inventory item name for the tablet |
| `StationItem` | string | Inventory item name for the monitoring station |
| `StationProp` | string | GTA prop model for fixed station objects |

## Camera types

```lua
Config.MaxCamerasPerPlayer = 10
Config.PlacementDistance = 8.0
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `MaxCamerasPerPlayer` | number | Maximum cameras a player can place |
| `PlacementDistance` | number | Maximum distance (meters) to place a camera |

### Camera type structure

Each entry in `Config.CameraTypes` defines a camera model:

```lua
{
    id = "standard",
    item = "cctv_cam_standard",
    label = "Standard",
    description = "Classic wall-mounted surveillance camera.",
    specs = { "FOV 70", "ZOOM x4", "60 FPS" },
    prop = "prop_cctv_cam_01a",
    price = 3000,
    offset = {
        pos = vector3(-0.13, 0.61, 0.21),
        pitch = -16.9,
        yaw = 40.0,
        propYaw = 180.0,
    },
    fov = { default = 70.0, min = 25.0, max = 100.0 },
    zoomStep = 5.0,
    rotationSpeed = 2.0,
    maxVertAngle = 60.0,
},
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `id` | string | Unique identifier (stored in database) |
| `item` | string | Inventory item name for this camera type |
| `label` | string | Display name in the shop UI |
| `description` | string | Description shown in the shop UI |
| `specs` | table | Array of spec badges shown in the shop (e.g. "FOV 70") |
| `prop` | string | GTA prop model name |
| `price` | number | Purchase price from the shop |
| `offset.pos` | vector3 | Camera view position offset (forward, left, up) relative to the prop |
| `offset.pitch` | number | Camera view pitch offset (degrees) |
| `offset.yaw` | number | Camera view yaw offset (degrees) |
| `offset.propYaw` | number | Prop rotation offset relative to camera view direction (degrees) |
| `fov.default` | number | Default field of view (degrees) |
| `fov.min` | number | Minimum FOV when zoomed in |
| `fov.max` | number | Maximum FOV when zoomed out |
| `zoomStep` | number | FOV change per scroll step |
| `rotationSpeed` | number | Mouse sensitivity for camera rotation |
| `maxVertAngle` | number | Maximum vertical rotation angle (degrees) |

### Default camera types

| ID | Prop | Price | FOV | Description |
|----|------|-------|-----|-------------|
| `standard` | `prop_cctv_cam_01a` | $3,000 | 70 | Classic wall-mounted camera |
| `dome` | `prop_cctv_cam_02a` | $5,500 | 90 | 360 dome wide-angle |
| `bullet` | `prop_cctv_cam_04b` | $4,000 | 55 | Long-range with powerful zoom |
| `mini_bullet` | `hei_prop_bank_cctv_02` | $3,500 | 55 | Compact and discreet |
| `ptz` | `prop_cctv_cam_05a` | $8,000 | 60 | Professional pan-tilt-zoom |

### Calibrating offsets

Use the in-game debug command to calibrate camera offsets:

```
/cctv_debug
```

1. Approach a placed camera (< 15m)
2. Run the command — enters debug camera view
3. Adjust with controls:
   - **Mouse** — pitch / yaw offset
   - **Scroll** — prop yaw rotation
   - **Arrow keys** — position offset (forward/back/left/right)
   - **E / Q** — position offset (up/down)
   - **Backspace** — exit and print values
4. Copy the printed values into `Config.CameraTypes[x].offset`

## Permissions

```lua
Config.AllowedJobs = {
    "police",
    "ambulance",
}
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `AllowedJobs` | table | Jobs allowed to place cameras. Empty table = everyone can place |

## Motion detection

```lua
Config.MotionDetection = {
    Radius = 15.0,
    Cooldown = 60,
    Default = true,
}
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `Radius` | number | Detection radius in meters |
| `Cooldown` | number | Seconds between alerts for the same camera |
| `Default` | boolean | Whether new cameras have motion detection enabled by default |

## Destruction

```lua
Config.DestructionHits = 3

Config.DestructionWeapons = {
    "WEAPON_CROWBAR",
    "WEAPON_PISTOL",
    -- ...
}
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `DestructionHits` | number | Number of hits/shots required to destroy a camera |
| `DestructionWeapons` | table | List of weapon hashes that can damage cameras |

## Camera visual effects

```lua
Config.CameraEffect = {
    timecycle = "CAMERA_secuirity",
    strength = 0.6,
    vignette = 1.0,
    grain = 1.0,
    scanline = 1.0,
}
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `timecycle` | string | GTA timecycle modifier name |
| `strength` | number | Timecycle intensity (0.0 = off, 1.0 = max) |
| `vignette` | number | Screen vignette intensity (0.0 = off, 1.0 = max) |
| `grain` | number | Film grain intensity (0.0 = off, 1.0 = max) |
| `scanline` | number | Scanline effect intensity (0.0 = off, 1.0 = max) |

Available timecycles: `CAMERA_secuirity` (default), `CAMERA_BW` (black & white), `NG_filmic08` (cinematic), `phone_cam3` (webcam look).

## Captures

```lua
Config.MaxCaptures = 20
```

Maximum number of screenshots saved per player. When exceeded, the oldest capture is automatically deleted.

> Requires `screenshot-basic` and `set screenshot_basic_allow_fs_write "true"` in server.cfg.

## Shop PED

```lua
Config.Ped = {
    model = "s_m_y_ammucity_01",
    scenario = "WORLD_HUMAN_STAND_IMPATIENT",
}
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `model` | string | PED model name for the shop vendor |
| `scenario` | string | PED idle animation scenario |

## Shop positions

```lua
Config.ShopPositions = {
    {
        pos = vector3(72.25, -1399.10, 29.38),
        heading = 270.0,
        blip = {
            sprite = 689,
            color = 3,
            scale = 0.7,
            label = "Security Shop",
        },
    },
}
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `pos` | vector3 | PED spawn position |
| `heading` | number | PED facing direction |
| `blip.sprite` | number | Map blip sprite ID |
| `blip.color` | number | Map blip color ID |
| `blip.scale` | number | Map blip size |
| `blip.label` | string | Map blip label text |

## Computer positions

```lua
Config.ComputerPositions = {
    {
        pos = vector3(441.81, -982.08, 30.69),
        heading = 0.0,
        label = "computer_label",
    },
}
```

Fixed computer terminals that open the camera panel (no prop spawned, zone-based interaction).

## Station positions

```lua
Config.StationPositions = {
    {
        pos = vector3(441.81, -982.08, 30.69),
        heading = 0.0,
    },
}
```

Fixed monitoring stations with `prop_cctv_unit_01` prop spawned. Same functionality as tablets.

## Interaction

```lua
Config.InteractionDistance = 2.5

Config.Marker = {
    type = 1,
    scale = vector3(1.0, 1.0, 0.5),
    color = { r = 59, g = 130, b = 246, a = 120 },
}
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `InteractionDistance` | number | Distance to trigger interaction (drawtext/marker modes) |
| `Marker.type` | number | GTA marker type (1 = cylinder) |
| `Marker.scale` | vector3 | Marker dimensions |
| `Marker.color` | table | RGBA color of the marker |

## Notifications

```lua
function Notification(source, message, type)
```

Override this function in `config.lua` to use your own notification system.
