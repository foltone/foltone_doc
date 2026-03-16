---
title: "Installation"
description: "Props Storage script installation guide"
script: "foltone-props-storage"
section: "Props Storage"
order: 1
version: "1.0.0"
---

# Installation — foltone_props_storage

## Requirements

- **ESX Legacy** (v1.12.3 or higher)
- **oxmysql** — MySQL library
- **ox_lib** *(optional)* — For input dialogs
- **ox_inventory** *(optional)* — Alternative inventory system
- **ox_target** *(optional)* — Required if using ox_inventory

## Download

Download the script from your Tebex account and place the folder in your `resources/` directory.

## Database

Import the SQL table into your database:

```sql
CREATE TABLE IF NOT EXISTS `props_inventory` (
  `id` INT PRIMARY KEY AUTO_INCREMENT,
  `owner` VARCHAR(255) NOT NULL,
  `inventory` JSON NOT NULL,
  `position` JSON NOT NULL,
  `prop` VARCHAR(100) NOT NULL,
  `pin` VARCHAR(10) NOT NULL,
  `bucket` INT DEFAULT NULL
);
```

## Server Configuration

Add to your `server.cfg`:

```ini
ensure ox_lib
ensure oxmysql
ensure es_extended
ensure foltone_props_storage
```

> **Important**: `foltone_props_storage` must start **after** `es_extended` and `oxmysql`.

## Adding Items

Add the safe items to your ESX database:

```sql
INSERT INTO `items` (`name`, `label`, `weight`, `rare`, `can_remove`) VALUES
  ('big_safe', 'Large Safe', 5, 0, 1),
  ('safe', 'Safe', 3, 0, 1);
```

If you're using **ox_inventory**, add items in `ox_inventory/data/items.lua`:

```lua
['big_safe'] = {
    label = 'Large Safe',
    weight = 5000,
    stack = false,
},
['safe'] = {
    label = 'Safe',
    weight = 3000,
    stack = false,
},
```

## ox_lib (optional)

If you want to use ox_lib for input dialogs, uncomment the line in `fxmanifest.lua`:

```lua
shared_scripts {
    '@ox_lib/init.lua', -- uncomment this line
    "config.lua",
    "trad.lua",
    "locales/*.lua"
}
```

## Verification

After restarting your server:

1. Give yourself a safe item: `/giveitem [id] big_safe 1`
2. Use the item — the placement UI should appear
3. Place the safe and set a PIN code
4. Check the server console logs

## Discord Webhook

To enable Discord logging, edit `server/sv_editable.lua` and replace the webhook URL:

```lua
PerformHttpRequest("https://discord.com/api/webhooks/YOUR_WEBHOOK_HERE", ...)
```
