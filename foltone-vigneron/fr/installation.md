---
title: "Installation"
description: "Installation du script Vigneron"
script: "foltone-vigneron"
section: "Vigneron"
order: 1
version: "2.0.0"
---

# Installation — foltone_vigneron

## Prérequis

- **ESX Legacy** — Framework serveur
- **ox_lib** — Notifications, inputs, progress bars
- **oxmysql** — Librairie MySQL
- **skinchanger** — Vestiaire / tenues
- **esx_society** — Gestion de société

### Optionnels

- **ox_inventory** — Coffres stash (fallback automatique vers esx_addoninventory)
- **ox_target** — Interactions 3D (fallback automatique vers markers + touche E)
- **esx_billing** — Facturation de joueurs

## Téléchargement

Téléchargez le script depuis votre espace Tebex et placez le dossier `foltone_vigneron` dans votre répertoire `resources/`.

## Configuration serveur

Ajoutez dans votre `server.cfg` :

```ini
ensure oxmysql
ensure es_extended
ensure ox_lib
ensure esx_society
ensure skinchanger
ensure foltone_vigneron
```

> **Important** : `foltone_vigneron` doit être démarré **après** `es_extended`, `ox_lib` et `oxmysql`.

## Base de données

Si vous utilisez **esx_addoninventory** (pas ox_inventory), exécutez le fichier `foltone_vigneron.sql` dans votre base de données pour créer les coffres partagés.

Si vous utilisez **ox_inventory**, les stash sont créés automatiquement au démarrage.

## Vérification

Après redémarrage du serveur :

1. Connectez-vous avec un personnage ayant le job `vigne`
2. Vérifiez que le blip "Vigneron" apparaît sur la carte
3. Rendez-vous aux marqueurs pour tester les interactions
4. Vérifiez la console serveur : `[Foltone Vigneron] v2.0.0 chargee`
