---
title: "Installation"
description: "Guide d'installation du script foltone_vehicleitem"
script: "foltone-vehicleitem"
section: "Vehicle Item"
order: 1
version: "1.0.0"
---

# Installation

## Prerequis

Avant d'installer `foltone_vehicleitem`, assurez-vous que les ressources suivantes sont installees :

- **es_extended** (ESX Framework)
- **oxmysql** (base de donnees)

## Etapes d'installation

### 1. Transfert des fichiers

Placez le dossier `foltone_vehicleitem` dans votre repertoire `resources/` :

```
resources/
  [esx]/
  [foltone]/
    foltone_vehicleitem/
      client/
      server/
      shared/
      fxmanifest.lua
```

### 2. Import SQL

Executez le fichier SQL fourni pour ajouter les items vehicules dans votre base de donnees :

```sql
SOURCE install.sql;
```

Cela ajoutera les items necessaires (ex: `bmx_item`, etc.) dans votre table `items`.

### 3. Configuration du server.cfg

Ajoutez la ressource dans votre `server.cfg` **apres** les dependances :

```cfg
ensure es_extended
ensure oxmysql
ensure foltone_vehicleitem
```

### 4. Verification des items

Assurez-vous que chaque vehicule configure dans le script a un item correspondant dans la table `items` de la base de donnees.

## Verification

1. Demarrez le serveur
2. Connectez-vous en jeu
3. Verifiez que la boutique est accessible (si configuree)
4. Testez l'achat et le spawn d'un vehicule depuis l'inventaire

## Notes importantes

- Ce script ne necessite **pas** esx_society ni esx_addonaccount.
- Les fichiers de configuration (`shared/`) sont modifiables librement.
- Le script est compatible avec les inventaires standards ESX.
