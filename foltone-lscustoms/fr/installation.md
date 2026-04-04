---
title: "Installation"
description: "Guide d'installation du script foltone_lscustoms"
script: "foltone-lscustoms"
section: "LS Customs"
order: 1
version: "1.0.0"
---

# Installation de foltone_lscustoms

## Prerequis

- **ESX Framework** (es_extended)
- **oxmysql** pour la base de donnees
- **RageUI** (inclus ou a installer separement)

## Etapes d'installation

### 1. Telecharger le script

Placez le dossier `foltone_lscustoms` dans votre repertoire `resources/`.

### 2. Importer la base de donnees

Executez le fichier SQL fourni pour creer les tables necessaires (factures, logs de modifications, etc.).

### 3. Configurer le server.cfg

Ajoutez la ligne suivante dans votre `server.cfg` :

```cfg
ensure foltone_lscustoms
```

### 4. Ordre de demarrage

```cfg
ensure es_extended
ensure oxmysql
ensure foltone_lscustoms
```

### 5. Desactiver les mecaniciens par defaut

Si vous utilisez un autre script de mecanicien (version job), assurez-vous qu'il n'y a pas de conflit. Ce script est **standalone** et ne necessite aucun job.

## Verification

1. Redemarrez votre serveur
2. Rendez-vous a un point LS Customs sur la carte
3. Entrez dans la zone avec un vehicule
4. Verifiez que le menu RageUI s'ouvre et que l'apercu en direct fonctionne
5. Testez une mission de depannage NPC
