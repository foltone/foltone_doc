---
title: "Installation"
description: "Installation guide for the foltone_gruppe6 script"
script: "foltone-gruppe6"
section: "Gruppe6"
order: 1
version: "1.0.0"
---

# Installing foltone_gruppe6

## Requirements

- **ESX Framework** (es_extended)
- **oxmysql** for database
- **RageUI** (included or install separately)

## Installation Steps

### 1. Download the script

Place the `foltone_gruppe6` folder in your `resources/` directory.

### 2. Import the database

Run the provided SQL file in your database:

```sql
-- Import the SQL file included with the script
-- It contains the tables needed for the job and robbery systems
```

### 3. Add the job to the database

Make sure the `gruppe6` job exists in your `jobs` table with the configured grades.

### 4. Configure server.cfg

Add the following line to your `server.cfg`:

```cfg
ensure foltone_gruppe6
```

### 5. Start order

The script must start **after** the following resources:

```cfg
ensure es_extended
ensure oxmysql
ensure foltone_gruppe6
```

## Verification

1. Restart your server
2. Connect and assign yourself the `gruppe6` job
3. Go to the service point to verify the RageUI menu opens correctly
4. Check server logs for any errors
