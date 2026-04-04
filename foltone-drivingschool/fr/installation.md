---
title: "Installation"
description: "Guide d'installation du script foltone_drivingschool"
script: "foltone-drivingschool"
section: "Driving School"
order: 1
version: "1.0.0"
---

# Installation

## Prerequis

- **ESX Framework** (es_extended)
- **esx_license** (systeme de licences)

## Etapes d'installation

### 1. Telecharger le script

Placez le dossier `foltone_drivingschool` dans votre repertoire `resources/[foltone]/`.

### 2. Ajouter les types de licence

Assurez-vous que les types de licence suivants existent dans esx_license :

- `drive` - Permis voiture
- `drive_bike` - Permis moto
- `drive_truck` - Permis poids lourd

### 3. Ajouter au server.cfg

```cfg
ensure foltone_drivingschool
```

Assurez-vous que les dependances sont demarrees avant :

```cfg
ensure es_extended
ensure esx_license
```

### 4. Configurer le script

Editez le fichier `config.lua` pour personnaliser les questions d'examen, les parcours et les vehicules (voir la section Configuration).

### 5. Redemarrer le serveur

Redemarrez votre serveur ou executez `refresh` puis `ensure foltone_drivingschool` dans la console.

## Structure des fichiers

```
foltone_drivingschool/
├── client/
├── server/
├── html/          -- Interface NUI pour l'examen du code
│   ├── index.html
│   ├── style.css
│   └── script.js
├── config.lua
└── fxmanifest.lua
```

## Problemes courants

| Probleme | Solution |
|---|---|
| Interface NUI ne s'affiche pas | Verifiez les fichiers dans le dossier html/ |
| Licence non attribuee | Verifiez que esx_license est fonctionnel |
| Vehicule d'examen n'apparait pas | Verifiez les modeles de vehicules dans la config |
