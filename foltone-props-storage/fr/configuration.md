---
title: "Configuration"
description: "Configuration du script Props Storage"
script: "foltone-props-storage"
section: "foltone_props_storage"
order: 2
version: "1.0.0"
---

# Configuration — foltone_props_storage

Toute la configuration se fait dans le fichier `config.lua` à la racine du script.

## Langue

```lua
Config.Locale = "fr" -- "fr" ou "en"
```

Les traductions sont dans le dossier `locales/`. Vous pouvez ajouter vos propres langues en créant un nouveau fichier (ex: `locales/de.lua`).

## Inventaire

```lua
Config.useOxInventory = GetResourceState("ox_inventory") ~= "missing"
```

Le script détecte automatiquement si **ox_inventory** est installé :
- **Avec ox_inventory** : utilise le système de stash natif + ox_target pour l'interaction
- **Sans ox_inventory** : utilise le menu RageUI intégré + touche E pour interagir

## Sauvegarde en base de données

```lua
Config.saveToDBWithInterval = true
Config.saveToDBInterval = 60 * 1000 -- 1 minute
```

| Option | Description |
|--------|-------------|
| `saveToDBWithInterval = true` | Sauvegarde périodique (recommandé pour serveurs avec beaucoup de joueurs) |
| `saveToDBWithInterval = false` | Sauvegarde à chaque action (dépôt/retrait) |

> **Note** : Quand `useOxInventory` est activé, `saveToDBWithInterval` est forcé à `true`.

## Distance d'interaction

```lua
Config.distance = 2.5
```

Distance maximale (en mètres) à laquelle un joueur peut interagir avec un coffre.

## Codes PIN interdits

```lua
Config.forbidenPIN = {
    0000, 1111, 2222, 3333, 4444,
    5555, 6666, 7777, 8888, 9999,
    1234,
}
```

Les joueurs ne pourront pas utiliser ces codes PIN. Le code doit faire minimum 4 chiffres.

## Types de coffres

```lua
Config.propsList = {
    ["p_v_43_safe_s"] = {
        capacity = 50000,      -- Capacité en poids
        itemName = "big_safe", -- Nom de l'item ESX requis
        itemLabel = "Grand coffre",
    },
    ["prop_ld_int_safe_01"] = {
        capacity = 30000,
        itemName = "safe",
        itemLabel = "Coffre",
    },
}
```

Vous pouvez ajouter autant de types de coffres que vous le souhaitez. Chaque entrée utilise le **nom du modèle GTA** comme clé.

### Ajouter un nouveau type de coffre

1. Trouvez le nom du modèle du prop GTA V souhaité
2. Ajoutez une entrée dans `propsList` :

```lua
["nom_du_modele"] = {
    capacity = 40000,
    itemName = "mon_coffre",
    itemLabel = "Mon Coffre Custom",
},
```

3. N'oubliez pas d'ajouter l'item correspondant dans votre base de données ESX

## Grades boss

```lua
Config.bossGrades = {
    ["boss"] = true,
    ["underboss"] = true,
    ["capodecina"] = true,
    ["consigliere"] = true,
    ["don"] = true,
}
```

Grades de job qui ont des permissions spéciales (permissions boss).

## Poids des armes

```lua
Config.defaultWeaponWeight = 3

Config.weaponWeight = {
    ["WEAPON_KNIFE"] = 2,
    ["WEAPON_PISTOL"] = 4,
    ["WEAPON_ASSAULTRIFLE"] = 8,
    ["WEAPON_RPG"] = 10,
    -- ... voir config.lua pour la liste complète
}
```

Les armes non listées utilisent `defaultWeaponWeight`. Plus de 40 armes sont préconfigurées.

## Notifications

```lua
Config.Notification = function(text)
    SetNotificationTextEntry("STRING")
    AddTextComponentString(text)
    DrawNotification(false, true)
end
```

Remplacez cette fonction par votre système de notification préféré (ex: okokNotify, ox_lib notify, etc.).

## Texte d'aide

```lua
Config.DisplayHelpText = function(text)
    SetTextComponentFormat("STRING")
    AddTextComponentString(text)
    DisplayHelpTextFromStringLabel(0, 0, 1, -1)
end
```

Personnalisez l'affichage du texte d'aide (le texte qui apparaît quand un joueur est près d'un coffre).

## Webhook Discord

Dans le fichier `server/sv_editable.lua`, configurez votre webhook Discord pour les logs :

```lua
PerformHttpRequest("https://discord.com/api/webhooks/VOTRE_ID/VOTRE_TOKEN", ...)
```

Toutes les actions (placement, ouverture, dépôt, retrait, suppression) sont logguées dans Discord.
