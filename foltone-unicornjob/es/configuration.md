---
title: "Configuracion"
description: "Guia de configuracion del script foltone_unicornjob"
script: "foltone-unicornjob"
section: "Unicorn Job"
order: 2
version: "1.0.0"
---

# Configuracion

Todos los parametros configurables se encuentran en la carpeta `shared/`.

## Configuracion general

### Nombre del empleo

```lua
Config.JobName = 'unicorn'
Config.SocietyName = 'society_unicorn'
```

### Blip del mapa

```lua
Config.Blip = {
    enabled = true,
    coords = vector3(x, y, z),
    sprite = 93,
    scale = 0.8,
    color = 27,
    label = "Unicorn"
}
```

## Servicio de bar

Configure los items disponibles en el bar:

```lua
Config.BarItems = {
    { item = 'beer', label = 'Cerveza', price = 10 },
    { item = 'wine', label = 'Vino', price = 15 },
    { item = 'cocktail', label = 'Coctel', price = 25 },
    { item = 'whiskey', label = 'Whiskey', price = 30 },
    { item = 'water', label = 'Agua', price = 5 }
}
```

Cada item debe existir en su tabla `items` de la base de datos.

## Sistema de farming

Configure los puntos de farming para ingredientes:

```lua
Config.FarmingPoints = {
    {
        coords = vector3(x, y, z),
        item = 'hops',
        label = 'Lupulo',
        amount = 1,
        time = 5000,
        animation = { dict = "anim@dict", name = "anim_name" }
    },
    {
        coords = vector3(x, y, z),
        item = 'grape',
        label = 'Uva',
        amount = 1,
        time = 5000
    }
}
```

## Menu de jefe

```lua
Config.BossMenu = {
    coords = vector3(x, y, z),
    grade = 'boss'
}
```

Funcionalidades del menu de jefe:
- Gestion de empleados (contratar, despedir, promover)
- Gestion de salarios por grado
- Gestion de uniformes por grado
- Almacen de sociedad y cuenta bancaria

## Almacen y vestuario

```lua
Config.Storage = {
    coords = vector3(x, y, z),
    slots = 50,
    weight = 100000
}

Config.Locker = {
    coords = vector3(x, y, z)
}
```

## Garaje

```lua
Config.Garage = {
    coords = vector3(x, y, z),
    spawnPoint = vector4(x, y, z, heading),
    vehicles = {
        { model = 'speedo', label = 'Speedo', grade = 0 }
    }
}
```

## Activacion de funcionalidades

```lua
Config.Features = {
    garage = true,
    locker = true,
    storage = true,
    bossMenu = true,
    blip = true,
    farming = true,
    barService = true
}
```
