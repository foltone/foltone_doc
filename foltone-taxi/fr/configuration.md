---
title: "Configuration"
description: "Configuration du script Taxi"
script: "foltone-taxi"
section: "Taxi"
order: 2
version: "2.0.0"
---

# Configuration — foltone_taxi

## Paramètres généraux

```lua
Config.JobName = 'taxi'
Config.SocietyName = 'society_taxi'
Config.EventPrefix = 'foltone_taxi'
Config.MenuSystem = 'rageui'   -- 'rageui' ou 'ox_lib'
```

## Features

```lua
Config.Features = {
    boss = true, storage = true, locker = true, garage = true,
    processing = false,   -- Pas de pipeline pour le taxi
    f6menu = true, bills = true, ads = true, duty = true,
    missions = true,      -- Système de missions NPC
}
```

## Système de missions

```lua
Config.Missions = {
    timeToFind = { 10000, 20000 },       -- Délai entre missions (ms)
    pricePerMeter = { 0.3, 0.5 },        -- Prix par mètre parcouru
    percentForSociety = 0.30,            -- 30% pour la société
    requiredDamageToPenalty = 50,         -- Seuil de dégâts pour pénalité
    vehicleDamagePenalty = { 100, 200 },  -- Montant pénalité ($)
    usePredefinedPositions = true,        -- Positions prédéfinies ou aléatoires
    pedList = { 'ig_ortega', 'ig_milton', ... },  -- Modèles de PNJ
    positionList = { vector4(...), ... },          -- Points de rendez-vous
}
```

| Paramètre | Description |
|-----------|-------------|
| `timeToFind` | Temps d'attente min/max avant une nouvelle mission |
| `pricePerMeter` | Fourchette de prix par mètre de distance |
| `percentForSociety` | Pourcentage du gain reversé à la société |
| `requiredDamageToPenalty` | Dégâts cumulés (moteur+carrosserie) déclenchant la pénalité |
| `vehicleDamagePenalty` | Fourchette du montant de pénalité |
| `usePredefinedPositions` | `true` = positions de la liste, `false` = routes aléatoires |

## Exports

```lua
-- Activer/désactiver le service (retourne le statut)
exports["foltone_taxi"]:startStopService()

-- Annuler la mission en cours
exports["foltone_taxi"]:cancelMission()
```

## Coffre

Un seul coffre principal accessible à tous les grades.

## Discord Webhooks

```lua
Config.DiscordWebhook = 'https://discord.com/api/webhooks/...'
```

Actions loguées : courses terminées, argent société, employés, duty.
