---
title: "Changelog"
description: "Barbershop script version history"
script: "foltone-barbershop"
section: "Barbershop"
order: 4
version: "1.1.0"
---

# Changelog

## v1.1.0

NUI menu fixes, server hardening and update notifier.

### NUI Menu
- Renamed-resource compatibility: `GetParentResourceName()` is now used instead of a hardcoded name, so the resource folder can be renamed without breaking NUI callbacks
- Fixed menu becoming unusable on second open: internal state (keyboard focus, current page, DOM content) is now reset on every open
- Fixed the "ghost" highlighted cell that remained selected after closing the menu
- Selection highlight now follows the mouse cursor: no more offset between the hovered cell and the highlighted cell
- No more double highlight: only a single element can be marked active at a time
- No more unwanted scroll on mouse hover: automatic `scrollIntoView` is disabled for mouse navigation (still kept for keyboard navigation)

### Server hardening
- Server-side `chairId` validation: only chair IDs defined in `Config.Positions` are accepted, preventing a malicious client from reserving phantom chairs
- Payment now requires the player to actually be seated on a chair: any `pay` call without an active chair is rejected
- Added rate-limit on the `releaseChair` event (consistency with `takeChair` and `pay`)

### Configuration
- New `Config.AutoUpdateCheck` option (default: `true`) to enable or disable the automatic update check at server startup
- Removed `Config.Debug` (was never read by the script)

### Update notifier
- Automatic update notifier: the server compares the installed version with the latest published version and prints a console message when an update is available

## v1.0.0

Initial release.

- NUI-based barbershop menu with glass/solid style options
- Multi-framework support: ESX Legacy, QBCore, QBX
- Appearance resource integration: illenium-appearance, fivem-appearance, qb-clothing
- 5 customization categories: Hair, Beard, Eyebrows, Eyes, Makeup
- Style grid with color picker and opacity slider
- Full keyboard navigation (arrow keys, Enter, Escape)
- Head rotation controls (A/Q/D keys) for previewing changes
- Real-time preview of all appearance changes
- 7 preconfigured barbershop locations with map blips
- NPC barber with scissors animation
- Configurable interaction methods (ox_target, qb-target, qtarget, interact, drawtext, marker)
- Configurable pricing, UI colors, menu position, and menu style
- Multi-language support (English and French)
