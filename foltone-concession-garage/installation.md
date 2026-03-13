---
title: "Installation"
description: "Installation de Concession & Garage V2"
script: "foltone-concession-garage"
section: "foltone_concession-garage"
order: 1
---

# Installation — Concession & Garage V2

## Prérequis

- ESX Legacy
- MySQL / MariaDB

## Installation

1. Téléchargez depuis votre espace Tebex
2. Placez le dossier dans `resources/`
3. Importez le SQL :

```sql
mysql -u root -p votre_base < foltone_concession/sql/install.sql
```

4. Ajoutez dans `server.cfg` :

```ini
ensure foltone_concession
```

## Types de véhicules supportés

Le script gère 4 types de concessions :

- **Voitures** — Concession auto classique
- **Bateaux** — Concession nautique
- **Hélicoptères** — Héliport
- **Avions** — Aéroport

Chaque type peut avoir ses propres points de vente et garages.
