---
title: "Installation"
description: "Installation guide for foltone_baginventory script"
script: "foltone-baginventory"
section: "Bag Inventory"
order: 1
version: "1.0.0"
---

# Installation

## Requirements

- **ESX Framework** (es_extended)
- **oxmysql** (database)
- **RageUI** (menu interface)

## Installation steps

### 1. Download the script

Place the `foltone_baginventory` folder in your `resources/[foltone]/` directory.

### 2. Import the database

Run the provided SQL file:

```sql
-- Import the sql/install.sql file into your database
```

This creates the table needed to store the contents of bags placed on the ground.

### 3. Add to server.cfg

```cfg
ensure foltone_baginventory
```

Make sure dependencies are started first:

```cfg
ensure es_extended
ensure oxmysql
ensure RageUI
```

### 4. Add bag items

Add the bag items to your `items` database table:

```sql
INSERT INTO `items` (`name`, `label`, `weight`) VALUES
('bag_small', 'Small Bag', 2),
('bag_medium', 'Medium Bag', 3),
('bag_large', 'Large Bag', 5);
```

### 5. Configure and restart

Edit `config.lua` then restart the server.

## File structure

```
foltone_baginventory/
├── client/
├── server/
├── config.lua
├── fxmanifest.lua
└── sql/
```
