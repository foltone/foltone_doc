---
title: "Configuration"
description: "Guide de configuration du script foltone_drivingschool"
script: "foltone-drivingschool"
section: "Driving School"
order: 2
version: "1.0.0"
---

# Configuration

Toute la configuration se fait dans le fichier `config.lua`.

## Parametres generaux

```lua
Config.Locale = 'fr'
Config.PedModel = 's_m_y_cop_01'       -- Modele du PNJ moniteur
Config.SchoolLocation = vector3(228.46, -1394.87, 30.59) -- Position de l'auto-ecole
```

## Blip sur la carte

```lua
Config.Blip = {
    sprite = 545,
    color = 3,
    scale = 0.8,
    label = "Auto-ecole"
}
```

## Types d'examens

### Examen du code de la route (NUI)

```lua
Config.TheoryExam = {
    passingScore = 80,          -- Score minimum pour reussir (%)
    questionsPerExam = 20,      -- Nombre de questions par examen
    timePerQuestion = 30,       -- Temps par question (secondes)
    price = 500,                -- Prix de l'examen
}
```

### Questions d'examen

```lua
Config.Questions = {
    {
        question = "Quelle est la vitesse maximale en ville ?",
        answers = { "30 km/h", "50 km/h", "70 km/h", "90 km/h" },
        correct = 2,  -- Index de la bonne reponse
    },
    {
        question = "Que signifie un feu orange ?",
        answers = { "Accelerer", "S'arreter si possible", "Priorite", "Ralentir" },
        correct = 2,
    },
    -- Ajoutez autant de questions que necessaire...
}
```

## Examens pratiques

### Permis voiture

```lua
Config.CarExam = {
    license = "drive",
    vehicle = "sultan",           -- Modele du vehicule
    price = 1500,                 -- Prix de l'examen
    maxErrors = 3,                -- Erreurs max avant echec
    speedLimit = 80,              -- Limite de vitesse (km/h)
    checkpoints = {
        vector3(230.0, -1390.0, 30.0),
        vector3(250.0, -1350.0, 30.0),
        -- Ajoutez des points de passage...
    },
}
```

### Permis moto

```lua
Config.BikeExam = {
    license = "drive_bike",
    vehicle = "bati",
    price = 1000,
    maxErrors = 3,
    speedLimit = 90,
    checkpoints = { --[[ ... ]] },
}
```

### Permis poids lourd

```lua
Config.TruckExam = {
    license = "drive_truck",
    vehicle = "mule",
    price = 3000,
    maxErrors = 2,
    speedLimit = 60,
    checkpoints = { --[[ ... ]] },
}
```

### Criteres d'erreur

Les erreurs sont comptabilisees pour :

| Infraction | Erreurs |
|---|---|
| Exces de vitesse | +1 |
| Collision avec un vehicule | +1 |
| Collision avec un pieton | +2 (echec immediat) |
| Point de passage manque | +1 |
| Vehicule endommage (seuil) | +1 |

## Notifications

```lua
Config.Notification = function(msg)
    ESX.ShowNotification(msg)
end
```
