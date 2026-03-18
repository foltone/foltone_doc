---
title: "Changelog"
description: "Changelog for Foltone CCTV"
script: "foltone-cctv"
section: "Foltone CCTV"
order: 99
version: "1.0.0"
---

# Changelog — foltone_cctv

## 1.0.0 — 2026-03-18

- Initial release
- 5 camera types: Standard, Dome, Bullet, Mini Bullet, PTZ Pro
- Camera shop with card grid UI, per-type pricing and SVG images
- Wall-snapping placement system using surface normals
- Camera view with mouse rotation, scroll zoom, keyboard shortcuts
- CCTV visual effects: timecycle filter, vignette, grain, scanlines, corner markers
- Configurable effect intensity via Config.CameraEffect
- Night vision toggle (N key)
- Screenshot capture via screenshot-basic
- Motion detection with configurable radius and cooldown
- Camera destruction by shooting/melee (configurable hits and weapons)
- Job group system: assign cameras to a job for shared access
- Individual sharing via player server ID
- Tablet item with holding animation and prop
- Monitoring station item with prop_cctv_unit_01
- Fixed computer terminals
- Sound effects for all camera actions
- Camera debug tool (/cctv_debug) for offset calibration
- Multi-framework support: ESX, QBCore, QBX
- Multi-language support: English, French
- Automatic database migration on startup
- State machine hardening: all UI states properly guarded
