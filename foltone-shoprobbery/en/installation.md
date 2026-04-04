---
title: "Installation"
description: "Installation guide for the foltone_shoprobbery script"
script: "foltone-shoprobbery"
section: "Shop Robbery"
order: 1
version: "1.0.0"
---

# Installing foltone_shoprobbery

## Requirements

- **ESX Framework** (es_extended)
- **oxmysql** for database
- **RageUI** (included or install separately)

## Installation Steps

### 1. Download the script

Place the `foltone_shoprobbery` folder in your `resources/` directory.

### 2. Import the database

Run the provided SQL file to create the necessary tables (cooldowns, robbery logs).

### 3. Configure server.cfg

Add the following line to your `server.cfg`:

```cfg
ensure foltone_shoprobbery
```

### 4. Start order

```cfg
ensure es_extended
ensure oxmysql
ensure foltone_shoprobbery
```

### 5. Configure police notifications

Adapt the notification functions in the config to match your dispatch system (phone, MDT, etc.).

## Verification

1. Restart your server
2. Go to a convenience store
3. Verify the shop menu works (purchasing items)
4. Test the robbery with the required number of police on duty
5. Verify that police alerts are sent correctly
