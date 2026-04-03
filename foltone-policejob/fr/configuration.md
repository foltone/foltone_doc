---
title: "Configuration"
description: "Configuration du script Police"
script: "foltone-policejob"
section: "Police"
order: 2
version: "2.0.0"
---

# Configuration — foltone_policejob

## Paramètres généraux

```lua
Config.JobName = 'police'
Config.SocietyName = 'society_police'
Config.MenuSystem = 'rageui'
```

## Features

```lua
Config.Features = {
    boss = true, storage = true, locker = true, garage = true,
    f6menu = true, bills = true, duty = true, police = true,
}
```

## Features police spécifiques

### K9

```lua
Config.K9DogModel = "a_c_rottweiler"
```

### Props (objets posables)

```lua
Config.PropsList = {
    { prop = "prop_roadcone02a", label = "Plot", freeze = false },
    { prop = "prop_barrier_work06a", label = "Barrier", freeze = false },
    { prop = "prop_gazebo_03", label = "Gazebo", freeze = true },
}
```

### Armurerie

```lua
Config.Armory = {
    menuPosition = vector3(479.15, -996.59, 29.69),
    itemsList = {
        { type = "item", grade = 1, name = "armor", label = "Gilet par balle" },
        { type = "weapon", grade = 1, name = "WEAPON_PISTOL", label = "Pistolet" },
        { type = "weapon", grade = 3, name = "WEAPON_CARBINERIFLE", label = "Carabine" },
    },
}
```

### Système de prison (Jail)

```lua
Config.Jail = {
    exitCellsCoords = vector3(488.76, -1002.48, 28.01),
    cells = { vector3(...), ... },
    jailPosition = vector3(1644.77, 2537.45, 45.56),
    exitPrisonCoords = vector3(1846.72, 2585.62, 45.67),
    MaleClothes = { ... },
    FemaleClothes = { ... },
}
```

### Amendes catégorisées

5 catégories : Délit routier, Délit mineur, Délit majeur, Infraction administrative, Infraction environnementale. Chaque amende a un label et un montant.

### Codes radio

```lua
Config.Calls = { { title = "~b~Prise de service", message = "Code: 10-8..." }, ... }
Config.Helps = { { title = "~g~Demande de renforts", blip = {...} }, ... }
```

### Garage hélicoptère

Garage séparé pour les hélicoptères avec spawn sur le toit.

## Discord Webhooks

```lua
Config.DiscordWebhook = 'https://discord.com/api/webhooks/...'
```
