---
title: "Configuration"
description: "Guide de configuration du script foltone_vehicleitem"
script: "foltone-vehicleitem"
section: "Vehicle Item"
order: 2
version: "1.0.0"
---

# Configuration

Tous les parametres configurables se trouvent dans le dossier `shared/`.

## Liste des vehicules

Configurez les vehicules disponibles a l'achat :

```lua
Config.Vehicles = {
    {
        model = 'bmx',
        label = 'BMX',
        item = 'bmx_item',
        price = 500
    },
    {
        model = 'cruiser',
        label = 'Cruiser',
        item = 'cruiser_item',
        price = 800
    },
    {
        model = 'scorcher',
        label = 'Scorcher',
        item = 'scorcher_item',
        price = 1000
    }
}
```

### Parametres de chaque vehicule

| Parametre | Type   | Description                                       |
|-----------|--------|---------------------------------------------------|
| `model`   | string | Nom du modele GTA (spawn name)                    |
| `label`   | string | Nom affiche dans le menu                          |
| `item`    | string | Nom de l'item dans la base de donnees             |
| `price`   | number | Prix d'achat en dollars                           |

Chaque `item` doit correspondre a une entree dans la table `items` de votre base de donnees.

## Position de la boutique

```lua
Config.Shop = {
    coords = vector3(x, y, z),
    heading = 0.0,
    blip = {
        enabled = true,
        sprite = 226,
        scale = 0.8,
        color = 3,
        label = "Vehicules"
    },
    ped = {
        model = 's_m_y_shop_mid',
        heading = 0.0
    }
}
```

## Parametres de spawn

```lua
Config.Spawn = {
    offset = vector3(2.0, 0.0, 0.0), -- decalage par rapport au joueur
    deleteOnStore = true -- supprimer le vehicule quand il est range
}
```

### Options de spawn

- `offset` : position relative au joueur ou le vehicule apparait.
- `deleteOnStore` : si `true`, le vehicule est supprime du monde quand le joueur le range (le remet en item).

## Parametres divers

```lua
Config.UseRageUI = true -- utiliser RageUI pour les menus
Config.Locale = 'fr' -- langue par defaut
```
