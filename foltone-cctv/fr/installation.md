---
title: "Installation"
description: "Guide d'installation de Foltone CCTV"
script: "foltone-cctv"
section: "Foltone CCTV"
order: 1
version: "1.0.0"
---

# Installation — foltone_cctv

## Prerequis

- **ESX Legacy**, **QBCore**, ou **QBX** — Framework FiveM
- **oxmysql** — Librairie MySQL

### Dependances optionnelles

| Dependance | Utilite | Requis pour |
|-----------|---------|-------------|
| `ox_target` | Interaction 3D target | Si `Config.InteractionType = "ox_target"` |
| `screenshot-basic` | Capture d'ecran des cameras | Fonctionnalite de capture |

## Telechargement

Telechargez le script depuis votre compte Tebex et placez le dossier `foltone_cctv` dans votre repertoire `resources/`.

## Configuration serveur

Ajoutez dans votre `server.cfg` :

```ini
set screenshot_basic_allow_fs_write "true"

ensure oxmysql
ensure es_extended      # ou qb-core / qbx_core
ensure screenshot-basic # optionnel, pour les captures
ensure foltone_cctv
```

> **Important** : `foltone_cctv` doit demarrer **apres** votre framework et `oxmysql`. Le convar `screenshot_basic_allow_fs_write` est necessaire pour la fonctionnalite de capture.

## Framework

Le script supporte 3 frameworks :

| Framework | Valeur config | Dependances |
|-----------|-------------|-------------|
| ESX Legacy | `"esx"` | `es_extended`, `oxmysql` |
| QBCore | `"qbcore"` | `qb-core`, `oxmysql` |
| QBX | `"qbx"` | `qbx_core`, `oxmysql` |

Configurez le framework dans `config.lua` :

```lua
Config.Framework = "esx" -- "esx", "qbcore" ou "qbx"
```

## Base de donnees

### Nouvelle installation

Executez le fichier `sql/install.sql` dans votre base de donnees MySQL :

```bash
mysql -u root -p votre_base < sql/install.sql
```

Vous pouvez aussi copier le contenu et l'executer dans phpMyAdmin ou HeidiSQL.

> Le script ajoute automatiquement les colonnes manquantes (`camera_type`, `job_group`) au premier demarrage. Aucune migration manuelle necessaire.

## Items d'inventaire

Vous devez enregistrer les items suivants dans votre systeme d'inventaire (ox_inventory, qb-inventory, etc.) :

| Nom de l'item | Utilite |
|-----------|---------|
| `cctv_tablet` | Tablette de surveillance — ouvre le panneau |
| `cctv_station` | Poste de surveillance — ouvre le panneau |
| `cctv_cam_standard` | Camera Standard — murale classique |
| `cctv_cam_dome` | Camera Dome — grand angle 360 |
| `cctv_cam_bullet` | Camera Bullet — longue portee |
| `cctv_cam_mini` | Camera Mini Bullet — compacte et discrete |
| `cctv_cam_ptz` | Camera PTZ Pro — pan-tilt-zoom professionnelle |

> Chaque type de camera a son propre item. Utiliser l'item lance le mode placement pour ce type specifique.

## Verification

Apres avoir redemarre le serveur :

1. Connectez-vous au serveur avec un personnage
2. Rendez-vous a la position du PNJ vendeur configuree dans `Config.ShopPositions`
3. Interagissez avec le vendeur pour ouvrir la boutique
4. Achetez une camera, puis utilisez l'item pour entrer en mode placement
5. Placez la camera sur un mur, nommez-la, puis utilisez la tablette pour la visualiser
