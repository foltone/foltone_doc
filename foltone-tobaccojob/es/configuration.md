---
title: "Configuracion"
description: "Guia de configuracion del script foltone_tobaccojob"
script: "foltone-tobaccojob"
section: "Tobacco Job"
order: 2
version: "1.0.0"
---

# Configuracion

Todos los parametros configurables se encuentran en la carpeta `shared/`.

## Configuracion general

### Nombre del empleo

```lua
Config.JobName = 'tobaccojob'
Config.SocietyName = 'society_tobaccojob'
```

- `JobName`: debe coincidir con el nombre del empleo en la base de datos.
- `SocietyName`: nombre de la cuenta de sociedad utilizada por esx_addonaccount.

### Blip del mapa

```lua
Config.Blip = {
    enabled = true,
    coords = vector3(x, y, z),
    sprite = 365,
    scale = 0.8,
    color = 2,
    label = "Tabaco"
}
```

## Pipeline de produccion

El script sigue un pipeline de 3 pasos: **Cosecha -> Transformacion -> Venta**.

### Cosecha (Harvest)

```lua
Config.Harvest = {
    coords = vector3(x, y, z),
    item = 'tobacco_leaf',
    amount = 1,
    time = 5000, -- milisegundos
    animation = { dict = "anim@dict", name = "anim_name" }
}
```

### Transformacion (Processing)

```lua
Config.Processing = {
    coords = vector3(x, y, z),
    recipes = {
        {
            input = { item = 'tobacco_leaf', amount = 3 },
            output = { item = 'cigarettes', amount = 1 },
            time = 8000
        }
    }
}
```

### Venta (Sell)

```lua
Config.Sell = {
    coords = vector3(x, y, z),
    items = {
        { item = 'cigarettes', price = 50 }
    }
}
```

## Menu de jefe

```lua
Config.BossMenu = {
    coords = vector3(x, y, z),
    grade = 'boss' -- grado minimo para acceder al menu
}
```

El menu de jefe permite:
- Gestion de empleados (contratar, despedir, promover)
- Gestion de salarios por grado
- Gestion de uniformes por grado
- Acceso al almacen de sociedad y cuenta bancaria

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
        { model = 'mule', label = 'Mule', grade = 0 }
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
    blip = true
}
```

Desactive cualquier funcionalidad que no necesite cambiando su valor a `false`.
