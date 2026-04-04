---
title: "Installation"
description: "Guide d'installation du script foltone_unicornjob"
script: "foltone-unicornjob"
section: "Unicorn Job"
order: 1
version: "1.0.0"
---

# Installation

## Prerequis

Avant d'installer `foltone_unicornjob`, assurez-vous que les ressources suivantes sont installees et fonctionnelles :

- **es_extended** (ESX Framework)
- **oxmysql** (base de donnees)
- **esx_addonaccount** (comptes societe)
- **esx_addoninventory** (inventaire societe)
- **esx_society** (gestion de societe)

## Etapes d'installation

### 1. Transfert des fichiers

Placez le dossier `foltone_unicornjob` dans votre repertoire `resources/` :

```
resources/
  [esx]/
  [foltone]/
    foltone_unicornjob/
      client/
      server/
      shared/
      fxmanifest.lua
```

### 2. Import SQL

Executez le fichier SQL fourni dans votre base de donnees :

```sql
SOURCE install.sql;
```

Cela creera les tables pour la societe Unicorn, les comptes et les inventaires associes.

### 3. Configuration du server.cfg

Ajoutez la ressource dans votre `server.cfg` **apres** les dependances :

```cfg
ensure es_extended
ensure oxmysql
ensure esx_addonaccount
ensure esx_addoninventory
ensure esx_society
ensure foltone_unicornjob
```

### 4. Ajout du metier

Verifiez que le job `unicorn` est present dans les tables `jobs` et `job_grades`. Un fichier SQL d'exemple est fourni avec la ressource.

### 5. Ajout des items

Ajoutez les items de bar (boissons, cocktails, etc.) dans votre table `items` si le SQL d'installation ne les a pas crees.

## Verification

1. Demarrez le serveur
2. Connectez-vous en jeu
3. Verifiez le blip du Unicorn sur la carte
4. Assignez-vous le metier et testez l'acces au bar

## Notes importantes

- Script protege par **escrow** (Tebex). Les fichiers proteges ne sont pas modifiables.
- Les fichiers `shared/` sont entierement configurables.
- Consultez la console serveur en cas d'erreur.
