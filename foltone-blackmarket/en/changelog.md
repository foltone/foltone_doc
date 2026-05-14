---
title: "Changelog"
description: "Change history for foltone_blackmarket script"
script: "foltone-blackmarket"
section: "Blackmarket"
order: 4
version: "1.0.0"
---

# Changelog

## v1.0.0 — Initial release

### Added
- Mobile illegal weapons van with random spawn cycle
- Configurable spawn locations (10 LS / countryside presets)
- Multi-framework support (ESX / QBCore / QBox / standalone)
- Multi-inventory support (ox_inventory / qs-inventory / esx / qb)
- Multi-target support (ox_target / qb-target / qtarget) + textUI fallback
- Dual menu : RageUI (in-game) and NUI (HTML/CSS) selectable via `Config.MenuType`
- 3D preview of items with mouse wheel zoom
- Weapon customization tab (components + tints) for player-owned weapons
- Real-time preview when hovering a custom
- Weapon selector with arrows in the customs tab
- ox_inventory metadata persistence (components + tint)
- Encrypted phone item with two-phase blip system (search 161 then van 110)
- Police & heat system (alerts, automatic despawn at threshold)
- Cop nearby detection : dealer flees when police approach (80m radius)
- Stock and price variance per van (+/-30% / +/-10%)
- Reputation gate (optional, `GetPlayerReputation` hook)
- Anti-cheat protections : distance check, cooldown, source validation, atomic transactions
- Server-side weapon ownership check for customs
- Discord webhook logging on every purchase
- Admin command `bm_van spawn/despawn/status`
- Multi-language support (fr / en / es)
- Automatic version check at startup
