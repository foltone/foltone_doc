---
title: "Installation"
description: "Installation du système de tickets"
script: "foltone-ticket"
section: "foltone_ticket"
order: 1
version: "1.2.0"
---

# Installation — foltone_ticket

## Téléchargement

```bash
cd resources
git clone https://github.com/foltone/foltone_ticket
```

## Configuration serveur

Ajoutez dans votre `server.cfg` :

```ini
ensure foltone_ticket
```

## Dépendances

- **Framework** : ESX Legacy, QB-Core ou Standalone
- **Menu** : RageUI (inclus)

Aucune dépendance externe requise. Le script est 100% standalone-compatible.

## Vérification

Après restart, tapez `/ticket` en jeu pour ouvrir le menu.

Performance : **0.00ms** en idle.
