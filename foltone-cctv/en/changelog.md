---
title: "Changelog"
description: "Changelog for Foltone CCTV"
script: "foltone-cctv"
section: "Foltone CCTV"
order: 99
version: "1.1.0"
---

# Changelog — foltone_cctv

## 1.1.0 — 2026-03-22

### Additions
- Shop accessories: tablet and monitoring station available for purchase in the shop
- Monitoring station is now a placeable item (like cameras) that opens the camera UI when interacted with
- Capture lightbox: click on a capture to view it fullscreen with camera name and date
- `propPitch` and `propRoll` offset parameters for camera prop rotation correction
- `wallOffset` and `image` fields in camera type configuration
- `Config.ShopAccessories` section for tablet and station shop items

### Changes
- Camera types updated: 4 types (Standard, Bullet, Mini Bullet, Shop Cam) replacing previous 5 types
- Shop images now use PNG files from config `image` field instead of SVG
- Notification system refactored: `ClientNotification` in config.lua (client-side, customizable) + server triggers client event
- getCameras SQL optimized: replaced N+1 shared queries with single IN subquery
- install.sql updated with stations table, all columns, and database indexes
- Reduced purchase timeout between shop buys
- All UI strings translated to English

### Fixes
- Fixed requestCapture not validating camera ownership/access
- Fixed destroyCamera allowing remote abuse (added distance check)
- Fixed XSS vulnerability: replaced inline onclick handlers with data-attributes + event delegation
- Fixed motionCooldowns memory leak when cameras are deleted
- Fixed camera access entries not cleaned up when camera deleted
- Fixed ALTER TABLE migrations using async instead of await
- Fixed CAM_TYPE_ICONS mismatch (removed dome/ptz, added shop_cam)
- Fixed button icon+text misalignment across all UI buttons
- Fixed monitor shop purchase giving wrong item
- Fixed screenshot-basic HTTPS mixed content error
- Moved cctv_debug command behind admin permission check

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
