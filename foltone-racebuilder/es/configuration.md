---
title: "Configuracion"
description: "Referencia de configuracion de Race Builder"
script: "foltone-racebuilder"
section: "Race Builder"
order: 2
version: "1.1.0"
---

# Configuracion — foltone_racebuilder

Toda la configuracion se encuentra en `config.lua`. Este archivo no esta encriptado y puede editarse libremente.

## Ajustes generales

| Opcion | Por defecto | Descripcion |
|--------|-------------|-------------|
| `Config.Locale` | `"en"` | Idioma (`"en"` o `"fr"`) |
| `Config.Framework` | `"ESX"` | Framework: `"ESX"`, `"QBCore"` o `"standalone"` |
| `Config.Debug` | `true` | Activar mensajes de depuracion en la consola del servidor |
| `Config.AdminPermission` | `"admin"` | Permiso ACE para verificacion de administrador (modo standalone) |
| `Config.InteractionDistance` | `3.0` | Distancia para interactuar con el NPC (tecla E como alternativa) |
| `Config.CountdownSeconds` | `2` | Duracion de la cuenta regresiva antes del inicio de la carrera |
| `Config.DefaultMaxPlayers` | `10` | Jugadores maximos por defecto por carrera |
| `Config.NpcModel` | `"csb_janitor"` | Modelo de ped para el NPC de carreras |

## Blip del mapa

| Opcion | Por defecto | Descripcion |
|--------|-------------|-------------|
| `Config.Blip.Sprite` | `315` | Icono del blip en el mapa |
| `Config.Blip.Color` | `1` | Color del blip |
| `Config.Blip.Scale` | `0.8` | Tamano del blip |
| `Config.Blip.Display` | `2` | Modo de visualizacion del blip |

## Apariencia de checkpoints

| Opcion | Por defecto | Descripcion |
|--------|-------------|-------------|
| `Config.Checkpoint.Diameter` | `10.0` | Diametro predeterminado del checkpoint (editable por checkpoint en el editor) |
| `Config.Checkpoint.NearHeight` | `4.0` | Altura del cilindro |
| `Config.Checkpoint.Color` | `{r=45, g=110, b=185, a=200}` | Color del checkpoint normal (RGBA) |
| `Config.Checkpoint.FinishColor` | `{r=53, g=154, b=71, a=255}` | Color del checkpoint de meta (RGBA) |
| `Config.Checkpoint.CylinderZOffset` | `0.05` | Desplazamiento Z del cilindro en el suelo |
| `Config.Checkpoint.IconZOffset` | `3.0` | Altura del icono sobre el checkpoint |
| `Config.Checkpoint.IconSizeRatio` | `0.2` | Tamano del icono = diametro x ratio |
| `Config.Checkpoint.IconType` | `2` | Tipo de DrawMarker para flecha (2 = flecha) |
| `Config.Checkpoint.FinishIconType` | `4` | Tipo de DrawMarker para meta (4 = bandera a cuadros) |

## Blip GPS del checkpoint

| Opcion | Por defecto | Descripcion |
|--------|-------------|-------------|
| `Config.CheckpointBlip.Sprite` | `854` | Sprite del blip GPS durante la carrera |
| `Config.CheckpointBlip.Color` | `3` | Color del blip GPS |
| `Config.CheckpointBlip.Scale` | `0.9` | Escala del blip GPS |

## Parrilla de salida (Multijugador)

| Opcion | Por defecto | Descripcion |
|--------|-------------|-------------|
| `Config.StartGrid.Columns` | `2` | Columnas de la parrilla (2 = estilo F1 lado a lado) |
| `Config.StartGrid.ColumnSpacing` | `3.5` | Espaciado lateral entre columnas (metros) |
| `Config.StartGrid.RowSpacing` | `8.0` | Espaciado entre filas (metros) |
| `Config.StartGrid.StaggerOffset` | `4.0` | Desplazamiento escalonado de la columna derecha (metros) |
| `Config.StartGrid.StartOffset` | `12.0` | Distancia entre la linea de salida y la primera fila de coches (metros) |
| `Config.StartGrid.PreviewSlots` | `10` | Posiciones mostradas en la vista previa del editor |

## Ajustes de carrera

| Opcion | Por defecto | Descripcion |
|--------|-------------|-------------|
| `Config.Race.ExitVehicleTimeout` | `10` | Segundos antes de descalificacion si esta fuera del vehiculo |
| `Config.Race.QuitKey` | `166` | Tecla para abandonar la carrera (166 = F5) |

## Controles del editor

Todos los controles del editor usan IDs de control de FiveM. Referencia: https://docs.fivem.net/docs/game-references/controls/

| Opcion | Por defecto | Tecla |
|--------|-------------|-------|
| `Forward` | `32` | W |
| `Backward` | `33` | S |
| `StrafeLeft` | `34` | A |
| `StrafeRight` | `35` | D |
| `Up` | `22` | Espacio |
| `Down` | `36` | Ctrl |
| `Sprint` | `21` | Shift |
| `Place` | `24` | Clic izquierdo |
| `GrabMove` | `25` | Clic derecho |
| `Menu` | `191` | Enter |
| `DeleteLast` | `177` | Retroceso |
| `RotateLeft` | `44` | Q |
| `RotateRight` | `46` | E |

## Sistema de notificaciones

Edita `Config.Notification` en `config.lua` para usar tu propio sistema de notificaciones:

```lua
Config.Notification = function(message)
    -- Por defecto: usa foltone_ultra_hud
    exports.foltone_ultra_hud:Notify(message)

    -- Ejemplo: notificacion nativa de GTA
    -- SetNotificationTextEntry("STRING")
    -- AddTextComponentString(message)
    -- DrawNotification(false, false)

    -- Ejemplo: ox_lib
    -- lib.notify({ description = message })
end
```

## Personalizacion del framework

Edita `client/cl_editable.lua` y `server/sv_editable.lua` para adaptar a tu framework. Estos archivos no estan encriptados.

### sv_editable.lua

Contiene funciones de verificacion de administrador, identificador de jugador y nombre de jugador. Personaliza estas funciones para tu framework:

- `IsPlayerAdminServer(source)` — Devuelve true si el jugador es administrador
- `GetPlayerIdentifierServer(source)` — Devuelve el identificador unico del jugador
- `GetPlayerNameServer(source)` — Devuelve el nombre del jugador
