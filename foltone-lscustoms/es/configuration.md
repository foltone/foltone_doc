---
title: "Configuracion"
description: "Guia de configuracion del script foltone_lscustoms"
script: "foltone-lscustoms"
section: "LS Customs"
order: 2
version: "1.0.0"
---

# Configuracion de foltone_lscustoms

## Archivo de configuracion

Toda la configuracion se realiza en `config.lua`.

## Posicion del menu

```lua
Config.MenuPosition = "right" -- "left" o "right"
```

## Precios de modificaciones

### Pintura

```lua
Config.Prices.Paint = {
    primary = 500,
    secondary = 500,
    pearlescent = 750,
    wheels = 300,
}
```

### Mejoras de rendimiento

```lua
Config.Prices.Performance = {
    engine = 2500,
    brakes = 1500,
    transmission = 2000,
    suspension = 1200,
    turbo = 5000,
}
```

### Modificaciones esteticas

```lua
Config.Prices.Aesthetic = {
    spoiler = 800,
    bumper_front = 600,
    bumper_rear = 600,
    skirts = 500,
    exhaust = 400,
    grille = 350,
    hood = 700,
    roof = 500,
    wheels = 1000,
    xenon = 300,
    plate = 200,
    horn = 150,
    windows = 400,
}
```

### Reparacion y limpieza

```lua
Config.Prices.Repair = 500
Config.Prices.Clean = 100
```

## Misiones de remolque NPC

```lua
Config.Towing = {
    reward = {min = 300, max = 800},
    cooldown = 300, -- segundos
    maxDistance = 500.0, -- distancia maxima de la mision
}
```

## Sistema de facturas

```lua
Config.Invoice = {
    enabled = true,
    maxAmount = 50000,
}
```

Permite a los jugadores enviar facturas a otros jugadores por trabajos realizados.
