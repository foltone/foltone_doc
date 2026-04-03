---
title: "Configuration"
description: "Configuration du script Mechanic"
script: "foltone-mechanic"
section: "Mechanic"
order: 2
version: "2.0.0"
---

# Configuration — foltone_mechanic

## Paramètres généraux

```lua
Config.JobName = 'mechanic'
Config.SocietyName = 'society_mechanic'
Config.MenuSystem = 'rageui'   -- 'rageui' ou 'ox_lib'
```

## Features

```lua
Config.Features = {
    boss = true, storage = true, locker = true, garage = true,
    processing = false, f6menu = true, bills = true, ads = true,
    duty = true, customs = true, towMissions = true,
}
```

## Système de customisation

Le mechanic dispose d'un système complet de personnalisation véhicule :

### Peintures (Config.Paint)

6 catégories de peinture avec prix individuels :
- Métallique, Mat, Util, Worn, Autre, Caméléon

### Modifications (Config.Mods)

30+ types de mods véhicule : aileron, pare-chocs, capot, moteur, freins, transmission, turbo, xénon, néons, roues, etc.

### Autres options
- **XenonNeonColour** : 13 couleurs de néon
- **WheelsType** : 8 types de roues
- **WindowTint** : 6 niveaux de teinte

### Prix
- **DefaultPrice** : prix de base d'un véhicule pour le calcul
- **PriceByVehicleClass** : prix par classe de véhicule
- **CustomerPercentPriceList** : pourcentage de bénéfice (10% à 100%)

### Points de custom
```lua
Config.CustomPoints = {
    { job = "mechanic", position = vector3(268.4, -1810.62, 25.85) },
    { job = "police", position = vector3(225.63, -792.51, 30.29) },
}
```

## Missions de remorquage

```lua
Config.MissionRewardPlayer = { min = 100, max = 200 }
Config.MissionRewardSociety = { min = 100, max = 200 }
Config.Missions = { vector3(...), ... }    -- Points de spawn véhicules en panne
Config.Finishs = { vector3(...), ... }     -- Points de livraison
Config.VehiclesMission = { "rhapsody", "previon", ... }  -- Modèles de véhicules en panne
```

## Discord Webhooks

```lua
Config.DiscordWebhook = 'https://discord.com/api/webhooks/...'
```
