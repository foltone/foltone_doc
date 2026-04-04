---
title: "Configuration"
description: "Configuration du script Job Builder"
script: "foltone-job-builder"
section: "Job Builder"
order: 2
version: "2.0.0"
---

# Configuration — foltone_job_builder

## General

```lua
Config.Debug = true
Config.AdminGroups = { 'admin', 'superadmin' }
Config.UseOxInventory = GetResourceState('ox_inventory') ~= 'missing'
```

## Fonctionnalites

Le job builder permet de creer des jobs complets in-game avec :
- Nom, label, couleur, blip configurable
- Grades avec salaires et tenues
- Multi-coffres avec grade minimum
- Garage avec liste de vehicules
- Pipeline de processing (recolte/transformation/vente)
- Annonces de service
- Systeme de boss, vestiaire, duty

## Commandes

| Commande | Description |
|----------|-------------|
| `/jb` | Ouvrir le builder RageUI |
| `/jbnui` | Ouvrir le NUI builder (carte interactive) |
