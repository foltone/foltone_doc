---
title: "Configuration"
description: "Référence de configuration du script barbershop"
script: "foltone-barbershop"
section: "Barbershop"
order: 2
version: "1.1.0"
---

# Configuration

Tous les paramètres se trouvent dans `config.lua`.

## Général

| Option | Type | Défaut | Description |
|--------|------|--------|-------------|
| `Config.Framework` | string | `"esx"` | Framework utilisé : `"esx"`, `"qbcore"` ou `"qbx"` |
| `Config.Locale` | string | `"en"` | Langue : `"en"` ou `"fr"` |
| `Config.AutoUpdateCheck` | boolean | `true` | Vérifier au démarrage si une nouvelle version est publiée et l'afficher dans la console serveur |

## Interaction

| Option | Type | Défaut | Description |
|--------|------|--------|-------------|
| `Config.InteractionType` | string | `"ox_target_prop"` | Méthode d'interaction (voir ci-dessous) |
| `Config.InteractionDistance` | number | `1.5` | Distance pour les interactions drawtext / marker |
| `Config.ChairModels` | table | *(voir ci-dessous)* | Liste des modèles de props de chaises de barbier utilisés par les systèmes target |

### Types d'interaction supportés

| Valeur | Description |
|--------|-------------|
| `"drawtext"` | Texte à l'écran (drawtext du framework) |
| `"ox_target"` | ox_target sur l'entité de la chaise |
| `"ox_target_prop"` | ox_target sur le modèle de la chaise |
| `"qb-target"` | qb-target sur l'entité de la chaise |
| `"qb-target_prop"` | qb-target sur le modèle de la chaise |
| `"qtarget"` | qtarget sur l'entité de la chaise |
| `"qtarget_prop"` | qtarget sur le modèle de la chaise |
| `"interact"` | interact sur l'entité de la chaise |
| `"interact_prop"` | interact sur le modèle de la chaise |
| `"marker"` | Marqueur 3D sur chaque position de chaise |

### Modèles de chaises par défaut

```lua
Config.ChairModels = {
    "v_serv_bs_barbchair3",
    "v_serv_bs_barbchair5",
    "v_serv_bs_barbchair2",
    "v_serv_bs_barbchair",
    "m25_2_int_01_barber_chair",
}
```

## Interface / Menu

| Option | Type | Défaut | Description |
|--------|------|--------|-------------|
| `Config.MenuPosition` | string | `"right"` | Position du menu à l'écran : `"left"` ou `"right"` |
| `Config.MenuStyle` | string | `"glass"` | Style visuel du menu : `"glass"` ou `"solid"` |
| `Config.UIColors` | table | *(voir ci-dessous)* | Couleurs d'accentuation du menu NUI |

### Couleurs de l'interface

```lua
Config.UIColors = {
    accent      = "#e74c3c",
    accentLight = "#ff6b5a",
    accentDim   = "#c0392b",
}
```

Ces trois valeurs hexadécimales contrôlent la couleur d'accent principale, la couleur d'accent claire et la couleur d'accent sombre dans toute l'interface du menu.

## Tarification

| Option | Type | Défaut | Description |
|--------|------|--------|-------------|
| `Config.Price` | number | `75` | Prix facturé pour une coupe de cheveux |

## PNJ Barbier

| Option | Type | Défaut | Description |
|--------|------|--------|-------------|
| `Config.BarberModel` | string | `"s_f_y_hooker_01"` | Modèle du PNJ qui apparaît en tant que barbier |

## Ressource d'apparence

| Option | Type | Défaut | Description |
|--------|------|--------|-------------|
| `Config.AppearanceResource` | string | `"illenium-appearance"` | Ressource d'apparence pour sauvegarder/charger le skin (QBCore/QBX uniquement) : `"illenium-appearance"`, `"fivem-appearance"` ou `"qb-clothing"` |

## Emplacements des Barbershops — `Config.Positions`

Chaque entrée dans `Config.Positions` définit un barbershop :

```lua
{
    pos = vector3(x, y, z),                           -- Position centrale (utilisée pour le placement du blip)
    blip = { sprite = 71, color = 47, scale = 0.8, label = "Barber Shop" },
    chairs = {                                        -- Liste des positions de chaises
        vector4(x, y, z, heading),
        -- ...
    },
}
```

Le script est livré avec **7 emplacements**, chacun avec 3 à 4 chaises. Vous pouvez librement ajouter, supprimer ou déplacer des entrées.

## Paramètres du marqueur

Utilisé uniquement quand `Config.InteractionType = "marker"` :

```lua
Config.Marker = {
    type  = 1,
    scale = vector3(0.8, 0.8, 0.3),
    color = { r = 59, g = 130, b = 246, a = 120 },
}
```

## Paramètres du DrawText

Utilisé uniquement quand `Config.InteractionType = "drawtext"` :

```lua
Config.DrawText = {
    label = "interact_label",   -- Clé de locale utilisée pour le texte du prompt
}
```

## Notifications

La fonction `Notification(source, message, type)` dans `config.lua` gère les notifications côté serveur. Elle dispatche automatiquement vers le bon événement du framework (ESX ou QBCore/QBX). Vous pouvez la remplacer par votre propre système de notifications.
