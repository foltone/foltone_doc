---
title: "Configuration"
description: "Guide de configuration du script foltone_baginventory"
script: "foltone-baginventory"
section: "Bag Inventory"
order: 2
version: "1.0.0"
---

# Configuration

Toute la configuration se fait dans le fichier `config.lua`.

## Types de sacs

```lua
Config.BagTypes = {
    ['bag_small'] = {
        label = "Petit sac",
        model = 'prop_cs_heist_bag_01',
        weight = 10,       -- Poids maximum du contenu (kg)
        slots = 5,         -- Nombre d'emplacements
    },
    ['bag_medium'] = {
        label = "Sac moyen",
        model = 'prop_poly_bag_01',
        weight = 25,
        slots = 10,
    },
    ['bag_large'] = {
        label = "Grand sac",
        model = 'prop_michael_backpack',
        weight = 50,
        slots = 20,
    },
}
```

### Parametres de chaque sac

| Parametre | Type | Description |
|---|---|---|
| `label` | string | Nom affiche |
| `model` | string | Modele 3D du sac au sol |
| `weight` | number | Capacite maximale en poids |
| `slots` | number | Nombre d'emplacements disponibles |

## Comportement a la mort

```lua
Config.DropOnDeath = true    -- Les sacs tombent au sol a la mort du joueur
Config.DropAllBags = true    -- Lacher tous les sacs (true) ou seulement celui equipe (false)
```

## Placement au sol

```lua
Config.PlaceDistance = 2.0   -- Distance de placement du sac au sol
Config.PickupDistance = 2.0  -- Distance pour ramasser un sac
```

## Notifications

```lua
Config.Notification = function(msg)
    ESX.ShowNotification(msg)
end
```

## Parametres generaux

```lua
Config.Locale = 'fr'              -- Langue
Config.FoldBagItem = true         -- Permettre de plier le sac pour le ranger
Config.MaxBagsPerPlayer = 3       -- Nombre max de sacs par joueur
```
