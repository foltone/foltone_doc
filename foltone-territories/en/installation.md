---
title: "Installation"
description: "Installation guide for the foltone_territories script"
script: "foltone-territories"
section: "Territories"
order: 1
version: "1.0.0"
---

# Installing foltone_territories

## Requirements

- **ESX Framework** (es_extended)
- **oxmysql** for database
- **RageUI** (included or install separately)

## Installation Steps

### 1. Download the script

Place the `foltone_territories` folder in your `resources/` directory.

### 2. Import the database

Run the provided SQL file to create the necessary tables (territories, capture progress, history).

### 3. Configure server.cfg

Add the following line to your `server.cfg`:

```cfg
ensure foltone_territories
```

### 4. Start order

```cfg
ensure es_extended
ensure oxmysql
ensure foltone_territories
```

### 5. Configure gangs

Make sure the gang jobs exist in your `jobs` table and match those configured in the script.

## Verification

1. Restart your server
2. Assign yourself a configured gang job
3. Go to a territory zone
4. Verify the zone displays correctly on the map
5. Test selling drugs to an NPC in the zone
6. Verify that capture points increment
