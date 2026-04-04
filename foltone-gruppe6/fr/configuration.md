---
title: "Configuration"
description: "Guide de configuration du script foltone_gruppe6"
script: "foltone-gruppe6"
section: "Gruppe6"
order: 2
version: "1.0.0"
---

# Configuration de foltone_gruppe6

## Fichier de configuration

Toute la configuration se fait dans le fichier `config.lua` a la racine du script.

## Parametres du metier

### Grades du job

```lua
Config.JobGrades = {
    { name = "recrue", label = "Recrue", salary = 200 },
    { name = "agent", label = "Agent", salary = 350 },
    { name = "chef", label = "Chef d'equipe", salary = 500 },
    { name = "patron", label = "Patron", salary = 700 },
}
```

### Recompenses de mission

```lua
Config.MissionReward = {min = 500, max = 1500}
```

Definissez la fourchette de recompense pour chaque mission completee.

### Tenues

```lua
Config.Outfits = {
    male = { ... },
    female = { ... },
}
```

Configurez les composants de tenue (tshirt, torso, pantalon, chaussures, etc.) pour chaque sexe.

### Vehicule

```lua
Config.VehicleModel = "stockade"
```

Modele du vehicule blinde utilise pour les missions.

## Parametres du braquage

### Police requise

```lua
Config.Robbery = {
    requiredPolice = 2,
    cooldown = 1800, -- en secondes (30 minutes)
    explosiveItem = "explosive", -- item necessaire
    rewardMin = 5000,
    rewardMax = 15000,
}
```

| Parametre | Description |
|-----------|-------------|
| `requiredPolice` | Nombre minimum de policiers en service |
| `cooldown` | Temps d'attente entre deux braquages (secondes) |
| `explosiveItem` | Nom de l'item explosif requis dans l'inventaire |
| `rewardMin` / `rewardMax` | Fourchette de gain du braquage |

## Traduction

Les textes affichables se trouvent dans `locales/`. Ajoutez ou modifiez les fichiers pour supporter d'autres langues.
