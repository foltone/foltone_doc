---
title: "Installation"
description: "Guide d'installation du script foltone_gruppe6"
script: "foltone-gruppe6"
section: "Gruppe6"
order: 1
version: "1.0.0"
---

# Installation de foltone_gruppe6

## Prerequis

- **ESX Framework** (es_extended)
- **oxmysql** pour la base de donnees
- **RageUI** (inclus ou a installer separement)

## Etapes d'installation

### 1. Telecharger le script

Placez le dossier `foltone_gruppe6` dans votre repertoire `resources/`.

### 2. Importer la base de donnees

Executez le fichier SQL fourni dans votre base de donnees :

```sql
-- Importez le fichier SQL fourni avec le script
-- Il contient les tables necessaires pour le metier et le braquage
```

### 3. Ajouter le job dans la base de donnees

Assurez-vous que le job `gruppe6` existe dans votre table `jobs` avec les grades configures.

### 4. Configurer le server.cfg

Ajoutez la ligne suivante dans votre `server.cfg` :

```cfg
ensure foltone_gruppe6
```

### 5. Ordre de demarrage

Le script doit demarrer **apres** les ressources suivantes :

```cfg
ensure es_extended
ensure oxmysql
ensure foltone_gruppe6
```

## Verification

1. Redemarrez votre serveur
2. Connectez-vous et assignez-vous le job `gruppe6`
3. Rendez-vous au point de service pour verifier que le menu RageUI s'ouvre correctement
4. Verifiez les logs serveur pour d'eventuelles erreurs
