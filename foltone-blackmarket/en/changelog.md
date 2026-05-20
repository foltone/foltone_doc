---
title: "Changelog"
description: "Change history for foltone_blackmarket script"
script: "foltone-blackmarket"
section: "Blackmarket"
order: 4
version: "1.1.0"
---

# Changelog

## v1.1.0 — i18n robustness + bugfixes

### Added
- Full **German** (`de.lua`) and **Spanish** (`es.lua`) locales
- New translation keys : `rui_price_format`, `rui_price_stock_format`, `rui_component_suffix`, `rui_tint_suffix`, `rui_weapon_list_title`, `ui_html_title`, `ui_close_tooltip`, `ui_select_weapon` (replace hardcoded strings in RageUI and NUI)
- HTML `data-i18n-title` attribute support in the NUI (translatable tooltips)
- `configuration.md` rewritten with **every** Config option : `MenuType` modes (nui/rageui), `TargetSystem` variants, RageUI themes (`classic`/`modern`) with visual descriptions, available banners, NUI 3D Preview options, VanCustom, door behavior, ped animations, phone parameters (radii / jitter), categories, etc.
- `version.json` consumed by the version check (`raw.githubusercontent.com/foltone/foltone_doc/main/foltone-blackmarket/version.json`)

### Fixed
- **NUI** : `RESOURCE_NAME` now resolved via `GetParentResourceName()` → all JS↔Lua callbacks keep working if the server owner renames the resource folder (otherwise the menu becomes inert and /restart is the only way to release the NUI focus)
- **NUI** : `state.customWeaponFilter` is reset on every open (avoids stale reference to a sold/removed weapon if `DefaultCategory = 'customs'`)
- **NUI** : `NUI.opening` guard against rapid double-opens (two `getCatalog` callbacks in flight)
- **Server** : `getCatalog` now sends a **merged** locale payload (en as base + active locale as override), so a missing key in a partial locale falls back to English instead of showing the raw key in the UI
- **Server** : hot reload (`ensure foltone_blackmarket` while players are online) re-broadcasts state to already-connected players
- **Server** : `BM_State.heat` is reset on every spawn (was persisting across van cycles)
- **Client** : 30s timeout + cleanup of orphan server callbacks on network drop, pcall around the callback to keep the queue healthy
- **Client** : log console once when `Config.Locale` points to a missing locale, listing what's available
- **RageUI** : `fmtMoney` now uses a thousands separator (`$1,234,567`) like the NUI
- **Bridge** : `Bridge.HasItem` (ESX/QB) more robust when the player object is missing
- **Version check** : moved to a JSON endpoint (`json.decode` native + regex fallback)

### Minor / security
- `playerDropped` captures `source` into a local (best practice)
- `applyCustomToOxInventory` : dropped an unused multi-value return

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
