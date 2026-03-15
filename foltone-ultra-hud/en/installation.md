---
title: "Installation"
description: "Ultra HUD installation guide"
script: "foltone-ultra-hud"
section: "foltone_ultra_hud"
order: 1
version: "1.0.0"
---

# Installation — foltone_ultra_hud

## Requirements

- **ESX Legacy** or **QBCore** or **QBX** or **Standalone** — Framework (auto-detected)

> No database required. Settings are stored in a JSON file.

## Download

Download the script from your [Tebex](https://foltone.tebex.io/) account and place the `foltone_ultra_hud` folder in your `resources/` directory.

## Server Configuration

Add to your `server.cfg`:

```ini
ensure es_extended       # or qb-core / qbx_core (optional for standalone)
ensure foltone_ultra_hud
```

> **Important**: `foltone_ultra_hud` must start **after** your framework. If running standalone, no framework dependency is needed.

## Framework

The script **auto-detects** your framework at startup. No manual configuration is needed.

| Framework | Detection | Hunger/Thirst source |
|---|---|---|
| ESX Legacy | `es_extended` started | `esx_status` |
| QBCore | `qb-core` started | `PlayerData.metadata` |
| QBX | `qbx_core` started | `PlayerData.metadata` |
| Standalone | No framework found | Returns `100, 100` |

The detected framework is printed in the server console:

```
[foltone_ultra_hud] Framework detected: esx
```

## Verification

After restarting your server:

1. Connect to the server with a character
2. The HUD should appear automatically with all status bars, wallet info and position
3. Try the admin command (default: `/hudadmin`) to open the configuration panel
4. Try `/testnotif all` to test all notification types

> If the HUD doesn't appear, check the server console (F8) and client console for errors. Make sure your framework is started before `foltone_ultra_hud`.
