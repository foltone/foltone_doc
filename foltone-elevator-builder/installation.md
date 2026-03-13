---
title: "Installation"
description: "Installation d'Elevator Builder"
script: "foltone-elevator-builder"
section: "foltone_elevator-builder"
order: 1
---

# Installation — Elevator Builder

## Prérequis

- ESX Legacy, QB-Core ou Standalone
- MySQL / MariaDB

## Installation

1. Téléchargez depuis votre espace Tebex
2. Placez dans `resources/`
3. Importez le SQL :

```sql
mysql -u root -p votre_base < foltone_elevator/sql/install.sql
```

4. `server.cfg` :

```ini
ensure foltone_elevator
```

## Créer un ascenseur

En jeu, utilisez la commande admin :

```
/elevator create
```

Suivez l'interface NUI pour :
1. Définir le nom de l'ascenseur
2. Placer les étages (position + label)
3. Sauvegarder

Les ascenseurs sont sauvegardés en base de données et persistent après restart.
