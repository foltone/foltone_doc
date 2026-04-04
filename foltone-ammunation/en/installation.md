---
title: "Installation"
description: "Installation guide for foltone_ammunation script"
script: "foltone-ammunation"
section: "Ammunation"
order: 1
version: "1.0.0"
---

# Installation

## Requirements

- **ESX Framework** (es_extended)
- **oxmysql** (database)
- **esx_license** (license system)
- **RageUI** (menu interface)

## Installation steps

### 1. Download the script

Place the `foltone_ammunation` folder in your `resources/[foltone]/` directory.

### 2. Import the database

Run the provided SQL file in your database:

```sql
-- Import the sql/install.sql file into your database
```

### 3. Add to server.cfg

```cfg
ensure foltone_ammunation
```

Make sure dependencies are started **before** this script:

```cfg
ensure es_extended
ensure oxmysql
ensure esx_license
ensure RageUI
```

### 4. Configure the script

Edit the `config.lua` file to match your needs (see Configuration section).

### 5. Restart the server

Restart your server or run `refresh` then `ensure foltone_ammunation` in the console.

## File structure

```
foltone_ammunation/
├── client/
├── server/
├── config.lua
├── fxmanifest.lua
└── sql/
```

## Common issues

| Issue | Solution |
|---|---|
| Menu doesn't open | Make sure RageUI is started |
| License not detected | Verify esx_license is working |
| Robbery doesn't start | Check required police count |
