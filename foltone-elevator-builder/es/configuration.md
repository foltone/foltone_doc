---
title: "Configuración"
description: "Guía de configuración del script Elevator Builder"
script: "foltone-elevator-builder"
section: "foltone_elevator_builder"
order: 2
version: "1.0.0"
---

# Configuración — foltone_elevator_builder

Toda la configuración se realiza en el archivo `Config.lua` en la raíz del script. Algunos parámetros también se pueden modificar en el juego a través del panel de configuración del menú de administración.

## Idioma

```lua
Config.Locale = 'fr' -- 'fr', 'en' o 'es'
```

Se incluyen tres idiomas: francés, inglés y español. Las traducciones están en la carpeta `locales/`. Puedes añadir tus propios idiomas creando un nuevo archivo.

## Marcador

El marcador indica las posiciones de los pisos a los jugadores.

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

| Parámetro | Descripción |
|-----------|-------------|
| `marker_type` | Tipo de marcador GTA V (ver [wiki FiveM](https://docs.fivem.net/docs/game-references/markers/)) |
| `marker_red/green/blue` | Color RGB del marcador |
| `marker_alpha` | Opacidad (0-255) |
| `marker_scaleX/Y/Z` | Tamaño del marcador |

Parámetros avanzados también disponibles: `marker_dirX/Y/Z`, `marker_rotX/Y/Z`, `marker_bobUpAndDown`, `marker_faceCamera`, `marker_rotate`.

## Distancias

```lua
Config.marker_render_distance = 10.0
Config.interaction_distance = 1.0
```

| Parámetro | Descripción |
|-----------|-------------|
| `marker_render_distance` | Distancia (en metros) a la que se muestra el marcador |
| `interaction_distance` | Distancia a la que el jugador puede interactuar (tecla E u ox_target) |

## Sistema de objetivo (ox_target)

```lua
Config.use_target = false
```

| Valor | Comportamiento |
|-------|---------------|
| `false` | Interacción mediante la **tecla E** (comportamiento por defecto) |
| `true` | Interacción mediante **ox_target** (requiere ox_target instalado) |

> Si ox_target no se detecta, el script usa automáticamente la tecla E como alternativa.

## Animación de teletransporte

```lua
Config.teleport_animation = true
Config.teleport_duration = 2000
Config.teleport_fade_duration = 500
```

| Parámetro | Descripción |
|-----------|-------------|
| `teleport_animation` | Activa/desactiva la animación de fundido negro durante el teletransporte |
| `teleport_duration` | Duración total de la transición en milisegundos |
| `teleport_fade_duration` | Duración del fundido negro (entrada y salida) en milisegundos |

Cuando la animación está activada, el jugador ve:
1. Fundido negro (cierre de puertas)
2. Teletransporte + espera (simulación del movimiento)
3. Fundido claro (apertura de puertas)

## Sonidos

```lua
Config.sounds_enabled = true
Config.sound_volume = 0.5
```

| Parámetro | Descripción |
|-----------|-------------|
| `sounds_enabled` | Activa/desactiva los efectos de sonido |
| `sound_volume` | Volumen del sonido (0.0 a 1.0) |

Sonidos reproducidos:
- **Ding** — Al llegar al piso
- **Puertas** — Al abrir/cerrar el panel
- **Movimiento** — Durante la transición entre pisos

## Panel de configuración en el juego

Todos los parámetros anteriores también se pueden modificar **en el juego** a través del panel de configuración accesible desde el menú de administración (`/fab` → botón Configuración). Los cambios se aplican inmediatamente y se transmiten a todos los clientes conectados.

## Personalización del comando

En `client/cl_editable.lua`, puedes cambiar el comando de acceso al menú de administración:

```lua
RegisterCommand("fab", function(source, args)
    TriggerEvent("foltone_ascenseur:open_menu")
end)
```

Reemplaza `"fab"` por el nombre de comando deseado.
