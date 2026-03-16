---
title: "Exports & Events"
description: "Ultra HUD API reference for developers"
script: "foltone-ultra-hud"
section: "Ultra HUD"
order: 3
version: "1.0.0"
---

# Exports & Events — foltone_ultra_hud

## Client Exports

### Notify

Send a simple notification (no image).

```lua
exports.foltone_ultra_hud:Notify(message, type, duration)
```

| Parameter | Type | Required | Description |
|---|---|---|---|
| `message` | string | yes | Notification text |
| `type` | string | no | `"success"`, `"error"`, `"warning"`, `"info"` (default: neutral) |
| `duration` | number | no | Duration in ms (default: 5000) |

**Example:**

```lua
exports.foltone_ultra_hud:Notify("You received $500", "success")
exports.foltone_ultra_hud:Notify("Access denied", "error", 3000)
```

### AdvancedNotify

Send a notification with an image (GTA-style).

```lua
exports.foltone_ultra_hud:AdvancedNotify(image, title, message, subtitle, duration)
```

| Parameter | Type | Required | Description |
|---|---|---|---|
| `image` | string | yes | Image URL or path |
| `title` | string | yes | Bold title text |
| `message` | string | yes | Message body |
| `subtitle` | string | no | Smaller subtitle below the title |
| `duration` | number | no | Duration in ms (default: 5000) |

**Example:**

```lua
exports.foltone_ultra_hud:AdvancedNotify(
    "https://i.imgur.com/example.png",
    "LESTER CREST",
    "I have a job for you. Come see me.",
    "New mission",
    7000
)
```

### ShowHud / HideHud

Show or hide the entire HUD.

```lua
exports.foltone_ultra_hud:ShowHud()
exports.foltone_ultra_hud:HideHud()
```

**Example:**

```lua
-- Hide HUD during a cutscene
exports.foltone_ultra_hud:HideHud()
Wait(5000)
exports.foltone_ultra_hud:ShowHud()
```

## Client Events

### foltone_ultra_hud:notify

Simple notification via event (usable from client or triggered from server).

```lua
-- Client-side
TriggerEvent("foltone_ultra_hud:notify", message, type, duration)

-- Server-side (to a specific player)
TriggerClientEvent("foltone_ultra_hud:notify", source, message, type, duration)

-- Server-side (to all players)
TriggerClientEvent("foltone_ultra_hud:notify", -1, message, type, duration)
```

### foltone_ultra_hud:advancedNotify

Advanced notification via event.

```lua
-- Client-side
TriggerEvent("foltone_ultra_hud:advancedNotify", image, title, message, subtitle, duration)

-- Server-side
TriggerClientEvent("foltone_ultra_hud:advancedNotify", source, image, title, message, subtitle, duration)
```

### foltone_ultra_hud:enableHud / foltone_ultra_hud:disableHud

Show or hide the HUD via events (useful for server-side control).

```lua
-- Server-side: hide HUD for a player
TriggerClientEvent("foltone_ultra_hud:disableHud", source)

-- Server-side: show HUD for a player
TriggerClientEvent("foltone_ultra_hud:enableHud", source)
```

## Notification Types

| Type | Color | Icon | Use case |
|---|---|---|---|
| *(none)* | White | None | General messages |
| `"success"` | Green | Checkmark | Confirmations, completed actions |
| `"error"` | Red | Cross | Errors, denied actions |
| `"warning"` | Yellow | Triangle | Warnings, important notices |
| `"info"` | Blue | Info circle | Informational messages |

## Test Command

Use `/testnotif` to test notifications in-game:

```
/testnotif all       -- Send all notification types
/testnotif simple    -- Neutral notification
/testnotif success   -- Success notification
/testnotif error     -- Error notification
/testnotif warning   -- Warning notification
/testnotif info      -- Info notification
/testnotif advanced  -- Advanced notification with image
```
