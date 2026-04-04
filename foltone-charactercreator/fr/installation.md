---
title: "Installation"
description: "Guide d'installation du script foltone_charactercreator"
script: "foltone-charactercreator"
section: "Character Creator"
order: 1
version: "1.0.0"
---

# Installation

## Prerequis

- **ESX Framework** (es_extended)
- **skinchanger** (gestion de l'apparence)
- **RageUI** (interface menu)

## Etapes d'installation

### 1. Telecharger le script

Placez le dossier `foltone_charactercreator` dans votre repertoire `resources/[foltone]/`.

### 2. Ajouter au server.cfg

```cfg
ensure foltone_charactercreator
```

Assurez-vous que les dependances sont demarrees avant :

```cfg
ensure es_extended
ensure skinchanger
ensure RageUI
```

### 3. Configurer le script

Editez le fichier `config.lua` selon vos besoins (voir la section Configuration).

### 4. Redemarrer le serveur

Redemarrez votre serveur ou executez `refresh` puis `ensure foltone_charactercreator` dans la console.

## Structure des fichiers

```
foltone_charactercreator/
├── client/
├── server/
├── config.lua
└── fxmanifest.lua
```

## Compatibilite

Ce script remplace le createur de personnage par defaut d'ESX. Assurez-vous de desactiver tout autre script de creation de personnage pour eviter les conflits.

## Problemes courants

| Probleme | Solution |
|---|---|
| Menu ne s'affiche pas | Verifiez que RageUI est demarre |
| Apparence non sauvegardee | Verifiez que skinchanger fonctionne |
| Conflit avec un autre script | Desactivez les autres createurs de personnage |
