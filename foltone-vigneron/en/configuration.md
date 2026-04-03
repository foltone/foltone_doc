---
title: "Configuration"
description: "Vintner script configuration"
script: "foltone-vigneron"
section: "Vigneron"
order: 2
version: "2.0.0"
---

# Configuration — foltone_vigneron

All settings are in `config.lua`.

## General

```lua
Config.JobName = 'vigne'
Config.SocietyName = 'society_vigne'
Config.MenuSystem = 'rageui'   -- 'rageui' or 'ox_lib'
Config.DiscordWebhook = ''     -- Discord webhook URL
```

## Features

```lua
Config.Features = {
    boss = true, storage = true, locker = true, garage = true,
    processing = true, f6menu = true, bills = true, ads = true, duty = true,
}
```

## Multi-storage

Multiple chests with grade permissions and optional ox_inventory stash support.

## Processing pipeline

| Type | Description |
|------|-------------|
| `harvest` | Gather an item |
| `transform` | Convert items into another |
| `sell` | Sell an item (player + society money) |

## Discord Webhooks

All sensitive actions are logged when `Config.DiscordWebhook` is set.
