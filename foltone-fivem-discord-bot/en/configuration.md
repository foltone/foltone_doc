---
title: "Configuration"
description: "Configuration of the Foltone FiveM Discord Bot script"
script: "foltone-fivem-discord-bot"
section: "Discord Bot"
order: 2
version: "1.0.0"
---

# Configuration — foltone_fivem_discord_bot

All configuration is done in the `config.lua` file at the root of the script.

## Language

```lua
Config.Locale = "en" -- "fr" or "en"
```

Translations are in the `locales/` folder. You can add your own languages by creating a new file (e.g., `locales/de.lua`).

## Framework

```lua
Config.Framework = "auto" -- "auto", "esx", "qbcore" or "qbx"
```

| Value | Framework | Description |
|-------|-----------|-------------|
| `"auto"` | Auto-detection | Automatically detects ESX / QBCore / QBX at startup |
| `"esx"` | ESX Legacy | Forces ESX usage |
| `"qbcore"` | QBCore | Forces QBCore usage |
| `"qbx"` | QBX | Forces QBX usage |

## Debug Mode

```lua
Config.Debug = false
```

Set to `true` to enable detailed logs in the server console. Disable in production.

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

| Parameter | Description |
|-----------|-------------|
| `token` | Discord bot token (obtained from the Developer Portal) |
| `guildId` | Target Discord server ID |
| `port` | Internal HTTP communication port between FiveM and the Node.js bot |
| `authToken` | Shared secret key between FiveM and the bot (internal security) |
| `autoStart` | `true` to start the bot automatically with the resource |
| `healthCheckInterval` | Seconds between each bot health check |

> **Security**: Never share your `token` or `authToken`. These values are in `config.lua` (open file), be careful with server access.

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
        commands = {"*"}    -- * = access to all commands
    }
}
```

| Parameter | Description |
|-----------|-------------|
| Key (e.g., `"moderator"`) | Permission group name (custom) |
| `roleIds` | List of Discord role IDs with this access level |
| `commands` | List of allowed commands, or `{"*"}` to allow all |

### Available commands by category

| Category | Commands |
|----------|----------|
| Players | `playerlist`, `playerinfo`, `kick`, `ban`, `unban` |
| Moderation | `warn`, `mute`, `unmute`, `freeze`, `unfreeze`, `slap`, `heal`, `spectate` |
| Economy | `givemoney`, `removemoney`, `setmoney`, `giveitem`, `removeitem` |
| Vehicles | `spawnvehicle`, `deletevehicle` |
| Teleportation | `tp`, `revive` |
| Job | `setjob` |
| Server | `announce`, `weather`, `time`, `whitelist` |
| Tracking | `sanctions`, `watchlist` |
| Scheduling | `schedule` |
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

| Parameter | Description |
|-----------|-------------|
| `enabled` | Enable/disable the logs system |
| `mode` | `"single"` = one channel for all logs, `"split"` = one channel per type |
| `channels.single` | Single channel ID (used if `mode = "single"`) |
| `channels.connection` | Channel for player connections/disconnections |
| `channels.death` | Channel for player deaths |
| `channels.transaction` | Channel for economy transactions |
| `channels.admin` | Channel for admin actions |
| `channels.chat` | Channel for in-game chat |
| `transactionThreshold` | Minimum amount to log a transaction |
| `maskIP` | `true` to hide player IPs in logs |
| `actionButtons` | `true` to show quick action buttons on embeds |

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

| Parameter | Description |
|-----------|-------------|
| `enabled` | Enable/disable the dashboard |
| `channelId` | Channel ID where the dashboard is displayed |
| `refreshInterval` | Seconds between each automatic update |
| `showPlayerList` | Show player list in the dashboard |
| `showAdminActions` | Show recent admin actions |
| `showConnections` | Show recent connections |
| `buttons` | Show quick action buttons under the dashboard |

> The dashboard shows a real-time updated embed with server statistics.

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

| Parameter | Description |
|-----------|-------------|
| `enabled` | Enable/disable the ticket system |
| `categoryId` | Discord category ID where ticket channels are created |
| `logsChannelId` | Log channel ID for closed tickets |
| `maxOpenPerPlayer` | Maximum open tickets per player simultaneously |
| `autoCloseAfter` | Minutes before auto-closing an inactive ticket (1440 = 24h) |
| `transcriptEnabled` | `true` to save transcripts of closed tickets |
| `command` | FiveM command to open a ticket from the game |
| `keybind` | Shortcut key to open a ticket from the game |

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

| Parameter | Description |
|-----------|-------------|
| `enabled` | Enable/disable chat synchronization |
| `channelId` | Discord channel ID linked to in-game chat |
| `mode` | `"all"` = all messages, `"discord_only"` = Discord to game only, `"game_only"` = game to Discord only |
| `discordPrefix` | Prefix shown in-game before Discord messages |
| `discordColor` | RGB color for Discord messages in-game |
| `webhookName` | Name shown on the Discord webhook |
| `filterLinks` | `true` to block links in chat |
| `maxLength` | Maximum length of synchronized messages |

## Alerts

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

| Parameter | Description |
|-----------|-------------|
| `enabled` | Enable/disable the alerts system |
| `channelId` | Channel ID where alerts are sent |
| `mentionRoleId` | Role ID mentioned in urgent alerts |
| `cooldownPerPlayer` | Seconds between two alerts for the same player |
| `cooldownGlobal` | Seconds between two global alerts |

### Alert rules

| Rule | Parameters | Description |
|------|------------|-------------|
| `warns` | `count`, `period` | Alert if a player receives X warnings in Y minutes |
| `transaction` | `threshold` | Alert if a transaction exceeds the threshold |
| `playersLow` | `threshold` | Alert if player count drops below threshold |
| `playersHigh` | `threshold` | Alert if player count exceeds threshold |
| `watchlist` | — | Alert when a watched player connects |
| `kills` | `count`, `period` | Alert if a player kills X players in Y minutes |
| `crashDetect` | `count`, `period` | Alert if X players disconnect in Y minutes |

## Scheduler

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

| Parameter | Description |
|-----------|-------------|
| `enabled` | Enable/disable the scheduler |
| `tasks` | List of scheduled tasks |
| `tasks[].name` | Unique task name |
| `tasks[].type` | Type: `"restart"` (server restart) or `"announce"` (announcement) |
| `tasks[].cron` | Cron expression for scheduling |
| `tasks[].countdownMinutes` | Minutes before restart to send warnings |

## NUI Panel

```lua
Config.Panel = {
    enabled = true,
    command = "adminpanel",
    keybind = "F7",
    refreshInterval = 15,
    logsMaxDisplay = 100,
}
```

| Parameter | Description |
|-----------|-------------|
| `enabled` | Enable/disable the in-game admin NUI panel |
| `command` | Command to open the panel |
| `keybind` | Shortcut key to open/close the panel |
| `refreshInterval` | Seconds between each automatic data refresh |
| `logsMaxDisplay` | Maximum number of logs displayed in the panel logs tab |

## Database

```lua
Config.Database = {
    logRetentionDays = 30,
    purgeInterval = 1440,
}
```

| Parameter | Description |
|-----------|-------------|
| `logRetentionDays` | Number of days to retain logs before automatic deletion |
| `purgeInterval` | Minutes between each automatic database cleanup |

## Admin system

```lua
Config.AdminSystem = "auto"
```

| Value | Description |
|-------|-------------|
| `"auto"` | Automatic detection (ACE, vMenu, txAdmin, EasyAdmin) |
| `"ace"` | Native FiveM ACE permissions (`IsPlayerAceAllowed`) |
| `"vmenu"` | vMenu permission system |
| `"txadmin"` | txAdmin permission system |
| `"easyadmin"` | EasyAdmin permission system |
| `"custom"` | Custom function in `server/sv_editable.lua` |
