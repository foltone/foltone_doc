---
title: "Configuration"
description: "Configuration du système de tickets"
script: "foltone-ticket"
section: "foltone_ticket"
order: 2
version: "1.2.0"
---

# Configuration — foltone_ticket

Ouvrez le fichier `config.lua` à la racine du script.

## Langue

```lua
Config.Locale = 'fr' -- 'fr', 'en', 'es'
```

Le script supporte trois langues nativement. Vous pouvez ajouter vos propres traductions dans le dossier `locales/`.

## Permissions

```lua
Config.AdminGroups = {
    'admin',
    'superadmin',
    'god'
}
```

Seuls les joueurs avec ces groupes pourront voir et gérer les tickets.

## Commandes

```lua
Config.Command = 'ticket' -- Commande pour ouvrir le menu
```

## Notifications

```lua
Config.Notify = function(source, msg, type)
    -- Adaptez à votre système de notification
    -- type: 'success', 'error', 'info'
end
```

## Webhook Discord

```lua
Config.DiscordWebhook = '' -- URL du webhook Discord
Config.DiscordColor = 3447003 -- Couleur de l'embed
```

Laissez vide pour désactiver les notifications Discord.

## Options avancées

```lua
Config.MaxTicketsPerPlayer = 3     -- Tickets max par joueur
Config.AutoCloseAfter = 48         -- Fermeture auto après X heures
Config.SaveHistory = true           -- Garder l'historique
```
