---
title: "Configuración"
description: "Configuración del script Foltone FiveM Discord Bot"
script: "foltone-fivem-discord-bot"
section: "Discord Bot"
order: 2
version: "1.0.0"
---

# Configuración — foltone_fivem_discord_bot

Toda la configuración se realiza en el archivo `config.lua` en la raíz del script.

## Idioma

```lua
Config.Locale = "en" -- "fr" o "en"
```

Las traducciones están en la carpeta `locales/`. Puedes añadir tus propios idiomas creando un nuevo archivo (por ejemplo, `locales/de.lua`).

## Framework

```lua
Config.Framework = "auto" -- "auto", "esx", "qbcore" o "qbx"
```

| Valor | Framework | Descripción |
|-------|-----------|-------------|
| `"auto"` | Detección automática | Detecta automáticamente ESX / QBCore / QBX al iniciar |
| `"esx"` | ESX Legacy | Fuerza el uso de ESX |
| `"qbcore"` | QBCore | Fuerza el uso de QBCore |
| `"qbx"` | QBX | Fuerza el uso de QBX |

## Modo Debug

```lua
Config.Debug = false
```

Establece `true` para habilitar registros detallados en la consola del servidor. Desactívalo en producción.

## Bot

```lua
Config.Bot = {
    token = "YOUR_BOT_TOKEN",
    guildId = "YOUR_GUILD_ID",
    port = 3847,
    authToken = "RANDOM_SECRET",
    autoStart = true,
    healthCheckInterval = 60,
}
```

| Parámetro | Descripción |
|-----------|-------------|
| `token` | Token del bot de Discord (obtenido del Portal de Desarrolladores) |
| `guildId` | ID del servidor de Discord objetivo |
| `port` | Puerto de comunicación HTTP interna entre FiveM y el bot de Node.js |
| `authToken` | Clave secreta compartida entre FiveM y el bot (seguridad interna) |
| `autoStart` | `true` para iniciar el bot automáticamente con el recurso |
| `healthCheckInterval` | Segundos entre cada verificación de estado del bot |

> **Seguridad**: Nunca compartas tu `token` o `authToken`. Estos valores están en `config.lua` (archivo abierto), ten cuidado con el acceso al servidor.

## Permisos

```lua
Config.Permissions = {
    ["moderator"] = {
        roleIds = {"ROLE_ID"},
        commands = {
            "kick", "warn", "mute", "unmute", "freeze", "unfreeze",
            "playerlist", "playerinfo", "slap", "heal", "spectate"
        }
    },
    ["admin"] = {
        roleIds = {"ROLE_ID"},
        commands = {
            "ban", "unban", "tp", "revive", "setjob",
            "givemoney", "removemoney", "setmoney",
            "giveitem", "removeitem",
            "spawnvehicle", "deletevehicle",
            "sanctions", "announce", "weather", "time",
            "whitelist", "watchlist"
        }
    },
    ["founder"] = {
        roleIds = {"ROLE_ID"},
        commands = {"*"}    -- * = acceso a todos los comandos
    }
}
```

| Parámetro | Descripción |
|-----------|-------------|
| Clave (ej., `"moderator"`) | Nombre del grupo de permisos (personalizado) |
| `roleIds` | Lista de IDs de roles de Discord con este nivel de acceso |
| `commands` | Lista de comandos permitidos, o `{"*"}` para permitir todos |

### Comandos disponibles por categoría

| Categoría | Comandos |
|----------|----------|
| Jugadores | `playerlist`, `playerinfo`, `kick`, `ban`, `unban` |
| Moderación | `warn`, `mute`, `unmute`, `freeze`, `unfreeze`, `slap`, `heal`, `spectate` |
| Economía | `givemoney`, `removemoney`, `setmoney`, `giveitem`, `removeitem` |
| Vehículos | `spawnvehicle`, `deletevehicle` |
| Teletransporte | `tp`, `revive` |
| Trabajo | `setjob` |
| Servidor | `announce`, `weather`, `time`, `whitelist` |
| Seguimiento | `sanctions`, `watchlist` |
| Programación | `schedule` |
| Información | `serverstatus` |

## Registros

```lua
Config.Logs = {
    enabled = true,
    mode = "split",
    channels = {
        single = "CHANNEL_ID",
        connection = "CHANNEL_ID",
        death = "CHANNEL_ID",
        transaction = "CHANNEL_ID",
        admin = "CHANNEL_ID",
        chat = "CHANNEL_ID",
    },
    transactionThreshold = 50000,
    maskIP = true,
    actionButtons = true,
}
```

| Parámetro | Descripción |
|-----------|-------------|
| `enabled` | Habilitar/deshabilitar el sistema de registros |
| `mode` | `"single"` = un canal para todos los registros, `"split"` = un canal por tipo |
| `channels.single` | ID del canal único (usado si `mode = "single"`) |
| `channels.connection` | Canal para conexiones/desconexiones de jugadores |
| `channels.death` | Canal para muertes de jugadores |
| `channels.transaction` | Canal para transacciones económicas |
| `channels.admin` | Canal para acciones de administradores |
| `channels.chat` | Canal para el chat del juego |
| `transactionThreshold` | Cantidad mínima para registrar una transacción |
| `maskIP` | `true` para ocultar las IPs de los jugadores en los registros |
| `actionButtons` | `true` para mostrar botones de acción rápida en los embeds |

## Dashboard

```lua
Config.Dashboard = {
    enabled = true,
    channelId = "CHANNEL_ID",
    refreshInterval = 30,
    showPlayerList = true,
    showAdminActions = true,
    showConnections = true,
    buttons = true,
}
```

| Parámetro | Descripción |
|-----------|-------------|
| `enabled` | Habilitar/deshabilitar el dashboard |
| `channelId` | ID del canal donde se muestra el dashboard |
| `refreshInterval` | Segundos entre cada actualización automática |
| `showPlayerList` | Mostrar la lista de jugadores en el dashboard |
| `showAdminActions` | Mostrar las acciones de administradores recientes |
| `showConnections` | Mostrar las conexiones recientes |
| `buttons` | Mostrar botones de acción rápida debajo del dashboard |

> El dashboard muestra un embed actualizado en tiempo real con estadísticas del servidor.

## Tickets

```lua
Config.Tickets = {
    enabled = true,
    categoryId = "CHANNEL_ID",
    logsChannelId = "CHANNEL_ID",
    maxOpenPerPlayer = 2,
    autoCloseAfter = 1440,
    transcriptEnabled = true,
    command = "ticket",
    keybind = "F6",
}
```

| Parámetro | Descripción |
|-----------|-------------|
| `enabled` | Habilitar/deshabilitar el sistema de tickets |
| `categoryId` | ID de la categoría de Discord donde se crean los canales de tickets |
| `logsChannelId` | ID del canal de registros para tickets cerrados |
| `maxOpenPerPlayer` | Máximo de tickets abiertos por jugador simultáneamente |
| `autoCloseAfter` | Minutos antes de cerrar automáticamente un ticket inactivo (1440 = 24h) |
| `transcriptEnabled` | `true` para guardar transcripciones de tickets cerrados |
| `command` | Comando de FiveM para abrir un ticket desde el juego |
| `keybind` | Tecla de acceso rápido para abrir un ticket desde el juego |

## Chat

```lua
Config.Chat = {
    enabled = true,
    channelId = "CHANNEL_ID",
    mode = "all",
    discordPrefix = "[DISCORD]",
    discordColor = {59, 130, 246},
    webhookName = "FiveM Chat",
    filterLinks = true,
    maxLength = 500,
}
```

| Parámetro | Descripción |
|-----------|-------------|
| `enabled` | Habilitar/deshabilitar la sincronización del chat |
| `channelId` | ID del canal de Discord vinculado al chat del juego |
| `mode` | `"all"` = todos los mensajes, `"discord_only"` = solo de Discord al juego, `"game_only"` = solo del juego a Discord |
| `discordPrefix` | Prefijo mostrado en el juego antes de los mensajes de Discord |
| `discordColor` | Color RGB para los mensajes de Discord en el juego |
| `webhookName` | Nombre mostrado en el webhook de Discord |
| `filterLinks` | `true` para bloquear enlaces en el chat |
| `maxLength` | Longitud máxima de los mensajes sincronizados |

## Alertas

```lua
Config.Alerts = {
    enabled = true,
    channelId = "CHANNEL_ID",
    mentionRoleId = "ROLE_ID",
    cooldownPerPlayer = 30,
    cooldownGlobal = 10,
    rules = {
        warns = { enabled = true, count = 3, period = 1440 },
        transaction = { enabled = true, threshold = 500000 },
        playersLow = { enabled = true, threshold = 5 },
        playersHigh = { enabled = true, threshold = 60 },
        watchlist = { enabled = true },
        kills = { enabled = true, count = 5, period = 10 },
        crashDetect = { enabled = true, count = 10, period = 5 },
    }
}
```

| Parámetro | Descripción |
|-----------|-------------|
| `enabled` | Habilitar/deshabilitar el sistema de alertas |
| `channelId` | ID del canal donde se envían las alertas |
| `mentionRoleId` | ID del rol mencionado en alertas urgentes |
| `cooldownPerPlayer` | Segundos entre dos alertas para el mismo jugador |
| `cooldownGlobal` | Segundos entre dos alertas globales |

### Reglas de alertas

| Regla | Parámetros | Descripción |
|------|------------|-------------|
| `warns` | `count`, `period` | Alerta si un jugador recibe X advertencias en Y minutos |
| `transaction` | `threshold` | Alerta si una transacción supera el umbral |
| `playersLow` | `threshold` | Alerta si el número de jugadores cae por debajo del umbral |
| `playersHigh` | `threshold` | Alerta si el número de jugadores supera el umbral |
| `watchlist` | — | Alerta cuando un jugador vigilado se conecta |
| `kills` | `count`, `period` | Alerta si un jugador mata a X jugadores en Y minutos |
| `crashDetect` | `count`, `period` | Alerta si X jugadores se desconectan en Y minutos |

## Programador de tareas

```lua
Config.Scheduler = {
    enabled = true,
    tasks = {
        {
            name = "daily_restart",
            type = "restart",
            cron = "0 4 * * *",
            countdownMinutes = {30, 15, 5, 1},
        },
    }
}
```

| Parámetro | Descripción |
|-----------|-------------|
| `enabled` | Habilitar/deshabilitar el programador |
| `tasks` | Lista de tareas programadas |
| `tasks[].name` | Nombre único de la tarea |
| `tasks[].type` | Tipo: `"restart"` (reinicio del servidor) o `"announce"` (anuncio) |
| `tasks[].cron` | Expresión cron para la programación |
| `tasks[].countdownMinutes` | Minutos antes del reinicio para enviar avisos |

## Panel NUI

```lua
Config.Panel = {
    enabled = true,
    command = "adminpanel",
    keybind = "F7",
    refreshInterval = 15,
    logsMaxDisplay = 100,
}
```

| Parámetro | Descripción |
|-----------|-------------|
| `enabled` | Habilitar/deshabilitar el panel NUI de administración en el juego |
| `command` | Comando para abrir el panel |
| `keybind` | Tecla de acceso rápido para abrir/cerrar el panel |
| `refreshInterval` | Segundos entre cada actualización automática de datos |
| `logsMaxDisplay` | Número máximo de registros mostrados en la pestaña de registros del panel |

## Base de datos

```lua
Config.Database = {
    logRetentionDays = 30,
    purgeInterval = 1440,
}
```

| Parámetro | Descripción |
|-----------|-------------|
| `logRetentionDays` | Número de días de retención de registros antes de la eliminación automática |
| `purgeInterval` | Minutos entre cada limpieza automática de la base de datos |

## Sistema de administración

```lua
Config.AdminSystem = "auto"
```

| Valor | Descripción |
|-------|-------------|
| `"auto"` | Detección automática (ACE, vMenu, txAdmin, EasyAdmin) |
| `"ace"` | Permisos nativos de FiveM ACE (`IsPlayerAceAllowed`) |
| `"vmenu"` | Sistema de permisos de vMenu |
| `"txadmin"` | Sistema de permisos de txAdmin |
| `"easyadmin"` | Sistema de permisos de EasyAdmin |
| `"custom"` | Función personalizada en `server/sv_editable.lua` |
