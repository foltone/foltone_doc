---
title: "Installation"
description: "Guide d'installation du script foltone_territories"
script: "foltone-territories"
section: "Territories"
order: 1
version: "1.0.0"
---

# Installation de foltone_territories

## Prerequis

- **ESX Framework** (es_extended)
- **oxmysql** pour la base de donnees
- **RageUI** (inclus ou a installer separement)

## Etapes d'installation

### 1. Telecharger le script

Placez le dossier `foltone_territories` dans votre repertoire `resources/`.

### 2. Importer la base de donnees

Executez le fichier SQL fourni pour creer les tables necessaires (territoires, progression de capture, historique).

### 3. Configurer le server.cfg

Ajoutez la ligne suivante dans votre `server.cfg` :

```cfg
ensure foltone_territories
```

### 4. Ordre de demarrage

```cfg
ensure es_extended
ensure oxmysql
ensure foltone_territories
```

### 5. Configurer les gangs

Assurez-vous que les jobs de gang existent dans votre table `jobs` et correspondent a ceux configures dans le script.

## Verification

1. Redemarrez votre serveur
2. Assignez-vous un job de gang configure
3. Rendez-vous dans une zone de territoire
4. Verifiez que la zone s'affiche correctement sur la carte
5. Testez la vente de drogue a un PNJ dans la zone
6. Verifiez que les points de capture s'incrementent
