---
title: "Configuration"
description: "Guide de configuration du script foltone_lscustoms"
script: "foltone-lscustoms"
section: "LS Customs"
order: 2
version: "1.0.0"
---

# Configuration de foltone_lscustoms

## Fichier de configuration

Toute la configuration se fait dans le fichier `config.lua`.

## Position du menu

```lua
Config.MenuPosition = "right" -- "left" ou "right"
```

## Prix des modifications

### Peinture

```lua
Config.Prices.Paint = {
    primary = 500,
    secondary = 500,
    pearlescent = 750,
    wheels = 300,
}
```

### Modifications mecaniques

```lua
Config.Prices.Performance = {
    engine = 2500,
    brakes = 1500,
    transmission = 2000,
    suspension = 1200,
    turbo = 5000,
}
```

### Modifications esthetiques

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

### Reparation et nettoyage

```lua
Config.Prices.Repair = 500
Config.Prices.Clean = 100
```

## Missions de depannage NPC

```lua
Config.Towing = {
    reward = {min = 300, max = 800},
    cooldown = 300, -- secondes
    maxDistance = 500.0, -- distance max de la mission
}
```

## Systeme de factures

```lua
Config.Invoice = {
    enabled = true,
    maxAmount = 50000,
}
```

Permet aux joueurs d'envoyer des factures a d'autres joueurs pour des travaux effectues.
