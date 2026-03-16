---
title: "Configuration"
description: "Configuration du script Foltone Garage"
script: "foltone-garage"
section: "Foltone Garage"
order: 2
version: "2.0.0"
---

# Configuration — foltone_garage

La configuration se repartit sur deux fichiers : `Config.lua` (options generales) et `config_garage.lua` (garages, fourrieres, vehicules de service).

## Config.lua — Options generales

### Framework

```lua
Config.Framework = "esx" -- "esx", "qbcore" ou "qbx"
```

| Valeur | Framework | Dependances requises |
|--------|-----------|---------------------|
| `"esx"` | ESX Legacy | `es_extended`, `oxmysql` |
| `"qbcore"` | QBCore | `qb-core`, `oxmysql` |
| `"qbx"` | QBX | `qbx_core`, `oxmysql` |

### Langue

```lua
Config.Locale = "en" -- "en" ou "fr"
```

Les traductions se trouvent dans `locales/en.lua` et `locales/fr.lua`. Vous pouvez ajouter votre propre langue en creant un nouveau fichier.

### Mode de menu

```lua
Config.MenuType = "nui" -- "nui" ou "rageui"
```

| Mode | Description |
|------|-------------|
| `"nui"` | Panel HTML moderne avec 4 onglets (vehicules, ranger, fourriere, label) |
| `"rageui"` | Menu RageUI classique avec 3 sous-menus (vehicules, ranger, fourriere) |

> Le mode `"rageui"` ne supporte pas les labels personnalises.

### Mode d'interaction

```lua
Config.InteractionType = "ox_target" -- 5 options disponibles
```

| Mode | Description | Dependance |
|------|-------------|------------|
| `"ox_target"` | Cible 3D via ox_target | `ox_target` |
| `"qb-target"` | Cible 3D via qb-target | `qb-target` |
| `"interact"` | Cible 3D via interact | `interact` |
| `"drawtext"` | Texte d'aide a l'ecran avec touche E | Aucune |
| `"marker"` | Marqueur au sol avec touche E | Aucune |

### Distance d'interaction

```lua
Config.InteractionDistance = 2.5
```

Distance en metres pour declencher l'interaction (drawtext et marker uniquement).

### Texte d'aide (drawtext)

```lua
Config.DrawText = {
    label = "interact_label", -- cle de locale
}
```

### Marqueur (marker)

```lua
Config.Marker = {
    type = 1,
    scale = vector3(1.0, 1.0, 0.5),
    color = { r = 59, g = 130, b = 246, a = 120 },
}
```

| Parametre | Description |
|-----------|-------------|
| `type` | Type de marqueur GTA (1 = cylindre) |
| `scale` | Dimensions du marqueur |
| `color` | Couleur RGBA du marqueur |

### PED

```lua
Config.Ped = {
    model = "a_m_y_business_03",
    scenario = "WORLD_HUMAN_STAND_IMPATIENT",
}
```

| Parametre | Description |
|-----------|-------------|
| `model` | Modele du PED gestionnaire de garage |
| `scenario` | Animation du PED (scenario GTA natif) |

### Blip

```lua
Config.Blip = {
    enabled = true,
    sprite = 357,
    color = 3,
    scale = 0.7,
}
```

| Parametre | Description |
|-----------|-------------|
| `enabled` | Activer/desactiver les blips sur la carte |
| `sprite` | ID du sprite blip GTA |
| `color` | ID de couleur du blip |
| `scale` | Taille du blip |

### Systeme de fourriere

```lua
Config.Pound = {
    basePrice = 500,
    pricePerHour = 100,
    maxPrice = 5000,
    minPrice = 200,
}
```

| Parametre | Description |
|-----------|-------------|
| `basePrice` | Prix de base pour recuperer un vehicule en fourriere |
| `pricePerHour` | Montant supplementaire par heure passee en fourriere |
| `maxPrice` | Plafond maximum du prix de fourriere |
| `minPrice` | Prix minimum garanti (ne descend pas en dessous) |

> Le prix est calcule dynamiquement en fonction du temps ecoule depuis la mise en fourriere.

### Label personnalise

```lua
Config.Label = {
    maxLength = 30,
}
```

| Parametre | Description |
|-----------|-------------|
| `maxLength` | Longueur maximum autorisee pour un label de vehicule |

---

## config_garage.lua — Garages et fourrieres

### Garages par defaut

```lua
ConfigGarage.defaultGarageCarName = "garage"
ConfigGarage.defaultGarageBoatName = "garage_bateau1"
ConfigGarage.defaultGaragePlaneName = "garage_plane1"
ConfigGarage.defaultGarageHeliName = "garage_heli1"
```

Ces noms correspondent aux garages ou les vehicules seront places lors d'une sauvegarde depuis un garage sans `saveGarage = false`.

### Structure d'un garage

```lua
{
    garageName = "garage",           -- identifiant unique (minuscules, sans espaces)
    garageLabel = "Place des Cube",  -- label affiche dans le menu
    saveGarage = true,               -- sauvegarder les vehicules dans ce garage
    job = nil,                       -- job requis (acces exclusif a ce job)
    job2 = nil,                      -- job secondaire (gang / job alternatif)
    annyJob = nil,                   -- acces restreint a CE job (independamment de job/job2)
    -- maxVehicles = 10,             -- limite de vehicules (optionnel, commenter pour illimite)
    distanceStore = 25.0,            -- distance de rangement en metres
    positionMenu = vector3(x, y, z), -- position du PED / interaction
    spawnVehPositions = {
        vector4(x, y, z, heading),   -- positions de sortie des vehicules
    },
    storeVeh = vector3(x, y, z),     -- zone de rangement des vehicules
}
```

| Parametre | Description |
|-----------|-------------|
| `garageName` | Identifiant unique du garage — doit etre unique si `saveGarage = true` |
| `garageLabel` | Nom affiche dans l'interface |
| `saveGarage` | Si `true`, les vehicules sont associes a ce garage en DB |
| `job` | Si defini, seuls les joueurs avec ce job peuvent acceder au garage |
| `job2` | Job secondaire (utile pour les gangs ou les doublons de job) |
| `annyJob` | Restreint l'acces a n'importe quel grade de ce job (police, ambulance…) |
| `maxVehicles` | Nombre max de vehicules (optionnel — commenter pour illimite) |
| `distanceStore` | Distance maximum pour ranger un vehicule depuis `storeVeh` |
| `positionMenu` | Coordonnees du PED / point d'interaction |
| `spawnVehPositions` | Tableau de positions de sortie (heading inclus) |
| `storeVeh` | Point de rangement du vehicule |

### Vehicules de service

Pour les garages de job, vous pouvez definir des vehicules de service accessibles depuis l'onglet **Ranger** (ou le sous-menu correspondant en RageUI) :

```lua
serviceVehicles = {
    { model = "police",  label = "Police Cruiser" },
    { model = "police2", label = "Police Buffalo" },
},
```

> Les vehicules de service sont disponibles uniquement pour les joueurs ayant le job requis. Ils ne sont pas sauvegardes en base de donnees.

### Personnaliser la couleur du blip par garage

```lua
blipColor = 38,
color = {r = 20, g = 100, b = 80},
```

| Parametre | Description |
|-----------|-------------|
| `blipColor` | Couleur du blip GTA pour ce garage specifique |
| `color` | Couleur RGB de l'indicateur dans l'interface NUI |

### Types de vehicules

Les vehicules sont organises en 4 categories :

| Cle | Description |
|-----|-------------|
| `"car"` | Voitures et motos |
| `"boat"` | Bateaux |
| `"plane"` | Avions |
| `"heli"` | Helicopteres |

Chaque type peut etre active ou desactive :

```lua
["car"] = {
    enable = true,
    positionGarageList = { ... },
},
```

### Ajouter un garage

Ajoutez une entree dans le tableau `positionGarageList` du type voulu :

```lua
{
    garageName = "mon_garage",
    garageLabel = "Mon Nouveau Garage",
    saveGarage = true,
    job = nil,
    job2 = nil,
    annyJob = nil,
    distanceStore = 25.0,
    positionMenu = vector3(x, y, z),
    spawnVehPositions = {
        vector4(x, y, z, 0.0),
    },
    storeVeh = vector3(x, y, z)
},
```

---

## Fourrieres (poundList)

```lua
ConfigGarage.poundList = {
    ["car"] = {
        ["pound_car_1"] = {
            label = "Fourriere Davis",
            positionMenu = vector3(x, y, z),
            spawnVehPositions = { vector4(x, y, z, heading) },
        },
    },
    ["boat"] = { ... },
    ["plane"] = { ... },
    ["heli"] = { ... },
}
```

| Parametre | Description |
|-----------|-------------|
| `label` | Nom de la fourriere affiche dans l'interface |
| `positionMenu` | Position du PED / point d'interaction de la fourriere |
| `spawnVehPositions` | Positions de sortie des vehicules recuperes |

### Ajouter une fourriere

Ajoutez une entree dans le tableau du type voulu :

```lua
["pound_car_3"] = {
    label = "Fourriere Nord",
    positionMenu = vector3(x, y, z),
    spawnVehPositions = { vector4(x, y, z, 0.0) },
},
```

> La cle doit etre unique par type de vehicule (ex: `"pound_car_3"`, `"pound_boat_2"`).
