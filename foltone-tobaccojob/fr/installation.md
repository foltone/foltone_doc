---
title: "Installation"
description: "Guide d'installation du script foltone_tobaccojob"
script: "foltone-tobaccojob"
section: "Tobacco Job"
order: 1
version: "1.0.0"
---

# Installation

## Prerequis

Avant d'installer `foltone_tobaccojob`, assurez-vous que les ressources suivantes sont installees et fonctionnelles sur votre serveur :

- **es_extended** (ESX Framework)
- **oxmysql** (base de donnees)
- **esx_addonaccount** (comptes societe)
- **esx_addoninventory** (inventaire societe)
- **esx_society** (gestion de societe)

## Etapes d'installation

### 1. Transfert des fichiers

Placez le dossier `foltone_tobaccojob` dans votre repertoire `resources/` :

```
resources/
  [esx]/
  [foltone]/
    foltone_tobaccojob/
      client/
      server/
      shared/
      fxmanifest.lua
```

### 2. Import SQL

Executez le fichier SQL fourni dans votre base de donnees :

```sql
-- Importez le fichier install.sql fourni avec la ressource
SOURCE install.sql;
```

Cela creera les tables necessaires pour la societe, les comptes et les inventaires.

### 3. Configuration du server.cfg

Ajoutez la ressource dans votre `server.cfg` **apres** les dependances :

```cfg
ensure es_extended
ensure oxmysql
ensure esx_addonaccount
ensure esx_addoninventory
ensure esx_society
ensure foltone_tobaccojob
```

### 4. Ajout du metier

Assurez-vous que le job `tobaccojob` est present dans votre table `jobs` et `job_grades` de la base de donnees. Un fichier SQL d'exemple est fourni.

### 5. Ajout des items

Ajoutez les items necessaires (feuilles de tabac, cigarettes, etc.) dans votre table `items` si ce n'est pas deja fait par le SQL d'installation.

## Verification

1. Demarrez votre serveur
2. Connectez-vous en jeu
3. Verifiez que le blip apparait sur la carte
4. Assignez-vous le metier via la commande admin ou la base de donnees

## Notes importantes

- Ce script est protege par **escrow** (Tebex). Ne modifiez pas les fichiers proteges.
- Les fichiers de configuration (`shared/`) sont modifiables librement.
- En cas de probleme, verifiez la console serveur pour les messages d'erreur.
