---
title: "Configuration"
description: "Guide de configuration du script foltone_unicornjob"
script: "foltone-unicornjob"
section: "Unicorn Job"
order: 2
version: "1.0.0"
---

# Configuration

Tous les parametres configurables se trouvent dans le dossier `shared/`.

## Configuration generale

### Nom du metier

```lua
Config.JobName = 'unicorn'
Config.SocietyName = 'society_unicorn'
```

### Blip carte

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

## Service au bar

Configurez les items disponibles au bar :

```lua
Config.BarItems = {
    { item = 'beer', label = 'Biere', price = 10 },
    { item = 'wine', label = 'Vin', price = 15 },
    { item = 'cocktail', label = 'Cocktail', price = 25 },
    { item = 'whiskey', label = 'Whiskey', price = 30 },
    { item = 'water', label = 'Eau', price = 5 }
}
```

Chaque item doit exister dans votre table `items` de la base de donnees.

## Systeme de farming

Configurez les points de farming pour les ingredients :

```lua
Config.FarmingPoints = {
    {
        coords = vector3(x, y, z),
        item = 'hops',
        label = 'Houblon',
        amount = 1,
        time = 5000,
        animation = { dict = "anim@dict", name = "anim_name" }
    },
    {
        coords = vector3(x, y, z),
        item = 'grape',
        label = 'Raisin',
        amount = 1,
        time = 5000
    }
}
```

## Menu Boss

```lua
Config.BossMenu = {
    coords = vector3(x, y, z),
    grade = 'boss'
}
```

Fonctionnalites du menu boss :
- Gestion des employes (embauche, licenciement, promotion)
- Gestion des salaires par grade
- Gestion des tenues par grade
- Coffre et compte bancaire de societe

## Stockage et vestiaire

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

## Garage

```lua
Config.Garage = {
    coords = vector3(x, y, z),
    spawnPoint = vector4(x, y, z, heading),
    vehicles = {
        { model = 'speedo', label = 'Speedo', grade = 0 }
    }
}
```

## Features toggle

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
