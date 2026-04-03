---
title: "Configuration"
description: "Configuration du script Vigneron"
script: "foltone-vigneron"
section: "Vigneron"
order: 2
version: "2.0.0"
---

# Configuration — foltone_vigneron

Toute la configuration se fait dans le fichier `config.lua` à la racine du script.

## Paramètres généraux

```lua
Config.Debug = false
Config.Locale = 'fr'                       -- 'fr' ou 'en'
Config.EventPrefix = 'foltone_vigneron'
Config.JobName = 'vigne'                   -- Nom du job en BDD
Config.SocietyName = 'society_vigne'
Config.DiscordWebhook = ''                 -- URL webhook Discord (vide = désactivé)
Config.KeyJobMenu = 'F6'
```

## Système de menus

```lua
Config.MenuSystem = 'rageui'   -- 'rageui' ou 'ox_lib'
```

| Valeur | Description |
|--------|-------------|
| `'rageui'` | Menus RageUI classiques (inclus dans le script) |
| `'ox_lib'` | Context menus ox_lib |

## Features activables

```lua
Config.Features = {
    boss = true,        -- Menu patron
    storage = true,     -- Coffres de société
    locker = true,      -- Vestiaire
    garage = true,      -- Garage véhicules
    processing = true,  -- Pipeline récolte/transformation/vente
    f6menu = true,      -- Menu F6
    bills = true,       -- Facturation
    ads = true,         -- Annonces
    duty = true,        -- Prise de service
}
```

## Multi-coffres

Plusieurs coffres avec permissions par grade. Chaque coffre peut utiliser ox_inventory :

```lua
Config.Storages = {
    {
        id = 'society_vigne',
        label = 'Coffre Principal',
        position = vector3(-1886.44, 2062.34, 139.98),
        gradeRequired = 0,
        blip = { sprite = 814, color = 7 },
        oxStash = {
            id = 'foltone_vigne_main',
            label = 'Coffre Principal Vigneron',
            slots = 50, weight = 100000,
        },
    },
}
```

| Paramètre | Description |
|-----------|-------------|
| `id` | Identifiant unique (esx_addoninventory) |
| `label` | Nom affiché |
| `gradeRequired` | Grade minimum (0 = tous) |
| `oxStash` | Config stash ox_inventory (optionnel) |

## Pipeline de récolte

```lua
Config.ProcessingList = {
    { type = 'harvest', itemName = 'grapes', max = 200, duration = 3000, ... },
    { type = 'transform', itemName = 'grapes_juice', itemNameNeeded = 'grapes', itemNameNeededCount = 1, ... },
    { type = 'sell', itemName = 'wine', playerMoney = 15, societyMoney = 40, ... },
}
```

| Type | Description |
|------|-------------|
| `harvest` | Récolte un item |
| `transform` | Consomme des items pour en produire un autre |
| `sell` | Vend un item (argent joueur + société) |

## Discord Webhooks

```lua
Config.DiscordWebhook = 'https://discord.com/api/webhooks/...'
```

Actions loguées : récolte, transformation, vente, argent société, employés, salaires, duty.
