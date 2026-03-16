---
title: "Installation"
description: "Installation of the Foltone FiveM Discord Bot script"
script: "foltone-fivem-discord-bot"
section: "Discord Bot"
order: 1
version: "1.0.0"
---

# Installation — foltone_fivem_discord_bot

## Prerequisites

- **Node.js 18+** — JavaScript runtime for the bot
- **FiveM Server** — Game server with `oxmysql`
- **ESX Legacy** or **QBCore** or **QBX** — FiveM framework
- **oxmysql** — MySQL library

### Optional dependencies

| Dependency | Purpose | Required for |
|-----------|---------|-------------|
| `vMenu` | Admin detection | If `AdminSystem = "vmenu"` |
| `txAdmin` | Admin detection | If `AdminSystem = "txadmin"` |
| `EasyAdmin` | Admin detection | If `AdminSystem = "easyadmin"` |

## Download

Download the script from your Tebex account and place the `foltone_fivem_discord_bot` folder in your `resources/` directory.

## Step 1 — Create the Discord bot

1. Go to the [Discord Developer Portal](https://discord.com/developers/applications)
2. Click **New Application** and give your bot a name
3. In the **Bot** tab:
   - Click **Reset Token** and copy the token (you will need it in `config.lua`)
   - Enable the following **Privileged Gateway Intents**:
     - `SERVER MEMBERS INTENT`
     - `MESSAGE CONTENT INTENT`
4. In the **OAuth2 > URL Generator** tab:
   - Check `bot` and `applications.commands`
   - Check the following permissions: `Send Messages`, `Manage Channels`, `Read Message History`, `Embed Links`, `Attach Files`, `Manage Messages`
   - Copy the generated URL and invite the bot to your Discord server

## Step 2 — Import the database

Run the `sql/install.sql` file in your MySQL database:

```bash
mysql -u root -p your_database < sql/install.sql
```

You can also copy the file contents and run it in phpMyAdmin or HeidiSQL.

## Step 3 — Configure config.lua

Open `config.lua` and fill in the required information:

```lua
Config.Bot = {
    token = "YOUR_TOKEN_HERE",          -- Token copied from the Developer Portal
    guildId = "YOUR_GUILD_ID",          -- Right-click your server > Copy ID
    port = 3847,                         -- Internal communication port (do not change unless conflict)
    authToken = "A_RANDOM_SECRET",      -- Internal secret key (generate a random string)
    autoStart = true,
    healthCheckInterval = 60,
}
```

> **Important**: To get Discord IDs, enable **Developer Mode** in Discord settings (Settings > Advanced > Developer Mode), then right-click a server, channel, or role to copy its ID.

Then configure channel and role IDs as needed. See the [Configuration](./configuration.md) page for details on each section.

## Step 4 — Install Node.js dependencies

```bash
cd resources/foltone_fivem_discord_bot/bot
npm install
```

> This step installs all Node.js dependencies required for the bot to function (discord.js, axios, etc.).

## Step 5 — Server configuration

Add to your `server.cfg`:

```ini
ensure oxmysql
ensure es_extended      # or qb-core / qbx_core
ensure foltone_fivem_discord_bot
```

> **Important**: `foltone_fivem_discord_bot` must start **after** your framework and `oxmysql`.

## Framework

The script supports 3 frameworks and automatic detection:

| Framework | Config value | Dependencies |
|-----------|-------------|--------------|
| Auto-detection | `"auto"` | Automatically detects ESX / QBCore / QBX |
| ESX Legacy | `"esx"` | `es_extended`, `oxmysql` |
| QBCore | `"qbcore"` | `qb-core`, `oxmysql` |
| QBX | `"qbx"` | `qbx_core`, `oxmysql` |

```lua
Config.Framework = "auto" -- "auto", "esx", "qbcore" or "qbx"
```

## Verification

After restarting the server:

1. Check the server console — you should see `[foltone_fivem_discord_bot] Bot connected as YourBotName#1234`
2. In Discord, type `/playerlist` — the list of connected players should appear
3. Connect to the server in-game, type `/adminpanel` (or F7) — the NUI panel should open
4. Check that the dashboard channel updates automatically

> If the bot does not start, make sure Node.js 18+ is installed on your machine and that the `npm install` dependencies have been installed.
