---
title: "Configuration"
description: "Guide de configuration du script foltone_shoprobbery"
script: "foltone-shoprobbery"
section: "Shop Robbery"
order: 2
version: "1.0.0"
---

# Configuration de foltone_shoprobbery

## Fichier de configuration

Toute la configuration se fait dans le fichier `config.lua`.

## Positions des boutiques

```lua
Config.Shops = {
    {
        coords = vector3(25.7, -1347.3, 29.5),
        robbable = true,
        blip = true,
    },
    -- Ajoutez autant de boutiques que souhaite
}
```

Chaque boutique peut etre definie comme braquable ou non.

## Parametres du braquage

```lua
Config.Robbery = {
    amount = {min = 500, max = 2000},
    requiredPolice = 2,
    cooldown = 1200, -- secondes (20 minutes)
    duration = 15000, -- duree du braquage en ms
}
```

| Parametre | Description |
|-----------|-------------|
| `amount` | Fourchette d'argent recupere lors du braquage |
| `requiredPolice` | Nombre minimum de policiers en service |
| `cooldown` | Temps d'attente entre deux braquages de la meme boutique |
| `duration` | Duree de la barre de progression du braquage |

## Conditions d'annulation

Le braquage est automatiquement annule si :
- Le joueur se deplace pendant le braquage
- Le PNJ vendeur meurt

## Articles de la boutique

```lua
Config.ShopItems = {
    { item = "bread", label = "Pain", price = 10 },
    { item = "water", label = "Eau", price = 5 },
    -- Ajoutez vos articles ici
}
```

## Notifications police

```lua
Config.PoliceNotification = function(source, coords)
    -- Personnalisez ici l'envoi de notification
    -- Inclut la photo du suspect et la geolocalisation
end
```

Adaptez cette fonction pour votre systeme de dispatch. La notification inclut automatiquement une photo du suspect et la position GPS de la boutique.
