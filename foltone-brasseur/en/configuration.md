---
title: "Configuration"
description: "Brewer script configuration"
script: "foltone-brasseur"
section: "Brasseur"
order: 2
version: "2.0.0"
---

# Configuration — foltone_brasseur

## General

```lua
Config.JobName = 'brasseur'
Config.SocietyName = 'society_brasseur'
Config.MenuSystem = 'rageui'   -- 'rageui' or 'ox_lib'
```

## Processing pipeline

| Step | Output | Input | Payment |
|------|--------|-------|---------|
| Harvest | `houblon` | — | — |
| Transform | `biere_blonde` | 1x `houblon` | — |
| Transform | `biere_rousse` | 2x `houblon` | — |
| Sell | — | `biere_blonde` | $5 player + $20 society |
| Sell | — | `biere_rousse` | $15 player + $40 society |

## Multi-storage

3 chests: Main (grade 0), Chef (grade 2), Boss (grade 3).
