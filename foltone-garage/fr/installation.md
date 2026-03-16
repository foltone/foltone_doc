---
title: "Installation"
description: "Installation du script Foltone Garage"
script: "foltone-garage"
section: "Foltone Garage"
order: 1
version: "2.0.0"
---

# Installation — foltone_garage

## Prerequis

- **ESX Legacy** ou **QBCore** ou **QBX** — Framework FiveM
- **oxmysql** — Librairie MySQL

### Dependances optionnelles

| Dependance | Utilite | Requis pour |
|-----------|---------|-------------|
| `ox_target` | Interaction target 3D | Si `Config.InteractionType = "ox_target"` |
| `qb-target` | Interaction target 3D | Si `Config.InteractionType = "qb-target"` |
| `interact` | Interaction target 3D | Si `Config.InteractionType = "interact"` |

## Telechargement

Telechargez le script depuis votre espace Tebex et placez le dossier `foltone_garage` dans votre repertoire `resources/`.

## Configuration serveur

Ajoutez dans votre `server.cfg` :

```ini
ensure oxmysql
ensure es_extended      # ou qb-core / qbx_core
ensure foltone_garage
```

> **Important** : `foltone_garage` doit etre demarre **apres** votre framework (`es_extended`, `qb-core` ou `qbx_core`) et `oxmysql`.

## Framework

Le script supporte 3 frameworks :

| Framework | Valeur config | Dependances |
|-----------|--------------|-------------|
| ESX Legacy | `"esx"` | `es_extended`, `oxmysql` |
| QBCore | `"qbcore"` | `qb-core`, `oxmysql` |
| QBX | `"qbx"` | `qbx_core`, `oxmysql` |

Configurez le framework dans `Config.lua` :

```lua
Config.Framework = "esx" -- "esx", "qbcore" ou "qbx"
```

## Base de donnees

### Nouvelle installation

Executez le fichier `sql/install.sql` dans votre base de donnees MySQL.

```bash
mysql -u root -p votre_base < sql/install.sql
```

Vous pouvez egalement copier le contenu et l'executer dans phpMyAdmin ou HeidiSQL.

### Mise a jour depuis une version existante

Si vous mettez a jour depuis une version anterieure (avant v2.0.0), executez le fichier de migration :

| Fichier | Contenu |
|---------|---------|
| `sql/migrate_pound_time.sql` | Ajoute la colonne `pound_time` aux vehicules existants |

> **Important** : N'executez `migrate_pound_time.sql` que si vous avez deja une installation existante. Ne le jouez pas sur une base fraiche.

## Verification

Apres redemarrage du serveur :

1. Connectez-vous au serveur avec un personnage
2. Rendez-vous a une position de garage configuree dans `config_garage.lua`
3. Interagissez avec le PED (ou le marker selon votre configuration)
4. L'interface NUI doit s'afficher avec les onglets Vehicules, Ranger, Fourriere et Label
