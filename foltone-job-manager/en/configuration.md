---
title: "Configuration"
description: "Job Manager script configuration guide"
script: "foltone-job-manager"
section: "Job Manager"
order: 2
version: "1.0.0"
---

# Configuration — foltone_job_manager

All configuration is done in `config.lua` at the root of the script.

## Language

```lua
Config.Locale = "fr" -- "fr" or "en"
```

Translations are in the `locales/` folder. You can add your own languages by creating a new file (e.g., `locales/de.lua`).

## Framework

```lua
Config.Framework = "esx" -- "esx", "qbcore" or "standalone"
```

The script supports ESX Legacy, QBCore and a Standalone mode. In Standalone mode, you must manually handle player loading and the `foltone_job_manager:getData` event.

## Society List

```lua
Config.SocietyList = {
    ["police"] = {
        bossGrade = "boss",
        position = vector3(448.25, -973.33, 29.69),
        color = { r = 0, g = 0, b = 255 },
    }
}
```

| Parameter | Description |
|-----------|-------------|
| Key (e.g., `"police"`) | Job name as defined in your framework |
| `bossGrade` | Grade name that has access to management (e.g., `"boss"`) |
| `position` | `vector3` coordinates for the access marker |
| `color` | RGB color for the marker |

### Adding a Society

```lua
["ambulance"] = {
    bossGrade = "boss",
    position = vector3(311.0, -595.0, 43.29),
    color = { r = 255, g = 0, b = 0 },
},
```

> The key name must match exactly the job name in your database.

## Interface Theme

```lua
Config.theme = {
    bgColorLight = "#f5f5f5",
    bgColorDark = "#2c2c2c",
    textColorLight = "#333",
    textColorDark = "#fff",
    borderColorLight = "#ddd",
    borderColorDark = "#444",
    primaryColor = "#ffffff",
    primaryDark = "#f5f5f5",
    secondaryColor = "#7476DC",
    shadow = "0 4px 6px rgba(0, 0, 0, 0.1)"
}
```

The interface supports **light** and **dark** modes. Players can toggle between them using the button in the interface. The choice is saved in the browser.

| Parameter | Description |
|-----------|-------------|
| `bgColorLight` / `bgColorDark` | Background color (light / dark mode) |
| `textColorLight` / `textColorDark` | Text color |
| `borderColorLight` / `borderColorDark` | Border color |
| `primaryColor` / `primaryDark` | Primary color |
| `secondaryColor` | Accent color (buttons, active sidebar) |
| `shadow` | Tablet drop shadow |

## Notifications

```lua
Config.Notification = function(message)
    SetNotificationTextEntry("STRING")
    AddTextComponentString(message)
    DrawNotification(false, false)
end
```

Replace this function with your preferred notification system (e.g., okokNotify, ox_lib notify, etc.).

## Help Text

```lua
Config.DisplayText = function(text)
    SetTextComponentFormat("STRING")
    AddTextComponentString(text)
    DisplayHelpTextFromStringLabel(0, 0, 1, -1)
end
```

Customize the help text display (shown when a boss is near the marker).
