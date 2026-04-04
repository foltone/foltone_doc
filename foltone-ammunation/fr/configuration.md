---
title: "Configuration"
description: "Guide de configuration du script foltone_ammunation"
script: "foltone-ammunation"
section: "Ammunation"
order: 2
version: "1.0.0"
---

# Configuration

Toute la configuration se fait dans le fichier `config.lua`.

## Parametres generaux

```lua
Config.Locale = 'fr'           -- Langue (fr, en, es)
Config.PedModel = 's_m_y_ammucity_01' -- Modele du PNJ vendeur
```

## Blip sur la carte

```lua
Config.AmmunationBlip = {
    sprite = 110,    -- Icone du blip
    color = 1,       -- Couleur (1 = rouge)
    scale = 0.8      -- Taille du blip
}
```

## Systeme de licence

```lua
Config.LicensePrice = 5000  -- Prix de la licence d'arme ($)
```

Les armes necessitant une licence sont marquees avec `RequireLicense = true` dans la configuration des rayons.

## Rayons et produits

```lua
Config.AisleProductList = {
    {
        label = "Armes de poing",
        RequireLicense = true,
        items = {
            { name = "WEAPON_PISTOL", label = "Pistolet", price = 2500, type = "weapon" },
            { name = "WEAPON_COMBATPISTOL", label = "Pistolet de combat", price = 3500, type = "weapon" },
        }
    },
    {
        label = "Munitions",
        RequireLicense = false,
        items = {
            { name = "ammo_pistol", label = "Munitions pistolet", price = 100, type = "item" },
        }
    },
}
```

### Parametres des produits

| Parametre | Type | Description |
|---|---|---|
| `name` | string | Nom technique de l'arme/item |
| `label` | string | Nom affiche dans le menu |
| `price` | number | Prix de vente |
| `type` | string | `"weapon"` ou `"item"` |

## Positions des magasins

```lua
Config.AmmunationsList = {
    vector4(-662.18, -935.3, 21.83, 174.89),
    vector4(810.25, -2157.6, 29.62, 0.72),
    -- Ajoutez d'autres positions...
}
```

## Braquage

```lua
Config.RobberyMinPolice = 2       -- Nombre minimum de policiers en service
Config.RobberyCooldown = 1800     -- Cooldown entre braquages (secondes)
Config.RobberyMinAmount = 5000    -- Montant minimum du braquage
Config.RobberyMaxAmount = 15000   -- Montant maximum du braquage
Config.RobberyDistance = 3.0      -- Distance max avant annulation
```

> Le braquage est annule si le joueur s'eloigne trop du PNJ ou si le PNJ meurt.

## Notifications

```lua
Config.Notification = function(msg)
    -- Personnalisez votre systeme de notification
    ESX.ShowNotification(msg)
end

Config.DisplayHelpText = function(msg)
    -- Texte d'aide contextuel
    SetTextComponentFormat("STRING")
    AddTextComponentString(msg)
    DisplayHelpTextFromStringLabel(0, 0, 1, -1)
end
```

## Alertes police

Lors d'un braquage, les policiers recoivent :
- Photo du suspect (mugshot)
- Geolocalisation du magasin braque
- Notification sonore
