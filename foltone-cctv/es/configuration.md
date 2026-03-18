---
title: "Configuracion"
description: "Guia de configuracion de Foltone CCTV"
script: "foltone-cctv"
section: "Foltone CCTV"
order: 2
version: "1.0.0"
---

# Configuracion — foltone_cctv

Toda la configuracion se encuentra en el archivo `config.lua`.

## Framework e idioma

```lua
Config.Framework = "esx"       -- "esx", "qbcore" o "qbx"
Config.Locale = "en"           -- "en" o "fr"
Config.InteractionType = "ox_target" -- "ox_target", "drawtext" o "marker"
Config.Debug = false
```

| Parametro | Tipo | Descripcion |
|-----------|------|-------------|
| `Framework` | string | Framework del servidor |
| `Locale` | string | Idioma para notificaciones e interfaz |
| `InteractionType` | string | Metodo de interaccion para NPCs y estaciones |
| `Debug` | boolean | Habilitar mensajes de depuracion en consola |

## Objetos

```lua
Config.TabletItem = "cctv_tablet"
Config.StationItem = "cctv_station"
Config.StationProp = "prop_cctv_unit_01"
```

| Parametro | Tipo | Descripcion |
|-----------|------|-------------|
| `TabletItem` | string | Nombre del objeto de inventario para la tablet |
| `StationItem` | string | Nombre del objeto de inventario para la estacion de monitoreo |
| `StationProp` | string | Modelo de prop de GTA para objetos de estacion fija |

## Tipos de camara

```lua
Config.MaxCamerasPerPlayer = 10
Config.PlacementDistance = 8.0
```

| Parametro | Tipo | Descripcion |
|-----------|------|-------------|
| `MaxCamerasPerPlayer` | number | Maximo de camaras que un jugador puede colocar |
| `PlacementDistance` | number | Distancia maxima (metros) para colocar una camara |

### Estructura del tipo de camara

Cada entrada en `Config.CameraTypes` define un modelo de camara:

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

| Parametro | Tipo | Descripcion |
|-----------|------|-------------|
| `id` | string | Identificador unico (almacenado en la base de datos) |
| `item` | string | Nombre del objeto de inventario para este tipo de camara |
| `label` | string | Nombre para mostrar en la interfaz de la tienda |
| `description` | string | Descripcion mostrada en la interfaz de la tienda |
| `specs` | table | Array de insignias de especificaciones mostradas en la tienda (ej. "FOV 70") |
| `prop` | string | Nombre del modelo de prop de GTA |
| `price` | number | Precio de compra en la tienda |
| `offset.pos` | vector3 | Offset de posicion de la vista de camara (adelante, izquierda, arriba) relativo al prop |
| `offset.pitch` | number | Offset de inclinacion de la vista de camara (grados) |
| `offset.yaw` | number | Offset de orientacion de la vista de camara (grados) |
| `offset.propYaw` | number | Offset de rotacion del prop relativo a la direccion de vista de la camara (grados) |
| `fov.default` | number | Campo de vision predeterminado (grados) |
| `fov.min` | number | FOV minimo cuando se acerca el zoom |
| `fov.max` | number | FOV maximo cuando se aleja el zoom |
| `zoomStep` | number | Cambio de FOV por paso de scroll |
| `rotationSpeed` | number | Sensibilidad del raton para la rotacion de la camara |
| `maxVertAngle` | number | Angulo maximo de rotacion vertical (grados) |

### Tipos de camara predeterminados

| ID | Prop | Precio | FOV | Descripcion |
|----|------|--------|-----|-------------|
| `standard` | `prop_cctv_cam_01a` | $3,000 | 70 | Camara clasica montada en pared |
| `dome` | `prop_cctv_cam_02a` | $5,500 | 90 | Domo 360 gran angular |
| `bullet` | `prop_cctv_cam_04b` | $4,000 | 55 | Largo alcance con zoom potente |
| `mini_bullet` | `hei_prop_bank_cctv_02` | $3,500 | 55 | Compacta y discreta |
| `ptz` | `prop_cctv_cam_05a` | $8,000 | 60 | Pan-tilt-zoom profesional |

### Calibracion de offsets

Usa el comando de depuracion en el juego para calibrar los offsets de la camara:

```
/cctv_debug
```

1. Acercate a una camara colocada (< 15m)
2. Ejecuta el comando — entra en la vista de depuracion de la camara
3. Ajusta con los controles:
   - **Raton** — offset de inclinacion / orientacion
   - **Scroll** — rotacion de orientacion del prop
   - **Teclas de flecha** — offset de posicion (adelante/atras/izquierda/derecha)
   - **E / Q** — offset de posicion (arriba/abajo)
   - **Retroceso** — salir e imprimir valores
4. Copia los valores impresos en `Config.CameraTypes[x].offset`

## Permisos

```lua
Config.AllowedJobs = {
    "police",
    "ambulance",
}
```

| Parametro | Tipo | Descripcion |
|-----------|------|-------------|
| `AllowedJobs` | table | Empleos permitidos para colocar camaras. Tabla vacia = todos pueden colocar |

## Deteccion de movimiento

```lua
Config.MotionDetection = {
    Radius = 15.0,
    Cooldown = 60,
    Default = true,
}
```

| Parametro | Tipo | Descripcion |
|-----------|------|-------------|
| `Radius` | number | Radio de deteccion en metros |
| `Cooldown` | number | Segundos entre alertas para la misma camara |
| `Default` | boolean | Si las camaras nuevas tienen la deteccion de movimiento activada por defecto |

## Destruccion

```lua
Config.DestructionHits = 3

Config.DestructionWeapons = {
    "WEAPON_CROWBAR",
    "WEAPON_PISTOL",
    -- ...
}
```

| Parametro | Tipo | Descripcion |
|-----------|------|-------------|
| `DestructionHits` | number | Numero de impactos/disparos necesarios para destruir una camara |
| `DestructionWeapons` | table | Lista de hashes de armas que pueden danar camaras |

## Efectos visuales de la camara

```lua
Config.CameraEffect = {
    timecycle = "CAMERA_secuirity",
    strength = 0.6,
    vignette = 1.0,
    grain = 1.0,
    scanline = 1.0,
}
```

| Parametro | Tipo | Descripcion |
|-----------|------|-------------|
| `timecycle` | string | Nombre del modificador timecycle de GTA |
| `strength` | number | Intensidad del timecycle (0.0 = desactivado, 1.0 = maximo) |
| `vignette` | number | Intensidad de la vineta de pantalla (0.0 = desactivado, 1.0 = maximo) |
| `grain` | number | Intensidad del grano de pelicula (0.0 = desactivado, 1.0 = maximo) |
| `scanline` | number | Intensidad del efecto de linea de escaneo (0.0 = desactivado, 1.0 = maximo) |

Timecycles disponibles: `CAMERA_secuirity` (predeterminado), `CAMERA_BW` (blanco y negro), `NG_filmic08` (cinematico), `phone_cam3` (aspecto de webcam).

## Capturas

```lua
Config.MaxCaptures = 20
```

Numero maximo de capturas de pantalla guardadas por jugador. Cuando se excede, la captura mas antigua se elimina automaticamente.

> Requiere `screenshot-basic` y `set screenshot_basic_allow_fs_write "true"` en server.cfg.

## PED de la tienda

```lua
Config.Ped = {
    model = "s_m_y_ammucity_01",
    scenario = "WORLD_HUMAN_STAND_IMPATIENT",
}
```

| Parametro | Tipo | Descripcion |
|-----------|------|-------------|
| `model` | string | Nombre del modelo de PED para el vendedor de la tienda |
| `scenario` | string | Escenario de animacion inactiva del PED |

## Posiciones de la tienda

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

| Parametro | Tipo | Descripcion |
|-----------|------|-------------|
| `pos` | vector3 | Posicion de aparicion del PED |
| `heading` | number | Direccion a la que mira el PED |
| `blip.sprite` | number | ID del sprite del blip en el mapa |
| `blip.color` | number | ID del color del blip en el mapa |
| `blip.scale` | number | Tamano del blip en el mapa |
| `blip.label` | string | Texto de la etiqueta del blip en el mapa |

## Posiciones de ordenadores

```lua
Config.ComputerPositions = {
    {
        pos = vector3(441.81, -982.08, 30.69),
        heading = 0.0,
        label = "computer_label",
    },
}
```

Terminales de ordenador fijos que abren el panel de camaras (sin prop generado, interaccion basada en zonas).

## Posiciones de estaciones

```lua
Config.StationPositions = {
    {
        pos = vector3(441.81, -982.08, 30.69),
        heading = 0.0,
    },
}
```

Estaciones de monitoreo fijas con prop `prop_cctv_unit_01` generado. Misma funcionalidad que las tablets.

## Interaccion

```lua
Config.InteractionDistance = 2.5

Config.Marker = {
    type = 1,
    scale = vector3(1.0, 1.0, 0.5),
    color = { r = 59, g = 130, b = 246, a = 120 },
}
```

| Parametro | Tipo | Descripcion |
|-----------|------|-------------|
| `InteractionDistance` | number | Distancia para activar la interaccion (modos drawtext/marker) |
| `Marker.type` | number | Tipo de marcador de GTA (1 = cilindro) |
| `Marker.scale` | vector3 | Dimensiones del marcador |
| `Marker.color` | table | Color RGBA del marcador |

## Notificaciones

```lua
function Notification(source, message, type)
```

Sobrescribe esta funcion en `config.lua` para usar tu propio sistema de notificaciones.
