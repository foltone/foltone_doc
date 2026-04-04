---
title: "Configuration"
description: "Guide de configuration du script foltone_territories"
script: "foltone-territories"
section: "Territories"
order: 2
version: "1.0.0"
---

# Configuration de foltone_territories

## Fichier de configuration

Toute la configuration se fait dans le fichier `config.lua`.

## Definition des zones

```lua
Config.Zones = {
    {
        name = "Grove Street",
        position = vector3(95.0, -1960.0, 21.0),
        width = 200.0,
        height = 200.0,
        rotation = 0.0,
        capturePoints = 100, -- points necessaires pour capturer
    },
    -- Ajoutez autant de zones que souhaite
}
```

| Parametre | Description |
|-----------|-------------|
| `name` | Nom affiche de la zone |
| `position` | Coordonnees du centre de la zone |
| `width` | Largeur de la zone |
| `height` | Hauteur de la zone |
| `rotation` | Rotation de la zone en degres |
| `capturePoints` | Nombre de points necessaires pour capturer la zone |

## Liste des drogues

```lua
Config.Drugs = {
    {
        item = "weed",
        label = "Cannabis",
        price = 50,
        capturePoints = 5,
        acceptRate = 0.6, -- 60% de chance d'accepter
        rejectRate = 0.3, -- 30% de chance de refuser
        -- 10% restant = appel police
    },
    {
        item = "coke",
        label = "Cocaine",
        price = 120,
        capturePoints = 10,
        acceptRate = 0.4,
        rejectRate = 0.4,
    },
}
```

| Parametre | Description |
|-----------|-------------|
| `item` | Nom de l'item dans l'inventaire |
| `price` | Prix de vente au PNJ |
| `capturePoints` | Points de capture gagnes par vente |
| `acceptRate` | Probabilite que le PNJ accepte |
| `rejectRate` | Probabilite que le PNJ refuse |

La probabilite restante (1 - acceptRate - rejectRate) correspond a la chance que le PNJ appelle la police.

## Jobs de police

```lua
Config.PoliceJobs = {"police", "fbi", "sheriff"}
```

Liste des jobs consideres comme forces de l'ordre pour les alertes.

## PNJ exclus

```lua
Config.BlacklistedPeds = {
    "s_m_y_cop_01",
    "s_f_y_cop_01",
    -- PNJ auxquels on ne peut pas vendre
}
```

## Zones de gang

```lua
Config.GangJobs = {"ballas", "vagos", "families", "lost"}
```

Seuls les joueurs ayant un de ces jobs peuvent participer au systeme de territoires.
