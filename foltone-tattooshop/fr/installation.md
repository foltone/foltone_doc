---
title: "Installation"
description: "Guide d'installation du script de salon de tatouage"
script: "foltone-tattooshop"
section: "Tattoo Shop"
order: 1
version: "1.0.0"
---

# Installation

## Prerequis

- **Framework** : ESX Legacy, QBCore ou QBX
- **Base de donnees** : oxmysql
- **FiveM** : Derniers artifacts recommandes

## Configuration de la base de donnees

Le script stocke les tatouages des joueurs dans une colonne dediee. Vous devez ajouter une colonne `tattoos` de type `LONGTEXT` a votre table joueurs.

### ESX Legacy

```sql
ALTER TABLE users ADD COLUMN tattoos LONGTEXT DEFAULT NULL;
```

### QBCore / QBX

```sql
ALTER TABLE players ADD COLUMN tattoos LONGTEXT DEFAULT NULL;
```

## Configuration du framework

Dans votre `config.lua`, definissez le framework que vous utilisez :

```lua
Config.Framework = "esx"     -- Pour ESX Legacy
Config.Framework = "qbcore"  -- Pour QBCore
Config.Framework = "qbx"     -- Pour QBX
```

## Configuration du serveur

Ajoutez les lignes suivantes a votre `server.cfg`, en respectant l'ordre de chargement :

```cfg
ensure oxmysql
ensure es_extended   # ou qb-core / qbx-core selon votre framework
ensure foltone_tattooshop
```

Assurez-vous que `oxmysql` et votre ressource framework sont demarres **avant** `foltone_tattooshop`.

## Emplacements des salons de tatouage

Le script est livre avec **6 emplacements preconfigures**, chacun avec un blip sur la carte. Ces positions peuvent etre personnalisees dans `config.lua` via `Config.TattooShopPositions`.
