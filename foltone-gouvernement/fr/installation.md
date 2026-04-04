---
title: "Installation"
description: "Installation du script Gouvernement"
script: "foltone-gouvernement"
section: "Gouvernement"
order: 1
version: "2.0.0"
---

# Installation — foltone_gouvernement

## Prerequis

- **ESX Legacy**, **ox_lib**, **oxmysql**, **skinchanger**, **esx_society**, **esx_addonaccount**
- Optionnels : **ox_inventory**, **ox_target**, **esx_billing** (fiches d'impot), **esx_license** (permis)

## Base de donnees

Executez `foltone_gouvernement.sql` pour creer le job, les 8 grades, les comptes et coffres.

## Configuration serveur

```ini
ensure foltone_gouvernement
```

## Verification

1. Connectez-vous avec un personnage ayant le job `gouvernement`
2. Verifiez le blip "Gouvernement" sur la carte
3. Console : `[Foltone Gouvernement] v2.0.0 chargee`
