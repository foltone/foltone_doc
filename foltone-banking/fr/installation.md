---
title: "Installation"
description: "Installation du script Foltone Banking"
script: "foltone-banking"
section: "Banking"
order: 1
version: "1.0.0"
---

# Installation — foltone_banking

## Prerequis

- **ESX Legacy** ou **QBCore** ou **QBX** — Framework FiveM
- **oxmysql** — Librairie MySQL

### Dependances optionnelles

| Dependance | Utilite | Requis pour |
|-----------|---------|-------------|
| `esx_addonaccount` | Comptes de societe | ESX uniquement |
| `qb-banking` | Comptes de societe | QBCore / QBX uniquement |
| `ox_inventory` | Carte bancaire comme item | Si `CardSystem.useItem = true` |
| `ox_target` | Interaction target | Si `InteractionType = "ox_target"` |
| `qb-target` | Interaction target | Si `InteractionType = "qb-target"` |
| `qtarget` | Interaction target | Si `InteractionType = "qtarget"` |
| `lb_phone` | Notifications telephone | Si `PhoneNotifications.resource = "lb_phone"` |
| `qs-smartphone` | Notifications telephone | Si `PhoneNotifications.resource = "qs-smartphone"` |
| `gksphone` | Notifications telephone | Si `PhoneNotifications.resource = "gksphone"` |

## Telechargement

Telechargez le script depuis votre espace Tebex et placez le dossier `foltone_banking` dans votre repertoire `resources/`.

## Configuration serveur

Ajoutez dans votre `server.cfg` :

```ini
ensure oxmysql
ensure es_extended      # ou qb-core / qbx_core
ensure esx_addonaccount # ESX uniquement, pour les comptes societe
ensure foltone_banking
```

> **Important** : `foltone_banking` doit etre demarre **apres** votre framework (`es_extended`, `qb-core` ou `qbx_core`) et `oxmysql`.

## Framework

Le script supporte 3 frameworks :

| Framework | Valeur config | Dependances |
|-----------|--------------|-------------|
| ESX Legacy | `"esx"` | `es_extended`, `oxmysql`, `esx_addonaccount` |
| QBCore | `"qbcore"` | `qb-core`, `oxmysql`, `qb-banking` |
| QBX | `"qbx"` | `qbx_core`, `oxmysql`, `qb-banking` |

Configurez le framework dans `config.lua` :

```lua
Config.Framework = "esx" -- "esx", "qbcore" ou "qbx"
```

## Base de donnees

### Nouvelle installation

Executez le fichier `sql/install.sql` dans votre base de donnees MySQL. Ce fichier cree toutes les tables necessaires au fonctionnement du script.

```bash
mysql -u root -p votre_base < sql/install.sql
```

Vous pouvez egalement copier le contenu du fichier et l'executer dans phpMyAdmin ou HeidiSQL.

### Mise a jour d'une installation existante

Si vous mettez a jour le script depuis une version anterieure, executez les fichiers de migration dans l'ordre :

| Fichier | Contenu |
|---------|---------|
| `sql/migrate_phase3.sql` | Score de credit, niveaux de compte, interets, taxation |
| `sql/migrate_phase4.sql` | Comptes joints, tables membres et transactions joints |
| `sql/migrate_phase5.sql` | Epargne, placements a terme, crypto holdings et trades |

> **Important** : Executez uniquement les migrations correspondant aux phases que vous n'avez pas encore installees. Ne rejouez pas une migration deja appliquee.

## Verification

Apres redemarrage du serveur :

1. Connectez-vous au serveur avec un personnage
2. Rendez-vous a une **banque** (position configuree dans `config.lua`)
3. Approchez-vous du **PED banquier**
4. Appuyez sur **E** (ou interagissez via target selon votre configuration)
5. L'interface bancaire NUI doit s'afficher avec la sidebar et le tableau de bord

> Si l'interface ne s'ouvre pas, verifiez la console serveur (F8) et la console client (F8 en jeu) pour d'eventuelles erreurs. Assurez-vous que toutes les dependances sont bien demarrees avant `foltone_banking`.
