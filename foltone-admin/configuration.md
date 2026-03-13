---
title: "Configuration"
description: "Configuration du menu admin"
script: "foltone-admin"
section: "foltone_admin"
order: 2
---

# Configuration — foltone_admin

## Permissions

```lua
Config.AdminGroups = {
    'admin',
    'superadmin',
    'god'
}
```

## Fonctionnalités

Le menu admin inclut :

- **Téléportation** — TP to waypoint, TP to player
- **Gestion joueurs** — Kick, ban, freeze, heal
- **Spawn véhicules** — Spawn par nom de modèle
- **Météo / Heure** — Contrôle du temps en jeu
- **Inventaire** — Donner/retirer items et argent

## Commande

```lua
Config.Command = 'admin'
Config.Key = 'F10' -- Optionnel : touche raccourci
```

## Logs Discord

```lua
Config.WebhookAdmin = '' -- Webhook pour logger les actions admin
```
