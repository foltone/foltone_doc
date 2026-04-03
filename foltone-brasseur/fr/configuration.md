---
title: "Configuration"
description: "Configuration du script Brasseur"
script: "foltone-brasseur"
section: "Brasseur"
order: 2
version: "2.0.0"
---

# Configuration — foltone_brasseur

Toute la configuration se fait dans `config.lua`.

## Paramètres généraux

```lua
Config.JobName = 'brasseur'
Config.SocietyName = 'society_brasseur'
Config.EventPrefix = 'foltone_brasseur'
Config.MenuSystem = 'rageui'   -- 'rageui' ou 'ox_lib'
```

## Features

```lua
Config.Features = {
    boss = true, storage = true, locker = true, garage = true,
    processing = true, f6menu = true, bills = true, ads = true, duty = true,
}
```

## Multi-coffres

3 coffres avec grade minimum :

| Coffre | Grade requis |
|--------|-------------|
| Coffre Principal | 0 (tous) |
| Coffre Chef | 2 |
| Coffre Patron | 3 |

## Pipeline de production

| Étape | Item produit | Item requis | Quantité | Paiement |
|-------|-------------|-------------|----------|----------|
| Récolte | `houblon` | — | max 200 | — |
| Transformation | `biere_blonde` | 1x `houblon` | max 100 | — |
| Transformation | `biere_rousse` | 2x `houblon` | max 100 | — |
| Vente | — | `biere_blonde` | — | $5 joueur + $20 société |
| Vente | — | `biere_rousse` | — | $15 joueur + $40 société |

## Discord Webhooks

```lua
Config.DiscordWebhook = 'https://discord.com/api/webhooks/...'
```
