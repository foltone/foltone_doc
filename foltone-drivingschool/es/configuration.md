---
title: "Configuracion"
description: "Guia de configuracion del script foltone_drivingschool"
script: "foltone-drivingschool"
section: "Driving School"
order: 2
version: "1.0.0"
---

# Configuracion

Toda la configuracion se realiza en el archivo `config.lua`.

## Parametros generales

```lua
Config.Locale = 'es'
Config.PedModel = 's_m_y_cop_01'       -- Modelo del NPC instructor
Config.SchoolLocation = vector3(228.46, -1394.87, 30.59) -- Ubicacion de la autoescuela
```

## Blip en el mapa

```lua
Config.Blip = {
    sprite = 545,
    color = 3,
    scale = 0.8,
    label = "Autoescuela"
}
```

## Tipos de examenes

### Examen teorico (NUI)

```lua
Config.TheoryExam = {
    passingScore = 80,          -- Puntuacion minima para aprobar (%)
    questionsPerExam = 20,      -- Preguntas por examen
    timePerQuestion = 30,       -- Tiempo por pregunta (segundos)
    price = 500,                -- Precio del examen
}
```

### Preguntas de examen

```lua
Config.Questions = {
    {
        question = "Cual es el limite de velocidad en zona urbana?",
        answers = { "30 km/h", "50 km/h", "70 km/h", "90 km/h" },
        correct = 2,  -- Indice de la respuesta correcta
    },
    {
        question = "Que significa un semaforo en ambar?",
        answers = { "Acelerar", "Detenerse si es posible", "Prioridad", "Reducir velocidad" },
        correct = 2,
    },
    -- Agregue tantas preguntas como necesite...
}
```

## Examenes practicos

### Examen de coche

```lua
Config.CarExam = {
    license = "drive",
    vehicle = "sultan",           -- Modelo del vehiculo
    price = 1500,                 -- Precio del examen
    maxErrors = 3,                -- Errores maximos antes de reprobar
    speedLimit = 80,              -- Limite de velocidad (km/h)
    checkpoints = {
        vector3(230.0, -1390.0, 30.0),
        vector3(250.0, -1350.0, 30.0),
        -- Agregue puntos de control...
    },
}
```

### Examen de moto

```lua
Config.BikeExam = {
    license = "drive_bike",
    vehicle = "bati",
    price = 1000,
    maxErrors = 3,
    speedLimit = 90,
    checkpoints = { --[[ ... ]] },
}
```

### Examen de camion

```lua
Config.TruckExam = {
    license = "drive_truck",
    vehicle = "mule",
    price = 3000,
    maxErrors = 2,
    speedLimit = 60,
    checkpoints = { --[[ ... ]] },
}
```

### Criterios de error

Los errores se cuentan por:

| Infraccion | Errores |
|---|---|
| Exceso de velocidad | +1 |
| Colision con vehiculo | +1 |
| Colision con peaton | +2 (reprobado inmediato) |
| Punto de control perdido | +1 |
| Vehiculo danado (umbral) | +1 |

## Notificaciones

```lua
Config.Notification = function(msg)
    ESX.ShowNotification(msg)
end
```
