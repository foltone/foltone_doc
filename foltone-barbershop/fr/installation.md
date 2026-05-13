---
title: "Installation"
description: "Guide d'installation du script barbershop"
script: "foltone-barbershop"
section: "Barbershop"
order: 1
version: "1.0.0"
---

# Installation

## Prérequis

- **Framework** : ESX Legacy, QBCore ou QBX
- **Base de données** : oxmysql
- **Ressource d'apparence** (QBCore/QBX uniquement) : `illenium-appearance`, `fivem-appearance` ou `qb-clothing`

Aucun fichier SQL supplémentaire n'est nécessaire. Le barbershop ne stocke pas ses propres données en base — il s'appuie sur votre ressource d'apparence pour sauvegarder et charger le look des joueurs.

## Configuration du Framework

Dans `config.lua`, définissez votre framework :

```lua
Config.Framework = "esx"       -- Pour ESX Legacy
Config.Framework = "qbcore"    -- Pour QBCore
Config.Framework = "qbx"       -- Pour QBX
```

## Ressource d'apparence (QBCore / QBX)

Si vous utilisez QBCore ou QBX, vous devez spécifier quelle ressource d'apparence gère la sauvegarde et le chargement du skin :

```lua
Config.AppearanceResource = "illenium-appearance"   -- ou "fivem-appearance" ou "qb-clothing"
```

Ce paramètre n'est pas utilisé sur ESX, qui gère l'apparence via son propre système de skin.

## server.cfg

Assurez-vous que votre framework et vos dépendances démarrent avant le barbershop :

```cfg
ensure oxmysql
ensure es_extended          # ou qb-core / qbx-core
ensure illenium-appearance  # QBCore/QBX uniquement — adaptez à votre ressource d'apparence
ensure foltone_barbershop
```

## Emplacements des Barbershops

Le script est livré avec **7 emplacements de barbershop** préconfigurés sur la carte. Chaque emplacement possède un blip sur la carte (sprite 71) et 3 à 4 chaises de barbier. Vous pouvez ajouter, supprimer ou déplacer les emplacements dans `Config.Positions` (voir la page Configuration pour les détails).

## Escrow et fichiers modifiables

Les fichiers suivants ne sont **pas protégés par l'escrow** et peuvent être librement modifiés :

- `config.lua` — tous les paramètres
- `locales/*.lua` — chaînes de traduction
- `client/cl_editable.lua` — logique modifiable côté client
- `server/sv_editable.lua` — logique modifiable côté serveur
