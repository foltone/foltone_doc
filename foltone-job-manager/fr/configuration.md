---
title: "Configuration"
description: "Configuration du script Job Manager"
script: "foltone-job-manager"
section: "foltone_job_manager"
order: 2
version: "1.0.0"
---

# Configuration — foltone_job_manager

Toute la configuration se fait dans le fichier `config.lua` à la racine du script.

## Langue

```lua
Config.Locale = "fr" -- "fr" ou "en"
```

Les traductions sont dans le dossier `locales/`. Vous pouvez ajouter vos propres langues en créant un nouveau fichier (ex: `locales/de.lua`).

## Framework

```lua
Config.Framework = "esx" -- "esx", "qbcore" ou "standalone"
```

Le script supporte ESX Legacy, QBCore et un mode Standalone. En mode Standalone, vous devez gérer manuellement le chargement du joueur et l'événement `foltone_job_manager:getData`.

## Liste des sociétés

```lua
Config.SocietyList = {
    ["police"] = {
        bossGrade = "boss",
        position = vector3(448.25, -973.33, 29.69),
        color = { r = 0, g = 0, b = 255 },
    }
}
```

| Paramètre | Description |
|-----------|-------------|
| Clé (ex: `"police"`) | Nom du job tel que défini dans votre framework |
| `bossGrade` | Nom du grade qui a accès à la gestion (ex: `"boss"`) |
| `position` | Coordonnées `vector3` du marqueur d'accès |
| `color` | Couleur RGB du marqueur |

### Ajouter une société

```lua
["ambulance"] = {
    bossGrade = "boss",
    position = vector3(311.0, -595.0, 43.29),
    color = { r = 255, g = 0, b = 0 },
},
```

> Le nom de la clé doit correspondre exactement au nom du job dans votre base de données.

## Thème de l'interface

```lua
Config.theme = {
    bgColorLight = "#f5f5f5",
    bgColorDark = "#2c2c2c",
    textColorLight = "#333",
    textColorDark = "#fff",
    borderColorLight = "#ddd",
    borderColorDark = "#444",
    primaryColor = "#ffffff",
    primaryDark = "#f5f5f5",
    secondaryColor = "#7476DC",
    shadow = "0 4px 6px rgba(0, 0, 0, 0.1)"
}
```

L'interface supporte un mode **clair** et un mode **sombre**. Les joueurs peuvent basculer entre les deux via le bouton dans l'interface. Le choix est sauvegardé dans le navigateur.

| Paramètre | Description |
|-----------|-------------|
| `bgColorLight` / `bgColorDark` | Couleur de fond (mode clair / sombre) |
| `textColorLight` / `textColorDark` | Couleur du texte |
| `borderColorLight` / `borderColorDark` | Couleur des bordures |
| `primaryColor` / `primaryDark` | Couleur primaire |
| `secondaryColor` | Couleur d'accentuation (boutons, sidebar active) |
| `shadow` | Ombre portée de la tablette |

## Notifications

```lua
Config.Notification = function(message)
    SetNotificationTextEntry("STRING")
    AddTextComponentString(message)
    DrawNotification(false, false)
end
```

Remplacez cette fonction par votre système de notification préféré (ex: okokNotify, ox_lib notify, etc.).

## Texte d'aide

```lua
Config.DisplayText = function(text)
    SetTextComponentFormat("STRING")
    AddTextComponentString(text)
    DisplayHelpTextFromStringLabel(0, 0, 1, -1)
end
```

Personnalisez l'affichage du texte d'aide (affiché quand un boss est près du marqueur).
