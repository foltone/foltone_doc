---
title: "Installation"
description: "Guide d'installation du Race Builder"
script: "foltone-racebuilder"
section: "foltone_racebuilder"
order: 1
version: "1.0.0"
---

# Installation — foltone_racebuilder

## Pré-requis

- **ESX Legacy** ou **QBCore** ou **Standalone** — Framework
- **oxmysql** — Driver base de données
- **ox_lib** *(optionnel)* — UI améliorée (menus contextuels, dialogues). Un fallback intégré est inclus si ox_lib n'est pas installé.
- **ox_target** ou **qb-target** *(optionnel)* — Interaction 3D avec le PNJ. Retombe sur la touche E si aucun n'est installé.

## Base de données

Le script crée automatiquement les tables nécessaires au premier démarrage :

- `foltone_races` — Données des courses (checkpoints, spawn, paramètres)
- `foltone_race_leaderboard` — Meilleurs temps par course et par joueur
- `foltone_race_sessions` — Historique des sessions multijoueur

## Téléchargement

Téléchargez le script depuis votre compte [Tebex](https://foltone.tebex.io/) et placez le dossier `foltone_racebuilder` dans votre répertoire `resources/`.

## Configuration serveur

Ajoutez dans votre `server.cfg` :

```ini
ensure oxmysql
ensure es_extended       # ou qb-core (optionnel en standalone)
ensure ox_lib            # optionnel mais recommandé
ensure ox_target         # optionnel (ou qb-target)
ensure foltone_racebuilder
```

> **Important** : `foltone_racebuilder` doit démarrer **après** oxmysql et votre framework.

## Vérification

Après le redémarrage du serveur :

1. Connectez-vous au serveur
2. Utilisez `/raceeditor` pour ouvrir l'éditeur de courses (nécessite la permission admin)
3. Créez une course test : placez le PNJ, le point de départ et au moins 2 checkpoints
4. Interagissez avec le PNJ pour ouvrir le menu et lancer un chrono solo
