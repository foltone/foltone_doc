---
title: "Configuration"
description: "Configuration du script Foltone FiveM Discord Bot"
script: "foltone-fivem-discord-bot"
section: "Discord Bot"
order: 2
version: "1.0.0"
---

# Configuration — foltone_fivem_discord_bot

Toute la configuration se fait dans le fichier `config.lua` a la racine du script.

## Langue

```lua
Config.Locale = "en" -- "fr" ou "en"
```

Les traductions sont dans le dossier `locales/`. Vous pouvez ajouter vos propres langues en creant un nouveau fichier (ex: `locales/de.lua`).

## Framework

```lua
Config.Framework = "auto" -- "auto", "esx", "qbcore" ou "qbx"
```

| Valeur | Framework | Description |
|--------|-----------|-------------|
| `"auto"` | Auto-detection | Detecte ESX / QBCore / QBX automatiquement au demarrage |
| `"esx"` | ESX Legacy | Force l'utilisation d'ESX |
| `"qbcore"` | QBCore | Force l'utilisation de QBCore |
| `"qbx"` | QBX | Force l'utilisation de QBX |

## Mode Debug

```lua
Config.Debug = false
```

Passez a `true` pour activer les logs detailles dans la console serveur. A desactiver en production.

## Bot

```lua
Config.Bot = {
    token = "YOUR_BOT_TOKEN",
    guildId = "YOUR_GUILD_ID",
    port = 3847,
    authToken = "RANDOM_SECRET",
    autoStart = true,
    healthCheckInterval = 60,
}
```

| Parametre | Description |
|-----------|-------------|
| `token` | Token du bot Discord (obtenu depuis le Developer Portal) |
| `guildId` | ID du serveur Discord cible |
| `port` | Port de communication HTTP interne entre FiveM et le bot Node.js |
| `authToken` | Cle secrete partagee entre FiveM et le bot (securite interne) |
| `autoStart` | `true` pour demarrer le bot automatiquement avec la resource |
| `healthCheckInterval` | Intervalle en secondes entre chaque verification de sante du bot |

> **Securite** : Ne partagez jamais votre `token` ou `authToken`. Ces valeurs sont dans `config.lua` (fichier ouvert), soyez vigilants avec les acces a votre serveur.

## Permissions

```lua
Config.Permissions = {
    ["moderator"] = {
        roleIds = {"ROLE_ID"},
        commands = {
            "kick", "warn", "mute", "unmute", "freeze", "unfreeze",
            "playerlist", "playerinfo", "slap", "heal", "spectate"
        }
    },
    ["admin"] = {
        roleIds = {"ROLE_ID"},
        commands = {
            "ban", "unban", "tp", "revive", "setjob",
            "givemoney", "removemoney", "setmoney",
            "giveitem", "removeitem",
            "spawnvehicle", "deletevehicle",
            "sanctions", "announce", "weather", "time",
            "whitelist", "watchlist"
        }
    },
    ["founder"] = {
        roleIds = {"ROLE_ID"},
        commands = {"*"}    -- * = acces a toutes les commandes
    }
}
```

| Parametre | Description |
|-----------|-------------|
| Cle (ex: `"moderator"`) | Nom du groupe de permissions (libre) |
| `roleIds` | Liste des IDs de roles Discord ayant ce niveau d'acces |
| `commands` | Liste des commandes autorisees, ou `{"*"}` pour tout autoriser |

### Commandes disponibles par categorie

| Categorie | Commandes |
|-----------|-----------|
| Joueurs | `playerlist`, `playerinfo`, `kick`, `ban`, `unban` |
| Moderation | `warn`, `mute`, `unmute`, `freeze`, `unfreeze`, `slap`, `heal`, `spectate` |
| Economie | `givemoney`, `removemoney`, `setmoney`, `giveitem`, `removeitem` |
| Vehicules | `spawnvehicle`, `deletevehicle` |
| Teleportation | `tp`, `revive` |
| Emploi | `setjob` |
| Serveur | `announce`, `weather`, `time`, `whitelist` |
| Suivi | `sanctions`, `watchlist` |
| Planification | `schedule` |
| Info | `serverstatus` |

## Logs

```lua
Config.Logs = {
    enabled = true,
    mode = "split",
    channels = {
        single = "CHANNEL_ID",
        connection = "CHANNEL_ID",
        death = "CHANNEL_ID",
        transaction = "CHANNEL_ID",
        admin = "CHANNEL_ID",
        chat = "CHANNEL_ID",
    },
    transactionThreshold = 50000,
    maskIP = true,
    actionButtons = true,
}
```

| Parametre | Description |
|-----------|-------------|
| `enabled` | Activer/desactiver le systeme de logs |
| `mode` | `"single"` = un seul canal pour tous les logs, `"split"` = un canal par type |
| `channels.single` | ID du canal unique (utilise si `mode = "single"`) |
| `channels.connection` | Canal pour les connexions/deconnexions |
| `channels.death` | Canal pour les morts de joueurs |
| `channels.transaction` | Canal pour les transactions economiques |
| `channels.admin` | Canal pour les actions administratives |
| `channels.chat` | Canal pour le chat in-game |
| `transactionThreshold` | Montant minimum pour logger une transaction |
| `maskIP` | `true` pour masquer les IPs des joueurs dans les logs |
| `actionButtons` | `true` pour afficher des boutons d'action rapide sur les embeds |

## Dashboard

```lua
Config.Dashboard = {
    enabled = true,
    channelId = "CHANNEL_ID",
    refreshInterval = 30,
    showPlayerList = true,
    showAdminActions = true,
    showConnections = true,
    buttons = true,
}
```

| Parametre | Description |
|-----------|-------------|
| `enabled` | Activer/desactiver le dashboard |
| `channelId` | ID du canal ou le dashboard est affiche |
| `refreshInterval` | Intervalle en secondes entre chaque mise a jour automatique |
| `showPlayerList` | Afficher la liste des joueurs dans le dashboard |
| `showAdminActions` | Afficher les dernieres actions admin |
| `showConnections` | Afficher les dernieres connexions |
| `buttons` | Afficher les boutons d'action rapide sous le dashboard |

> Le dashboard affiche un embed mis a jour en temps reel avec les statistiques du serveur.

## Tickets

```lua
Config.Tickets = {
    enabled = true,
    categoryId = "CHANNEL_ID",
    logsChannelId = "CHANNEL_ID",
    maxOpenPerPlayer = 2,
    autoCloseAfter = 1440,
    transcriptEnabled = true,
    command = "ticket",
    keybind = "F6",
}
```

| Parametre | Description |
|-----------|-------------|
| `enabled` | Activer/desactiver le systeme de tickets |
| `categoryId` | ID de la categorie Discord ou les canaux de tickets sont crees |
| `logsChannelId` | ID du canal de logs pour les tickets fermes |
| `maxOpenPerPlayer` | Nombre maximum de tickets ouverts simultanement par joueur |
| `autoCloseAfter` | Duree en minutes avant fermeture automatique d'un ticket inactif (1440 = 24h) |
| `transcriptEnabled` | `true` pour sauvegarder le transcript des tickets fermes |
| `command` | Commande FiveM pour ouvrir un ticket depuis le jeu |
| `keybind` | Touche raccourci pour ouvrir un ticket depuis le jeu |

## Chat

```lua
Config.Chat = {
    enabled = true,
    channelId = "CHANNEL_ID",
    mode = "all",
    discordPrefix = "[DISCORD]",
    discordColor = {59, 130, 246},
    webhookName = "FiveM Chat",
    filterLinks = true,
    maxLength = 500,
}
```

| Parametre | Description |
|-----------|-------------|
| `enabled` | Activer/desactiver la synchronisation du chat |
| `channelId` | ID du canal Discord lie au chat in-game |
| `mode` | `"all"` = tous les messages, `"discord_only"` = Discord vers jeu uniquement, `"game_only"` = jeu vers Discord uniquement |
| `discordPrefix` | Prefixe affiche en jeu devant les messages Discord |
| `discordColor` | Couleur RGB des messages Discord en jeu |
| `webhookName` | Nom affiche sur le webhook Discord |
| `filterLinks` | `true` pour bloquer les liens dans le chat |
| `maxLength` | Longueur maximale des messages synchronises |

## Alertes

```lua
Config.Alerts = {
    enabled = true,
    channelId = "CHANNEL_ID",
    mentionRoleId = "ROLE_ID",
    cooldownPerPlayer = 30,
    cooldownGlobal = 10,
    rules = {
        warns = { enabled = true, count = 3, period = 1440 },
        transaction = { enabled = true, threshold = 500000 },
        playersLow = { enabled = true, threshold = 5 },
        playersHigh = { enabled = true, threshold = 60 },
        watchlist = { enabled = true },
        kills = { enabled = true, count = 5, period = 10 },
        crashDetect = { enabled = true, count = 10, period = 5 },
    }
}
```

| Parametre | Description |
|-----------|-------------|
| `enabled` | Activer/desactiver le systeme d'alertes |
| `channelId` | ID du canal ou les alertes sont envoyees |
| `mentionRoleId` | ID du role mentionne dans les alertes urgentes |
| `cooldownPerPlayer` | Secondes entre deux alertes pour le meme joueur |
| `cooldownGlobal` | Secondes entre deux alertes globales |

### Regles d'alerte

| Regle | Parametre | Description |
|-------|-----------|-------------|
| `warns` | `count`, `period` | Alerte si un joueur recoit X avertissements en Y minutes |
| `transaction` | `threshold` | Alerte si une transaction depasse le seuil |
| `playersLow` | `threshold` | Alerte si le nombre de joueurs passe sous le seuil |
| `playersHigh` | `threshold` | Alerte si le nombre de joueurs depasse le seuil |
| `watchlist` | — | Alerte quand un joueur surveille se connecte |
| `kills` | `count`, `period` | Alerte si un joueur tue X joueurs en Y minutes |
| `crashDetect` | `count`, `period` | Alerte si X joueurs quittent le serveur en Y minutes |

## Planificateur

```lua
Config.Scheduler = {
    enabled = true,
    tasks = {
        {
            name = "daily_restart",
            type = "restart",
            cron = "0 4 * * *",
            countdownMinutes = {30, 15, 5, 1},
        },
    }
}
```

| Parametre | Description |
|-----------|-------------|
| `enabled` | Activer/desactiver le planificateur |
| `tasks` | Liste des taches programmees |
| `tasks[].name` | Nom unique de la tache |
| `tasks[].type` | Type : `"restart"` (redemarrage serveur) ou `"announce"` (annonce) |
| `tasks[].cron` | Expression cron pour la planification |
| `tasks[].countdownMinutes` | Minutes avant le restart ou envoyer des avertissements |

## Panel NUI

```lua
Config.Panel = {
    enabled = true,
    command = "adminpanel",
    keybind = "F7",
    refreshInterval = 15,
    logsMaxDisplay = 100,
}
```

| Parametre | Description |
|-----------|-------------|
| `enabled` | Activer/desactiver le panel NUI admin in-game |
| `command` | Commande pour ouvrir le panel |
| `keybind` | Touche raccourci pour ouvrir/fermer le panel |
| `refreshInterval` | Intervalle en secondes entre chaque refresh automatique des donnees |
| `logsMaxDisplay` | Nombre maximum de logs affiches dans l'onglet logs du panel |

## Base de donnees

```lua
Config.Database = {
    logRetentionDays = 30,
    purgeInterval = 1440,
}
```

| Parametre | Description |
|-----------|-------------|
| `logRetentionDays` | Nombre de jours de conservation des logs avant suppression automatique |
| `purgeInterval` | Intervalle en minutes entre chaque nettoyage automatique de la base |

## Systeme admin

```lua
Config.AdminSystem = "auto"
```

| Valeur | Description |
|--------|-------------|
| `"auto"` | Detection automatique (ACE, vMenu, txAdmin, EasyAdmin) |
| `"ace"` | Permissions ACE natives FiveM (`IsPlayerAceAllowed`) |
| `"vmenu"` | Systeme de permissions vMenu |
| `"txadmin"` | Systeme de permissions txAdmin |
| `"easyadmin"` | Systeme de permissions EasyAdmin |
| `"custom"` | Fonction personnalisee dans `server/sv_editable.lua` |
