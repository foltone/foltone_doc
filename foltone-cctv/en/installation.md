---
title: "Installation"
description: "Installation guide for Foltone CCTV"
script: "foltone-cctv"
section: "Foltone CCTV"
order: 1
version: "1.0.0"
---

# Installation — foltone_cctv

## Requirements

- **ESX Legacy**, **QBCore**, or **QBX** — FiveM framework
- **oxmysql** — MySQL library

### Optional dependencies

| Dependency | Purpose | Required for |
|-----------|---------|-------------|
| `ox_target` | 3D target interaction | If `Config.InteractionType = "ox_target"` |
| `screenshot-basic` | Camera screenshot capture | Capture feature in camera view |

## Download

Download the script from your Tebex account and place the `foltone_cctv` folder in your `resources/` directory.

## Server configuration

Add to your `server.cfg`:

```ini
set screenshot_basic_allow_fs_write "true"

ensure oxmysql
ensure es_extended      # or qb-core / qbx_core
ensure screenshot-basic # optional, for captures
ensure foltone_cctv
```

> **Important**: `foltone_cctv` must start **after** your framework and `oxmysql`. The `screenshot_basic_allow_fs_write` convar is required for the capture feature to work.

## Framework

The script supports 3 frameworks:

| Framework | Config value | Dependencies |
|-----------|-------------|-------------|
| ESX Legacy | `"esx"` | `es_extended`, `oxmysql` |
| QBCore | `"qbcore"` | `qb-core`, `oxmysql` |
| QBX | `"qbx"` | `qbx_core`, `oxmysql` |

Set the framework in `config.lua`:

```lua
Config.Framework = "esx" -- "esx", "qbcore" or "qbx"
```

## Database

### Fresh installation

Execute the `sql/install.sql` file in your MySQL database:

```bash
mysql -u root -p your_database < sql/install.sql
```

You can also copy the file contents and run it in phpMyAdmin or HeidiSQL.

> The script automatically adds missing columns (`camera_type`, `job_group`) on first startup. No manual migration needed.

## Inventory items

You need to register the following items in your inventory system (ox_inventory, qb-inventory, etc.):

| Item name | Purpose |
|-----------|---------|
| `cctv_tablet` | Surveillance tablet — opens the camera panel |
| `cctv_station` | Monitoring station — opens the camera panel |
| `cctv_cam_standard` | Standard camera — wall-mounted CCTV |
| `cctv_cam_dome` | Dome camera — 360 wide-angle |
| `cctv_cam_bullet` | Bullet camera — long-range zoom |
| `cctv_cam_mini` | Mini Bullet camera — compact and discreet |
| `cctv_cam_ptz` | PTZ Pro camera — pan-tilt-zoom professional |

> Each camera type has its own item. Using the item starts the placement mode for that specific camera type.

## Verification

After restarting the server:

1. Connect to the server with a character
2. Go to the shop PED position configured in `Config.ShopPositions`
3. Interact with the vendor to open the shop
4. Buy a camera, then use the item to enter placement mode
5. Place the camera on a wall, name it, then use the tablet to view it
