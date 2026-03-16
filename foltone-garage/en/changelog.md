---
title: "Changelog"
description: "Version history of Foltone Garage"
script: "foltone-garage"
section: "Foltone Garage"
order: 99
version: "2.0.0"
---

# Changelog

## v2.0.0 — 2026-03-16

### Added
- Full script rewrite (architecture, security, design)
- New NUI panel with 4 tabs (vehicles, store, pound, label)
- RageUI fallback configurable via `Config.MenuType`
- Multi-target support: ox_target, qb-target, interact, drawtext, marker
- Pound system with dynamic pricing (basePrice + pricePerHour, min/max cap)
- Custom vehicle labels (NUI exclusive, 30 characters max)
- Service vehicles for job garages (spawnable model list)
- Native QBX support alongside ESX and QBCore
- Secure custom callback system (`RegisterServerFoltoneGRCallback`)
- Rate limiting on all server events
- Server-side validation on all operations

### Changed
- Garage configuration moved to `config_garage.lua` (separation of config and logic)
- Pound price calculated server-side (prevents client-side manipulation)
- Vehicles organized by type (car, boat, plane, heli) with individual enable toggle
