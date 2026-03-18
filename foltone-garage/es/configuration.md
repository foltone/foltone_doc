---
title: "Configuracion"
description: "Guia de configuracion de Foltone Garage"
script: "foltone-garage"
section: "Foltone Garage"
order: 2
version: "2.0.0"
---

# Configuracion — foltone_garage

La configuracion se divide en dos archivos: `Config.lua` (opciones generales) y `config_garage.lua` (garajes, depositos, vehiculos de servicio).

## Config.lua — Opciones generales

### Framework

```lua
Config.Framework = "esx" -- "esx", "qbcore" o "qbx"
```

| Valor | Framework | Dependencias requeridas |
|-------|-----------|----------------------|
| `"esx"` | ESX Legacy | `es_extended`, `oxmysql` |
| `"qbcore"` | QBCore | `qb-core`, `oxmysql` |
| `"qbx"` | QBX | `qbx_core`, `oxmysql` |

### Idioma

```lua
Config.Locale = "en" -- "en" o "fr"
```

Las traducciones se encuentran en `locales/en.lua` y `locales/fr.lua`. Puedes agregar tu propio idioma creando un nuevo archivo.

### Tipo de menu

```lua
Config.MenuType = "nui" -- "nui" o "rageui"
```

| Modo | Descripcion |
|------|-------------|
| `"nui"` | Panel HTML moderno con 4 pestanas (vehiculos, almacenar, deposito, etiqueta) |
| `"rageui"` | Menu clasico RageUI con 3 submenus (vehiculos, almacenar, deposito) |

> El modo `"rageui"` no soporta etiquetas personalizadas de vehiculos.

### Tipo de interaccion

```lua
Config.InteractionType = "ox_target" -- 5 opciones disponibles
```

| Modo | Descripcion | Dependencia |
|------|-------------|------------|
| `"ox_target"` | Target 3D via ox_target | `ox_target` |
| `"qb-target"` | Target 3D via qb-target | `qb-target` |
| `"interact"` | Target 3D via interact | `interact` |
| `"drawtext"` | Texto de ayuda en pantalla con tecla E | Ninguna |
| `"marker"` | Marcador en el suelo con tecla E | Ninguna |

### Distancia de interaccion

```lua
Config.InteractionDistance = 2.5
```

Distancia en metros para activar la interaccion (solo modos drawtext y marker).

### Texto de ayuda (modo drawtext)

```lua
Config.DrawText = {
    label = "interact_label", -- clave de traduccion
}
```

### Marcador (modo marker)

```lua
Config.Marker = {
    type = 1,
    scale = vector3(1.0, 1.0, 0.5),
    color = { r = 59, g = 130, b = 246, a = 120 },
}
```

| Parametro | Descripcion |
|-----------|-------------|
| `type` | Tipo de marcador GTA (1 = cilindro) |
| `scale` | Dimensiones del marcador |
| `color` | Color RGBA del marcador |

### PED

```lua
Config.Ped = {
    model = "a_m_y_business_03",
    scenario = "WORLD_HUMAN_STAND_IMPATIENT",
}
```

| Parametro | Descripcion |
|-----------|-------------|
| `model` | Modelo del PED administrador del garaje |
| `scenario` | Animacion del PED (escenario nativo de GTA) |

### Blip

```lua
Config.Blip = {
    enabled = true,
    sprite = 357,
    color = 3,
    scale = 0.7,
}
```

| Parametro | Descripcion |
|-----------|-------------|
| `enabled` | Activar/desactivar blips en el mapa |
| `sprite` | ID del sprite del blip de GTA |
| `color` | ID del color del blip de GTA |
| `scale` | Tamano del blip |

### Sistema de deposito

```lua
Config.Pound = {
    basePrice = 500,
    pricePerHour = 100,
    maxPrice = 5000,
    minPrice = 200,
}
```

| Parametro | Descripcion |
|-----------|-------------|
| `basePrice` | Precio base para recuperar un vehiculo del deposito |
| `pricePerHour` | Monto adicional por hora en el deposito |
| `maxPrice` | Precio maximo tope para la tarifa del deposito |
| `minPrice` | Precio minimo garantizado (nunca baja de este valor) |

> El precio se calcula dinamicamente segun el tiempo transcurrido desde la incautacion.

### Etiqueta personalizada

```lua
Config.Label = {
    maxLength = 30,
}
```

| Parametro | Descripcion |
|-----------|-------------|
| `maxLength` | Longitud maxima permitida para la etiqueta de un vehiculo |

---

## config_garage.lua — Garajes y depositos

### Nombres de garaje predeterminados

```lua
ConfigGarage.defaultGarageCarName = "garage"
ConfigGarage.defaultGarageBoatName = "garage_bateau1"
ConfigGarage.defaultGaragePlaneName = "garage_plane1"
ConfigGarage.defaultGarageHeliName = "garage_heli1"
```

Estos nombres corresponden a los garajes donde se colocaran los vehiculos cuando se almacenen desde un garaje con `saveGarage = false`.

### Estructura de una entrada de garaje

```lua
{
    garageName = "garage",           -- identificador unico (minusculas, sin espacios)
    garageLabel = "Downtown Garage", -- etiqueta mostrada en el menu
    saveGarage = true,               -- guardar vehiculos en este garaje en la BD
    job = nil,                       -- trabajo requerido (acceso exclusivo para este trabajo)
    job2 = nil,                      -- trabajo secundario (banda / trabajo alternativo)
    annyJob = nil,                   -- restringir acceso a CUALQUIER grado de este trabajo
    -- maxVehicles = 10,             -- limite de vehiculos (opcional, comentar para ilimitado)
    distanceStore = 25.0,            -- radio de almacenamiento en metros
    positionMenu = vector3(x, y, z), -- posicion del PED / interaccion
    spawnVehPositions = {
        vector4(x, y, z, heading),   -- posiciones de aparicion del vehiculo
    },
    storeVeh = vector3(x, y, z),     -- zona de almacenamiento del vehiculo
}
```

| Parametro | Descripcion |
|-----------|-------------|
| `garageName` | Identificador unico del garaje — debe ser unico si `saveGarage = true` |
| `garageLabel` | Nombre mostrado en la interfaz |
| `saveGarage` | Si es `true`, los vehiculos se asocian a este garaje en la BD |
| `job` | Si se define, solo los jugadores con este trabajo pueden acceder al garaje |
| `job2` | Trabajo secundario (util para bandas o trabajos duplicados) |
| `annyJob` | Restringe el acceso a cualquier grado de este trabajo (police, ambulance...) |
| `maxVehicles` | Numero maximo de vehiculos (opcional — comentar para ilimitado) |
| `distanceStore` | Distancia maxima para almacenar un vehiculo desde `storeVeh` |
| `positionMenu` | Coordenadas del punto de interaccion / PED |
| `spawnVehPositions` | Array de posiciones de aparicion (incluye heading) |
| `storeVeh` | Punto de almacenamiento del vehiculo |

### Vehiculos de servicio

Para garajes de trabajo, puedes definir vehiculos de servicio accesibles desde la pestana **Almacenar** (o el submenu correspondiente en RageUI):

```lua
serviceVehicles = {
    { model = "police",  label = "Police Cruiser" },
    { model = "police2", label = "Police Buffalo" },
},
```

> Los vehiculos de servicio solo estan disponibles para jugadores con el trabajo requerido. No se guardan en la base de datos.

### Color de blip personalizado por garaje

```lua
blipColor = 38,
color = {r = 20, g = 100, b = 80},
```

| Parametro | Descripcion |
|-----------|-------------|
| `blipColor` | Color del blip de GTA para este garaje especifico |
| `color` | Color RGB del indicador en la interfaz NUI |

### Tipos de vehiculo

Los vehiculos se organizan en 4 categorias:

| Clave | Descripcion |
|-----|-------------|
| `"car"` | Coches y motocicletas |
| `"boat"` | Barcos |
| `"plane"` | Aviones |
| `"heli"` | Helicopteros |

Cada tipo puede activarse o desactivarse:

```lua
["car"] = {
    enable = true,
    positionGarageList = { ... },
},
```

### Agregar un garaje

Agrega una entrada al array `positionGarageList` del tipo deseado:

```lua
{
    garageName = "my_garage",
    garageLabel = "My New Garage",
    saveGarage = true,
    job = nil,
    job2 = nil,
    annyJob = nil,
    distanceStore = 25.0,
    positionMenu = vector3(x, y, z),
    spawnVehPositions = {
        vector4(x, y, z, 0.0),
    },
    storeVeh = vector3(x, y, z)
},
```

---

## Depositos (poundList)

```lua
ConfigGarage.poundList = {
    ["car"] = {
        ["pound_car_1"] = {
            label = "Davis Pound",
            positionMenu = vector3(x, y, z),
            spawnVehPositions = { vector4(x, y, z, heading) },
        },
    },
    ["boat"] = { ... },
    ["plane"] = { ... },
    ["heli"] = { ... },
}
```

| Parametro | Descripcion |
|-----------|-------------|
| `label` | Nombre del deposito mostrado en la interfaz |
| `positionMenu` | Punto de interaccion / PED del deposito |
| `spawnVehPositions` | Posiciones de aparicion para los vehiculos recuperados |

### Agregar un deposito

Agrega una entrada al array del tipo de vehiculo deseado:

```lua
["pound_car_3"] = {
    label = "North Pound",
    positionMenu = vector3(x, y, z),
    spawnVehPositions = { vector4(x, y, z, 0.0) },
},
```

> La clave debe ser unica por tipo de vehiculo (ej. `"pound_car_3"`, `"pound_boat_2"`).
