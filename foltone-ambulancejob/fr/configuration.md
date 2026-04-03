---
title: "Configuration"
description: "Configuration du script Ambulance"
script: "foltone-ambulancejob"
section: "Ambulance"
order: 2
version: "2.0.0"
---

# Configuration — foltone_advanced_ambulancejob

## Paramètres généraux

```lua
Config.JobName = 'ambulance'
Config.SocietyName = 'society_ambulance'
Config.MenuSystem = 'rageui'
```

## Features

```lua
Config.Features = {
    boss = true, storage = true, locker = true, garage = true,
    f6menu = true, bills = true, duty = true, ambulance = true,
}
```

## Système de mort

```lua
Config.FirstTimer = 5 * 60       -- 5 minutes avant le bouton "appeler les secours"
Config.SecondTimer = 10 * 60     -- 10 minutes avant le respawn automatique
Config.KillPlayerLeaveServer = true
Config.RespawnPosition = vector3(355.72, -596.24, 28.77)
Config.RespawnHeading = 270.0
```

### Pénalités au respawn
```lua
Config.ClearItemsAfterRevive = true
Config.ClearMoneyAfterRevive = true
Config.ClearBlackMoneyAfterRevive = true
Config.ClearWeaponsAfterRevive = true
```

## Soins

```lua
Config.TimeHealAnim = 5000       -- Durée animation soin léger (ms)
Config.TimeBigHealAnim = 5000    -- Durée animation soin complet (ms)
Config.TimeReviveAnim = 5000     -- Durée animation réanimation (ms)
```

## Props

```lua
Config.PropsList = {
    { prop = "prop_ld_health_pack", label = "Medikit", freeze = false },
    { prop = "prop_roadcone02a", label = "Plot", freeze = false },
    { prop = "prop_barrier_work06a", label = "Barrier", freeze = false },
}
```

## Brancards

3 types de brancards avec 3 positions chacun (haut, bas, assis) :
- **Plan dur** : combicarrier2
- **Brancard 1** : fernocot (avec animations)
- **Brancard 2** : strykergurney (avec animations)

Chaque brancard a une position de prise (`takePos`), une position du patient (`onPos`), et des animations.

## Pharmacie

```lua
Config.Pharmacie = {
    menuPosition = vector3(306.67, -601.67, 42.28),
    itemList = {
        ["medikit"] = { label = "Medikit", max = 10 },
        ["band"] = { label = "Bandage", max = 15 },
    },
}
```

## Garage hélicoptère

Garage séparé pour les hélicoptères avec spawn sur le toit de l'hôpital.

## Discord Webhooks

```lua
Config.DiscordWebhook = 'https://discord.com/api/webhooks/...'
```
