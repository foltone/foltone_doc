---
title: "Configuration"
description: "Guide de configuration du script foltone_tobaccojob"
script: "foltone-tobaccojob"
section: "Tobacco Job"
order: 2
version: "1.0.0"
---

# Configuration

Tous les parametres configurables se trouvent dans le dossier `shared/`.

## Configuration generale

### Nom du metier

```lua
Config.JobName = 'tobaccojob'
Config.SocietyName = 'society_tobaccojob'
```

- `JobName` : doit correspondre au nom du job dans la base de donnees.
- `SocietyName` : nom du compte societe utilise par esx_addonaccount.

### Blip carte

```lua
Config.Blip = {
    enabled = true,
    coords = vector3(x, y, z),
    sprite = 365,
    scale = 0.8,
    color = 2,
    label = "Tabac"
}
```

## Pipeline de production

Le script suit un pipeline en 3 etapes : **Recolte -> Transformation -> Vente**.

### Recolte (Harvest)

```lua
Config.Harvest = {
    coords = vector3(x, y, z),
    item = 'tobacco_leaf',
    amount = 1,
    time = 5000, -- millisecondes
    animation = { dict = "anim@dict", name = "anim_name" }
}
```

### Transformation (Processing)

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

### Vente (Sell)

```lua
Config.Sell = {
    coords = vector3(x, y, z),
    items = {
        { item = 'cigarettes', price = 50 }
    }
}
```

## Menu Boss

```lua
Config.BossMenu = {
    coords = vector3(x, y, z),
    grade = 'boss' -- grade minimum pour acceder au menu
}
```

Le menu boss permet de :
- Gerer les employes (embaucher, licencier, promouvoir)
- Gerer les salaires par grade
- Gerer les tenues par grade
- Acceder au coffre societe et au compte en banque

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
        { model = 'mule', label = 'Mule', grade = 0 }
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
    blip = true
}
```

Desactivez les fonctionnalites que vous ne souhaitez pas utiliser en passant la valeur a `false`.
