---
title: "Installation"
description: "Installation du script Brasseur"
script: "foltone-brasseur"
section: "Brasseur"
order: 1
version: "2.0.0"
---

# Installation — foltone_brasseur

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

## Téléchargement

Placez le dossier `foltone_brasseur` dans votre répertoire `resources/`.

## Configuration serveur

```ini
ensure oxmysql
ensure es_extended
ensure ox_lib
ensure esx_society
ensure skinchanger
ensure foltone_brasseur
```

## Base de données

Exécutez `foltone_brasseur.sql` pour créer les tables nécessaires (job, grades, items, coffres).

Si vous utilisez **ox_inventory**, les stash sont créés automatiquement.

## Vérification

1. Connectez-vous avec un personnage ayant le job `brasseur`
2. Vérifiez le blip "Brasseur" sur la carte
3. Console serveur : `[Foltone Brasseur] v2.0.0 chargee`
