---
title: "Installation"
description: "Installation du script Job Manager"
script: "foltone-job-manager"
section: "foltone_job_manager"
order: 1
version: "1.0.0"
---

# Installation — foltone_job_manager

## Prérequis

- **ESX Legacy** ou **QBCore** ou **Standalone**
- **oxmysql** — Librairie MySQL
- **esx_addonaccount** *(ESX uniquement)* — Pour la gestion des comptes de société

## Téléchargement

Téléchargez le script depuis votre espace Tebex et placez le dossier dans votre répertoire `resources/`.

## Configuration serveur

Ajoutez dans votre `server.cfg` :

```ini
ensure oxmysql
ensure es_extended # ou qb-core
ensure foltone_job_manager
```

> **Important** : `foltone_job_manager` doit être démarré **après** votre framework (`es_extended` ou `qb-core`) et `oxmysql`.

## Framework

Le script supporte 3 modes :

| Framework | Valeur config | Dépendances |
|-----------|--------------|-------------|
| ESX Legacy | `"esx"` | `es_extended`, `oxmysql`, `esx_addonaccount` |
| QBCore | `"qbcore"` | `qb-core`, `oxmysql`, `qb-banking` |
| Standalone | `"standalone"` | Configuration manuelle requise |

Configurez le framework dans `config.lua` :

```lua
Config.Framework = "esx" -- "esx", "qbcore" ou "standalone"
```

## Vérification

Après redémarrage du serveur :

1. Connectez-vous avec un personnage ayant le grade **boss** d'un job configuré
2. Rendez-vous au marqueur de la société (position configurée dans `config.lua`)
3. Appuyez sur **E** pour ouvrir l'interface de gestion
4. L'interface tablette doit s'afficher avec les onglets : Argent, Employés, Salaires, Virements
