---
title: "Changelog"
description: "Foltone Race Builder version history"
script: "foltone-racebuilder"
section: "Race Builder"
order: 99
version: "1.1.0"
---

# Changelog

## v1.1.0 — 2026-03-16

### Editor improvements
- Edit race properties (name, vehicle, type, laps, max players) on existing races from the checkpoint manager
- Editing a race now opens the checkpoint manager directly instead of placement mode
- Start/finish marker preview visible in real-time during spawn placement
- Improved start grid preview with circular markers and numbered positions
- Grid positions moved further from the start line (`StartOffset` config option)
- Closing the checkpoint manager (X or close) now returns to checkpoint placement mode

### Bug fixes
- Fixed checkpoint markers not appearing after script restart (Lua 5.4 integer/float compatibility with DrawMarker native)
- Fixed `restorePlayerBucket` nil error caused by function declaration order
- Fixed `getRaces` callback not returning checkpoint data, causing empty checkpoint list when editing races
- Fixed NUI state inconsistencies when navigating between editor form and checkpoint manager
- Fixed preview checkpoint artifact when closing checkpoint manager
- Fixed `editorNpcPoint` not being saved/restored during test race
- Prevented duplicate placement loop threads with guard flag

## v1.0.0 — 2026-03-10
- Initial release
- Full race creation system
- In-game checkpoint editor
- Leaderboards and timers
- QB-Core and ESX support
