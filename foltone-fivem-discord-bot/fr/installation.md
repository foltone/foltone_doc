---
title: "Installation"
description: "Installation du script Foltone FiveM Discord Bot"
script: "foltone-fivem-discord-bot"
section: "Discord Bot"
order: 1
version: "1.0.0"
---

# Installation — foltone_fivem_discord_bot

## Prerequis

- **Node.js 18+** — Runtime JavaScript pour le bot
- **FiveM Server** — Serveur de jeu avec `oxmysql`
- **ESX Legacy** ou **QBCore** ou **QBX** — Framework FiveM
- **oxmysql** — Librairie MySQL

### Dependances optionnelles

| Dependance | Utilite | Requis pour |
|-----------|---------|-------------|
| `vMenu` | Detection admin | Si `AdminSystem = "vmenu"` |
| `txAdmin` | Detection admin | Si `AdminSystem = "txadmin"` |
| `EasyAdmin` | Detection admin | Si `AdminSystem = "easyadmin"` |

## Telechargement

Telechargez le script depuis votre espace Tebex et placez le dossier `foltone_fivem_discord_bot` dans votre repertoire `resources/`.

## Etape 1 — Creer le bot Discord

1. Rendez-vous sur le [Discord Developer Portal](https://discord.com/developers/applications)
2. Cliquez sur **New Application** et donnez un nom a votre bot
3. Dans l'onglet **Bot** :
   - Cliquez sur **Reset Token** et copiez le token (vous en aurez besoin dans `config.lua`)
   - Activez les **Privileged Gateway Intents** suivants :
     - `SERVER MEMBERS INTENT`
     - `MESSAGE CONTENT INTENT`
4. Dans l'onglet **OAuth2 > URL Generator** :
   - Cochez `bot` et `applications.commands`
   - Cochez les permissions : `Send Messages`, `Manage Channels`, `Read Message History`, `Embed Links`, `Attach Files`, `Manage Messages`
   - Copiez l'URL generee et invitez le bot sur votre serveur Discord

## Etape 2 — Importer la base de donnees

Executez le fichier `sql/install.sql` dans votre base de donnees MySQL :

```bash
mysql -u root -p votre_base < sql/install.sql
```

Vous pouvez egalement copier le contenu et l'executer dans phpMyAdmin ou HeidiSQL.

## Etape 3 — Configurer config.lua

Ouvrez `config.lua` et renseignez les informations obligatoires :

```lua
Config.Bot = {
    token = "VOTRE_TOKEN_ICI",          -- Token copie depuis le Developer Portal
    guildId = "ID_DE_VOTRE_SERVEUR",    -- Clic droit sur votre serveur > Copier l'ID
    port = 3847,                         -- Port de communication interne (ne pas changer sauf conflit)
    authToken = "UN_SECRET_ALEATOIRE",  -- Cle secrete interne (generer une chaine aleatoire)
    autoStart = true,
    healthCheckInterval = 60,
}
```

> **Important** : Pour obtenir les IDs Discord, activez le **Mode developpeur** dans les parametres Discord (Parametres > Avance > Mode developpeur), puis faites clic droit sur un serveur, canal ou role pour copier son ID.

Configurez ensuite les IDs de canaux et de roles selon vos besoins. Consultez la page [Configuration](./configuration.md) pour le detail de chaque section.

## Etape 4 — Installer les dependances Node.js

```bash
cd resources/foltone_fivem_discord_bot/bot
npm install
```

> Cette etape installe toutes les dependances Node.js necessaires au fonctionnement du bot (discord.js, axios, etc.).

## Etape 5 — Configuration serveur

Ajoutez dans votre `server.cfg` :

```ini
ensure oxmysql
ensure es_extended      # ou qb-core / qbx_core
ensure foltone_fivem_discord_bot
```

> **Important** : `foltone_fivem_discord_bot` doit etre demarre **apres** votre framework et `oxmysql`.

## Framework

Le script supporte 3 frameworks et la detection automatique :

| Framework | Valeur config | Dependances |
|-----------|--------------|-------------|
| Auto-detection | `"auto"` | Detecte automatiquement ESX / QBCore / QBX |
| ESX Legacy | `"esx"` | `es_extended`, `oxmysql` |
| QBCore | `"qbcore"` | `qb-core`, `oxmysql` |
| QBX | `"qbx"` | `qbx_core`, `oxmysql` |

```lua
Config.Framework = "auto" -- "auto", "esx", "qbcore" ou "qbx"
```

## Verification

Apres redemarrage du serveur :

1. Verifiez la console serveur — vous devriez voir `[foltone_fivem_discord_bot] Bot connected as VotreBotName#1234`
2. Dans Discord, tapez `/playerlist` — la liste des joueurs connectes doit s'afficher
3. Connectez-vous au serveur en jeu, tapez `/adminpanel` (ou F7) — le panel NUI doit s'ouvrir
4. Verifiez que le canal dashboard se met a jour automatiquement

> Si le bot ne demarre pas, verifiez que Node.js 18+ est bien installe sur votre machine et que les dependances `npm install` ont ete executees.
