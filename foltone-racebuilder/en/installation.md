---
title: "Installation"
description: "Race Builder installation guide"
script: "foltone-racebuilder"
section: "foltone_racebuilder"
order: 1
version: "1.0.0"
---

# Installation — foltone_racebuilder

## Requirements

- **ESX Legacy** or **QBCore** or **Standalone** — Framework
- **oxmysql** — Database driver
- **ox_lib** *(optional)* — Enhanced UI (context menus, input dialogs). A built-in fallback is included if ox_lib is not installed.
- **ox_target** or **qb-target** *(optional)* — 3D interaction with NPC. Falls back to E key proximity if neither is installed.

## Database

The script will automatically create the required tables on first start:

- `foltone_races` — Stores race data (checkpoints, spawn points, settings)
- `foltone_race_leaderboard` — Player best times per race
- `foltone_race_sessions` — Multiplayer session history

## Download

Download the script from your [Tebex](https://foltone.tebex.io/) account and place the `foltone_racebuilder` folder in your `resources/` directory.

## Server Configuration

Add to your `server.cfg`:

```ini
ensure oxmysql
ensure es_extended       # or qb-core (optional for standalone)
ensure ox_lib            # optional but recommended
ensure ox_target         # optional (or qb-target)
ensure foltone_racebuilder
```

> **Important**: `foltone_racebuilder` must start **after** oxmysql and your framework.

## Verification

After restarting your server:

1. Connect to the server
2. Use `/raceeditor` to open the race editor (requires admin permission)
3. Create a test race: place NPC, spawn point, and at least 2 checkpoints
4. Interact with the NPC to open the race menu and start a solo time trial
