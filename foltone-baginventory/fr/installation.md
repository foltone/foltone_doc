---
title: "Installation"
description: "Guide d'installation du script foltone_baginventory"
script: "foltone-baginventory"
section: "Bag Inventory"
order: 1
version: "1.0.0"
---

# Installation

## Prerequis

- **ESX Framework** (es_extended)
- **oxmysql** (base de donnees)
- **RageUI** (interface menu)

## Etapes d'installation

### 1. Telecharger le script

Placez le dossier `foltone_baginventory` dans votre repertoire `resources/[foltone]/`.

### 2. Importer la base de donnees

Executez le fichier SQL fourni :

```sql
-- Importez le fichier sql/install.sql dans votre base de donnees
```

Ce fichier cree la table necessaire pour stocker le contenu des sacs poses au sol.

### 3. Ajouter au server.cfg

```cfg
ensure foltone_baginventory
```

Assurez-vous que les dependances sont demarrees avant :

```cfg
ensure es_extended
ensure oxmysql
ensure RageUI
```

### 4. Ajouter les items

Ajoutez les items de sac dans votre base de donnees `items` :

```sql
INSERT INTO `items` (`name`, `label`, `weight`) VALUES
('bag_small', 'Petit sac', 2),
('bag_medium', 'Sac moyen', 3),
('bag_large', 'Grand sac', 5);
```

### 5. Configurer et redemarrer

Editez `config.lua` puis redemarrez le serveur.

## Structure des fichiers

```
foltone_baginventory/
├── client/
├── server/
├── config.lua
├── fxmanifest.lua
└── sql/
```
