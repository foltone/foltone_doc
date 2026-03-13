---
title: "Installation"
description: "Installation du script Elevator Builder"
script: "foltone-elevator-builder"
section: "foltone_elevator_builder"
order: 1
version: "1.1.0"
---

# Installation — foltone_elevator_builder

## Prérequis

- **FiveM** avec **Lua 5.4**
- **ox_target** *(optionnel)* — Pour l'interaction par ciblage au lieu de la touche E

## Téléchargement

Téléchargez le script depuis votre espace Tebex et placez le dossier dans votre répertoire `resources/`.

## Configuration serveur

Ajoutez dans votre `server.cfg` :

```ini
ensure foltone-elevator-builder
```

> **Note** : Ce script est **standalone** — il ne nécessite aucun framework (ESX, QBCore, etc.). Les données sont sauvegardées dans le fichier `json/data.json`.

## Aucune base de données requise

Contrairement à d'autres scripts, Elevator Builder n'utilise **pas de base de données SQL**. Toutes les données des ascenseurs sont stockées dans le fichier `json/data.json` au format JSON.

## Commande d'administration

Le script enregistre la commande `/fab` pour ouvrir le menu d'administration des ascenseurs. Vous pouvez modifier cette commande dans `client/cl_editable.lua` :

```lua
RegisterCommand("fab", function(source, args)
    TriggerEvent("foltone_ascenseur:open_menu")
end)
```

> **Important** : Pensez à restreindre l'accès à cette commande via votre système ACE permissions pour éviter que tous les joueurs puissent créer des ascenseurs.

## ox_target (optionnel)

Si vous souhaitez utiliser ox_target pour l'interaction :

1. Assurez-vous que `ox_target` est démarré sur votre serveur
2. Activez l'option dans `Config.lua` :

```lua
Config.use_target = true
```

Le script détecte automatiquement la présence d'ox_target. Si `use_target` est activé mais ox_target n'est pas installé, le script utilise automatiquement la touche E comme fallback.

## Vérification

Après redémarrage du serveur :

1. Tapez `/fab` dans le chat
2. L'interface d'administration NUI doit s'ouvrir
3. Créez un ascenseur avec 2 étages pour tester
4. Les marqueurs doivent apparaître aux positions définies
