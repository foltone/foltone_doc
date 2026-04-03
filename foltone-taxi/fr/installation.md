---
title: "Installation"
description: "Installation du script Taxi"
script: "foltone-taxi"
section: "Taxi"
order: 1
version: "2.0.0"
---

# Installation — foltone_taxi

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
ensure foltone_taxi
```

## Vérification

1. Connectez-vous avec un personnage ayant le job `taxi`
2. Vérifiez le blip "Taxi" sur la carte
3. Console serveur : `[Foltone Taxi] v2.0.0 chargee`
