---
title: "Installation"
description: "Installation guide for foltone_charactercreator script"
script: "foltone-charactercreator"
section: "Character Creator"
order: 1
version: "1.0.0"
---

# Installation

## Requirements

- **ESX Framework** (es_extended)
- **skinchanger** (appearance management)
- **RageUI** (menu interface)

## Installation steps

### 1. Download the script

Place the `foltone_charactercreator` folder in your `resources/[foltone]/` directory.

### 2. Add to server.cfg

```cfg
ensure foltone_charactercreator
```

Make sure dependencies are started first:

```cfg
ensure es_extended
ensure skinchanger
ensure RageUI
```

### 3. Configure the script

Edit the `config.lua` file to match your needs (see Configuration section).

### 4. Restart the server

Restart your server or run `refresh` then `ensure foltone_charactercreator` in the console.

## File structure

```
foltone_charactercreator/
├── client/
├── server/
├── config.lua
└── fxmanifest.lua
```

## Compatibility

This script replaces the default ESX character creator. Make sure to disable any other character creation script to avoid conflicts.

## Common issues

| Issue | Solution |
|---|---|
| Menu doesn't show | Make sure RageUI is started |
| Appearance not saved | Verify skinchanger is working |
| Conflict with another script | Disable other character creators |
