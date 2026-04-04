---
title: "Installation"
description: "Guide d'installation du script foltone_ammunation"
script: "foltone-ammunation"
section: "Ammunation"
order: 1
version: "1.0.0"
---

# Installation

## Prerequis

- **ESX Framework** (es_extended)
- **oxmysql** (base de donnees)
- **esx_license** (systeme de licences)
- **RageUI** (interface menu)

## Etapes d'installation

### 1. Telecharger le script

Placez le dossier `foltone_ammunation` dans votre repertoire `resources/[foltone]/`.

### 2. Importer la base de donnees

Executez le fichier SQL fourni dans votre base de donnees :

```sql
-- Importez le fichier sql/install.sql dans votre base de donnees
```

### 3. Ajouter au server.cfg

```cfg
ensure foltone_ammunation
```

Assurez-vous que les dependances sont demarrees **avant** ce script :

```cfg
ensure es_extended
ensure oxmysql
ensure esx_license
ensure RageUI
```

### 4. Configurer le script

Editez le fichier `config.lua` selon vos besoins (voir la section Configuration).

### 5. Redemarrer le serveur

Redemarrez votre serveur ou executez `refresh` puis `ensure foltone_ammunation` dans la console.

## Structure des fichiers

```
foltone_ammunation/
├── client/
├── server/
├── config.lua
├── fxmanifest.lua
└── sql/
```

## Problemes courants

| Probleme | Solution |
|---|---|
| Menu ne s'ouvre pas | Verifiez que RageUI est bien demarre |
| Licence non detectee | Verifiez que esx_license est fonctionnel |
| Braquage ne demarre pas | Verifiez le nombre de policiers requis |
