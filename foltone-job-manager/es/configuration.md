---
title: "Configuración"
description: "Guía de configuración del script Job Manager"
script: "foltone-job-manager"
section: "Job Manager"
order: 2
version: "1.0.0"
---

# Configuración — foltone_job_manager

Toda la configuración se realiza en el archivo `config.lua` en la raíz del script.

## Idioma

```lua
Config.Locale = "fr" -- "fr" o "en"
```

Las traducciones están en la carpeta `locales/`. Puedes añadir tus propios idiomas creando un nuevo archivo (ej: `locales/de.lua`).

## Framework

```lua
Config.Framework = "esx" -- "esx", "qbcore" o "standalone"
```

El script soporta ESX Legacy, QBCore y un modo Standalone. En modo Standalone, debes gestionar manualmente la carga del jugador y el evento `foltone_job_manager:getData`.

## Lista de sociedades

```lua
Config.SocietyList = {
    ["police"] = {
        bossGrade = "boss",
        position = vector3(448.25, -973.33, 29.69),
        color = { r = 0, g = 0, b = 255 },
    }
}
```

| Parámetro | Descripción |
|-----------|-------------|
| Clave (ej: `"police"`) | Nombre del trabajo tal como está definido en tu framework |
| `bossGrade` | Nombre del grado que tiene acceso a la gestión (ej: `"boss"`) |
| `position` | Coordenadas `vector3` del marcador de acceso |
| `color` | Color RGB del marcador |

### Añadir una sociedad

```lua
["ambulance"] = {
    bossGrade = "boss",
    position = vector3(311.0, -595.0, 43.29),
    color = { r = 255, g = 0, b = 0 },
},
```

> El nombre de la clave debe coincidir exactamente con el nombre del trabajo en tu base de datos.

## Tema de la interfaz

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

La interfaz soporta modo **claro** y **oscuro**. Los jugadores pueden alternar entre ellos usando el botón en la interfaz. La elección se guarda en el navegador.

| Parámetro | Descripción |
|-----------|-------------|
| `bgColorLight` / `bgColorDark` | Color de fondo (modo claro / oscuro) |
| `textColorLight` / `textColorDark` | Color del texto |
| `borderColorLight` / `borderColorDark` | Color de los bordes |
| `primaryColor` / `primaryDark` | Color primario |
| `secondaryColor` | Color de acento (botones, sidebar activa) |
| `shadow` | Sombra de la tablet |

## Notificaciones

```lua
Config.Notification = function(message)
    SetNotificationTextEntry("STRING")
    AddTextComponentString(message)
    DrawNotification(false, false)
end
```

Reemplaza esta función con tu sistema de notificaciones preferido (ej: okokNotify, ox_lib notify, etc.).

## Texto de ayuda

```lua
Config.DisplayText = function(text)
    SetTextComponentFormat("STRING")
    AddTextComponentString(text)
    DisplayHelpTextFromStringLabel(0, 0, 1, -1)
end
```

Personaliza la visualización del texto de ayuda (se muestra cuando un jefe está cerca del marcador).
