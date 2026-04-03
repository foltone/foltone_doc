---
title: "Installation"
description: "Installation du script Mechanic"
script: "foltone-mechanic"
section: "Mechanic"
order: 1
version: "2.0.0"
---

# Installation — foltone_mechanic

## Prérequis

- **ESX Legacy** — Framework serveur
- **ox_lib** — Notifications, inputs, progress bars
- **oxmysql** — Librairie MySQL
- **skinchanger** — Vestiaire / tenues
- **esx_society** — Gestion de société

### Optionnels

- **ox_inventory** — Coffres stash (fallback vers esx_addoninventory)
- **ox_target** — Interactions 3D (fallback vers markers + touche E)
- **esx_billing** — Facturation

## Configuration serveur

```ini
ensure oxmysql
ensure es_extended
ensure ox_lib
ensure esx_society
ensure skinchanger
ensure foltone_mechanic
```

> Le script inclut des fichiers meta pour les couleurs de véhicule (`carcols_gen9.meta`, `carmodcols_gen9.meta`).

## Vérification

1. Connectez-vous avec un personnage ayant le job `mechanic`
2. Vérifiez le blip "Mécano" sur la carte
3. Console serveur : `[Foltone Mechanic] v2.0.0 chargee`
