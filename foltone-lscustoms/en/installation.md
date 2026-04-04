---
title: "Installation"
description: "Installation guide for the foltone_lscustoms script"
script: "foltone-lscustoms"
section: "LS Customs"
order: 1
version: "1.0.0"
---

# Installing foltone_lscustoms

## Requirements

- **ESX Framework** (es_extended)
- **oxmysql** for database
- **RageUI** (included or install separately)

## Installation Steps

### 1. Download the script

Place the `foltone_lscustoms` folder in your `resources/` directory.

### 2. Import the database

Run the provided SQL file to create the necessary tables (invoices, modification logs, etc.).

### 3. Configure server.cfg

Add the following line to your `server.cfg`:

```cfg
ensure foltone_lscustoms
```

### 4. Start order

```cfg
ensure es_extended
ensure oxmysql
ensure foltone_lscustoms
```

### 5. Disable default mechanic scripts

If you use another mechanic script (job version), make sure there are no conflicts. This script is **standalone** and does not require any job.

## Verification

1. Restart your server
2. Go to an LS Customs point on the map
3. Enter the zone with a vehicle
4. Verify the RageUI menu opens and the live preview works
5. Test an NPC towing mission
