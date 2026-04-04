---
title: "Installation"
description: "Installation guide for foltone_drivingschool script"
script: "foltone-drivingschool"
section: "Driving School"
order: 1
version: "1.0.0"
---

# Installation

## Requirements

- **ESX Framework** (es_extended)
- **esx_license** (license system)

## Installation steps

### 1. Download the script

Place the `foltone_drivingschool` folder in your `resources/[foltone]/` directory.

### 2. Add license types

Make sure the following license types exist in esx_license:

- `drive` - Car license
- `drive_bike` - Motorcycle license
- `drive_truck` - Truck license

### 3. Add to server.cfg

```cfg
ensure foltone_drivingschool
```

Make sure dependencies are started first:

```cfg
ensure es_extended
ensure esx_license
```

### 4. Configure the script

Edit the `config.lua` file to customize exam questions, routes, and vehicles (see Configuration section).

### 5. Restart the server

Restart your server or run `refresh` then `ensure foltone_drivingschool` in the console.

## File structure

```
foltone_drivingschool/
├── client/
├── server/
├── html/          -- NUI interface for road code exam
│   ├── index.html
│   ├── style.css
│   └── script.js
├── config.lua
└── fxmanifest.lua
```

## Common issues

| Issue | Solution |
|---|---|
| NUI interface doesn't show | Check files in the html/ folder |
| License not granted | Verify esx_license is working |
| Exam vehicle doesn't spawn | Check vehicle models in config |
