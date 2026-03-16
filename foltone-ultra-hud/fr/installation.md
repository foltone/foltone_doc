---
title: "Installation"
description: "Guide d'installation de Ultra HUD"
script: "foltone-ultra-hud"
section: "Ultra HUD"
order: 1
version: "1.0.0"
---

# Installation — foltone_ultra_hud

## Prerequis

- **ESX Legacy** ou **QBCore** ou **QBX** ou **Standalone** — Framework (detection automatique)

> Aucune base de donnees requise. Les parametres sont stockes dans un fichier JSON.

## Telechargement

Telechargez le script depuis votre espace [Tebex](https://foltone.tebex.io/) et placez le dossier `foltone_ultra_hud` dans votre repertoire `resources/`.

## Configuration serveur

Ajoutez dans votre `server.cfg` :

```ini
ensure es_extended       # ou qb-core / qbx_core (optionnel en standalone)
ensure foltone_ultra_hud
```

> **Important** : `foltone_ultra_hud` doit demarrer **apres** votre framework. En standalone, aucune dependance n'est necessaire.

## Framework

Le script **detecte automatiquement** votre framework au demarrage. Aucune configuration manuelle n'est necessaire.

| Framework | Detection | Source faim/soif |
|---|---|---|
| ESX Legacy | `es_extended` demarre | `esx_status` |
| QBCore | `qb-core` demarre | `PlayerData.metadata` |
| QBX | `qbx_core` demarre | `PlayerData.metadata` |
| Standalone | Aucun framework | Retourne `100, 100` |

Le framework detecte est affiche dans la console serveur :

```
[foltone_ultra_hud] Framework detected: esx
```

## Verification

Apres redemarrage du serveur :

1. Connectez-vous au serveur avec un personnage
2. Le HUD doit apparaitre automatiquement avec les barres de statut, le portefeuille et la position
3. Essayez la commande admin (par defaut : `/hudadmin`) pour ouvrir le panneau de configuration
4. Essayez `/testnotif all` pour tester tous les types de notification

> Si le HUD n'apparait pas, verifiez la console serveur (F8) et la console client pour d'eventuelles erreurs. Assurez-vous que votre framework est demarre avant `foltone_ultra_hud`.
