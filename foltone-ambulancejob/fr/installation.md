---
title: "Installation"
description: "Installation du script Ambulance"
script: "foltone-ambulancejob"
section: "Ambulance"
order: 1
version: "2.0.0"
---

# Installation — foltone_advanced_ambulancejob

## Prérequis

- **ESX Legacy**, **ox_lib**, **oxmysql**, **skinchanger**, **esx_society**
- Optionnels : **ox_inventory**, **ox_target**, **esx_billing**

> Le script inclut des props streamés (brancards) dans le dossier `stream/`.

## Configuration serveur

```ini
ensure foltone_advanced_ambulancejob
```

## Vérification

1. Connectez-vous avec un personnage ayant le job `ambulance`
2. Vérifiez le blip "Hopital" sur la carte
3. Console serveur : `[Foltone Ambulance] v2.0.0 chargee`
