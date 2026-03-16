---
title: "Configuración"
description: "Guía de configuración del script Elevator Builder"
script: "foltone-elevator-builder"
section: "Elevator Builder"
order: 2
version: "1.1.0"
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
Config.marker_type = 25
Config.marker_scale = 0.8
Config.marker_red = 114
Config.marker_green = 204
Config.marker_blue = 114
Config.marker_alpha = 180
Config.marker_bob = false
Config.marker_spin = true
```

| Parámetro | Descripción |
|-----------|-------------|
| `marker_type` | Tipo de marcador GTA V (ver [wiki FiveM](https://docs.fivem.net/docs/game-references/markers/)) — tipos soportados: 1, 2, 6, 20, 25, 27, 29 |
| `marker_scale` | Tamaño del marcador |
| `marker_red/green/blue` | Color RGB del marcador |
| `marker_alpha` | Opacidad (0-255) |
| `marker_bob` | Activa/desactiva la animación de rebote |
| `marker_spin` | Activa/desactiva la animación de rotación |

> Cada ascensor también puede tener su propio estilo de marcador personalizado, configurable desde el menú de administración durante la creación o edición.

## Distancias

```lua
Config.marker_render_distance = 10.0
Config.interaction_distance = 3.5
```

| Parámetro | Descripción |
|-----------|-------------|
| `marker_render_distance` | Distancia (en metros) a la que se muestra el marcador |
| `interaction_distance` | Distancia a la que el jugador puede interactuar (tecla E o sistema de objetivo) |

## Sistema de objetivo

```lua
Config.use_target = 'auto'
```

| Valor | Comportamiento |
|-------|---------------|
| `'auto'` | **Detección automática** — usa el primer sistema de objetivo disponible (por defecto) |
| `'ox_target'` | Fuerza el uso de **ox_target** |
| `'qb-target'` | Fuerza el uso de **qb-target** |
| `'interact'` | Fuerza el uso de **interact** (Renewed) |
| `false` | Desactivado — interacción mediante la **tecla E** únicamente |

Orden de detección en modo `'auto'`: ox_target → qb-target → interact.

> Si el sistema de objetivo configurado no se detecta, el script usa automáticamente la tecla E como alternativa.

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

## Apariencia del panel

Personaliza la interfaz del panel de ascensor mostrada a los jugadores.

```lua
Config.panel_accent_r = 255
Config.panel_accent_g = 180
Config.panel_accent_b = 0
Config.panel_scale = 1.0
Config.panel_side = 'right'
```

| Parámetro | Descripción |
|-----------|-------------|
| `panel_accent_r/g/b` | Color de acento del panel de ascensor (RGB) — dorado por defecto |
| `panel_scale` | Multiplicador de tamaño del panel (rango recomendado: 0.7 a 1.3) |
| `panel_side` | Posición del panel en pantalla: `'left'` o `'right'` |

> Cada ascensor puede tener su propio estilo de panel personalizado, configurable durante la creación o edición.

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
