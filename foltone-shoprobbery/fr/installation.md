---
title: "Installation"
description: "Guide d'installation du script foltone_shoprobbery"
script: "foltone-shoprobbery"
section: "Shop Robbery"
order: 1
version: "1.0.0"
---

# Installation de foltone_shoprobbery

## Prerequis

- **ESX Framework** (es_extended)
- **oxmysql** pour la base de donnees
- **RageUI** (inclus ou a installer separement)

## Etapes d'installation

### 1. Telecharger le script

Placez le dossier `foltone_shoprobbery` dans votre repertoire `resources/`.

### 2. Importer la base de donnees

Executez le fichier SQL fourni pour creer les tables necessaires (cooldowns, logs de braquages).

### 3. Configurer le server.cfg

Ajoutez la ligne suivante dans votre `server.cfg` :

```cfg
ensure foltone_shoprobbery
```

### 4. Ordre de demarrage

```cfg
ensure es_extended
ensure oxmysql
ensure foltone_shoprobbery
```

### 5. Configurer les notifications police

Adaptez les fonctions de notification dans le config pour correspondre a votre systeme de dispatch (telephone, MDT, etc.).

## Verification

1. Redemarrez votre serveur
2. Rendez-vous dans une supérette
3. Verifiez que le menu boutique fonctionne (achat d'items)
4. Testez le braquage avec le nombre de policiers requis en service
5. Verifiez que les alertes police sont envoyees correctement
