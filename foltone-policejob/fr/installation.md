---
title: "Installation"
description: "Installation du script Police"
script: "foltone-policejob"
section: "Police"
order: 1
version: "2.0.0"
---

# Installation — foltone_policejob

## Prérequis

- **ESX Legacy**, **ox_lib**, **oxmysql**, **skinchanger**, **esx_society**
- Optionnels : **ox_inventory**, **ox_target**, **esx_billing**

## Configuration serveur

```ini
ensure foltone_policejob
```

> Le script utilise une NUI pour le timer de prison (incluse).

## Vérification

1. Connectez-vous avec un personnage ayant le job `police`
2. Vérifiez le blip "Commissariat" sur la carte
3. Console serveur : `[Foltone Police] v2.0.0 chargee`
