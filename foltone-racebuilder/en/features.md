---
title: "Features"
description: "Race Builder features overview"
script: "foltone-racebuilder"
section: "Race Builder"
order: 3
version: "1.0.0"
---

# Features — foltone_racebuilder

## Race Editor (`/raceeditor`)

- **Noclip camera** — Fly around the map to place checkpoints
- **NPC placement** — Place an interactive NPC ped with preview
- **Spawn point / Start grid** — F1-style staggered grid for multiplayer races
- **Checkpoint placement** — Click to place, right-click to grab and move existing ones
- **Adjustable checkpoint size** — Scroll wheel to resize each checkpoint individually
- **Checkpoint rotation** — Q/E keys to rotate checkpoint heading
- **Checkpoint manager** — Enter key opens a menu to reorder, teleport, delete checkpoints
- **Test race** — Test your race directly from the editor
- **Edit existing races** — Load and modify any saved race
- **AZERTY/QWERTY auto-detection**

## Race Modes

### Solo Time Trial
- Player races alone against the clock
- Best times saved to leaderboard
- Personal records tracked per player

### Multiplayer (Simultaneous)
- Lobby system with host controls
- F1-style start grid with staggered positions
- Live position tracking during race
- Real-time standings broadcast to all players
- Final results screen with rankings

### Both
- Race supports both solo and multiplayer modes

## Race Features

- **Loop circuits** — Start line is also the finish, with multiple laps
- **Lap time tracking** — Individual lap times displayed in HUD
- **GPS route** — Blip with GPS path to next checkpoint
- **Countdown freeze** — Vehicle frozen during countdown
- **Vehicle exit detection** — DQ after configurable timeout
- **Death detection** — Race ends if player dies
- **Quit confirmation** — F5 to quit with confirmation dialog
- **Instanced races** — FiveM routing buckets for isolated race instances

## Vehicle System

- **Forced vehicle** — Race can require a specific vehicle model
- **Multiple vehicles** — Comma-separated list, random pick or player choice
- **Free choice** — Leave empty for any vehicle
- **Vehicle picker UI** — Visual vehicle selection with images from `config_vehicles.lua`

## Admin Commands

| Command | Description |
|---------|-------------|
| `/raceeditor` | Open the race editor (requires admin) |
| `/cancelrace [raceId]` | Cancel an active race/lobby |
| `/kickrace [playerId]` | Kick a player from their current race |

## Interaction Systems

The script supports multiple interaction methods (auto-detected):

1. **ox_target** — 3D target interaction with NPC ped
2. **qb-target** — 3D target interaction with NPC ped
3. **E key fallback** — Proximity-based interaction if no target system is installed
