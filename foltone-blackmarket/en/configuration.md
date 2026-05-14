---
title: "Configuration"
description: "Configuration guide for foltone_blackmarket script"
script: "foltone-blackmarket"
section: "Blackmarket"
order: 2
version: "1.0.0"
---

# Configuration

All configuration is done in `config.lua`. Options are organized from most to least frequently modified.

## Core settings

```lua
Config.Locale = 'en'                  -- 'fr' | 'en' | 'es'
Config.Debug  = true                  -- console logs

Config.FrameworkOverride = nil        -- 'esx' | 'qbcore' | 'qbox' | 'standalone' | nil (auto)
Config.InventoryOverride = nil        -- 'ox_inventory' | 'qs-inventory' | 'esx' | 'qb' | nil (auto)

Config.MenuType     = 'rageui'        -- 'rageui' (in-game) or 'nui' (HTML)
Config.TargetSystem = 'auto'          -- 'auto' | 'ox_target' | 'qb-target' | 'qtarget' | 'none'
Config.UseTextUI    = true            -- textUI fallback if TargetSystem='none'

Config.MoneyAccount  = 'cash'         -- money account used
Config.MoneyItemName = 'money'        -- ox_inventory money item

Config.PoliceJobs = { 'police', 'lspd', 'sasp', 'bcso' }
```

## RageUI menu appearance

```lua
Config.RageUI = {
    Theme = 'modern',                 -- 'classic' (GTA V) | 'modern' (dark)

    AccentColor = { R = 59, G = 130, B = 246, A = 200 },

    AnimationEnabled = true,
    AnimationSpeed   = 7,

    BannerDict    = 'shopui_title_gunvan',
    BannerTexture = 'shopui_title_gunvan',
}
```

Available banner presets : `shopui_title_gunvan` (Drug Wars DLC), `shopui_title_gunclub_shop`, `shopui_title_gunmod_shop`, `shopui_title_gunrunning` (always available). Detailed colors of the modern theme are tunable in `src/config.lua`.

## Van lifecycle

```lua
Config.FirstSpawnDelaySeconds = 5  * 60   -- first spawn after server start
Config.LifetimeSeconds        = 30 * 60   -- van duration
Config.RespawnCooldownSeconds = 45 * 60   -- pause before next spawn
Config.AvoidPreviousLocation  = true      -- avoid respawning at same place
```

## Map blip (permanent)

```lua
Config.ShowBlip           = false  -- not recommended in RP (use encrypted phone)
Config.RequireContactItem = false  -- blip only if player has bm_contact
Config.ContactItemName    = 'bm_contact'
Config.BlipSprite = 110
Config.BlipColor  = 1
Config.BlipScale  = 0.85
```

## Encrypted phone

```lua
Config.EncryptedPhone = {
    enable          = true,
    itemName        = 'bm_encrypted_phone',
    cooldownSeconds = 30,

    -- Phase 1 : flashing search blip
    searchBlipSprite   = 161,
    searchBlipColor    = 1,
    searchBlipScale    = 1.2,
    searchBlipFlash    = true,
    searchBlipDuration = 20,

    -- Phase 2 : precise van blip
    vanBlipSprite      = 110,
    vanBlipColor       = 5,
    vanBlipScale       = 0.95,
    vanBlipDuration    = 60,
}
```

When the player uses the item, a flashing blip 161 appears for 20 seconds, then the precise van location for 60 seconds.

## Police & heat

```lua
Config.CopFleeMode       = true     -- the dealer flees if police nearby
Config.CopFleeRadius     = 80.0
Config.PoliceAlertChance = 0.10     -- 10% chance of alert per purchase

Config.HeatSystem         = true    -- heat accumulates on the van
Config.HeatThreshold      = 8       -- forced despawn above this
Config.HeatDecayPerMinute = 1
```

## Economy

```lua
Config.StockVariance = 0.30   -- stock variation between vans (+/-30%)
Config.PriceVariance = 0.10   -- price variation between vans (+/-10%)

Config.MaxBuyDistance     = 5.0
Config.BuyCooldownSeconds = 3
```

## Interaction

```lua
Config.InteractDistance = 3.5

-- BoxZone for ox_target (the ped is attached to the van : no raycast)
Config.TargetZoneOffset = vector3(0.0, -2.6, 0.5)
Config.TargetZoneSize   = vector3(2.2, 2.2, 2.0)
```

## Spawn locations

```lua
Config.SpawnLocations = {
    { coords = vector3(1726.13, 3284.20, 41.22), heading = 200.0, label = 'Sandy Shores - Warehouse' },
    -- ... add as many as you like (~10 default presets are commented out)
}
```

## Items and weapons

Each item has a key, an invName (inventory name), a category, a price, a stock, etc.

```lua
Config.Items = {
    {
        key = 'weapon_pistol', category = 'weapons',
        invName = 'WEAPON_PISTOL', weaponHash = `WEAPON_PISTOL`, isWeapon = true,
        label = '9mm Pistol', description = 'Compact, reliable, traceable... maybe.',
        price = 4500, stock = 5, minRep = 0, heat = 1,
        stats = { damage = 35, range = 40, fireRate = 55, accuracy = 60 },
        scratched = true,        -- if true : 'SCRATCHED' serial in ox_inventory metadata
    },
    -- ...
}
```

### Item parameters

| Field | Type | Description |
|---|---|---|
| `key` | string | Unique key (for stock and price modifier) |
| `category` | string | `'weapons'` \| `'items'` \| `'protection'` \| `'customs'` |
| `invName` | string | Item name in the inventory |
| `isWeapon` | bool | `true` to use AddWeapon (1 unit only) |
| `weaponHash` | hash | Used for 3D preview (`prop_*` allowed for items) |
| `price` | number | Base price ($) |
| `stock` | number | Max quantity per van (modulated by StockVariance) |
| `minRep` | number | Minimum reputation required (0 = none) |
| `heat` | number | Heat points generated on purchase |
| `stats` | table | Stats shown in the menu (cosmetic) |
| `scratched` | bool | Sets `metadata.serial = 'SCRATCHED'` in ox_inventory |

## Weapon customs

```lua
Config.WeaponCustoms = {
    ['WEAPON_PISTOL'] = {
        weaponHash = `WEAPON_PISTOL`,
        label      = '9mm Pistol',
        components = {
            { key = 'p_supp', label = 'Suppressor', price = 800,
              component = `COMPONENT_AT_PI_SUPP_02`, metaName = 'at_pi_supp_02' },
            -- ...
        },
        tints = {
            { key = 't_norm', label = 'Standard', price = 0,    tint = 0 },
            { key = 't_gold', label = 'Gold',     price = 1200, tint = 2 },
            -- ...
        },
    },
}
```

Customs are only offered if the player **already owns** the weapon. The `metaName` corresponds to the entry in `metadata.components` of ox_inventory.

## Admin

```lua
Config.AdminAce    = 'foltone_blackmarket.admin'
Config.AdminGroups = { 'admin', 'superadmin', 'god', 'owner' }
```

## Discord webhook

```lua
Config.Webhook         = ''                          -- empty = disabled
Config.WebhookUsername = 'Foltone Blackmarket'
Config.WebhookColor    = 0x3b82f6
```

Every purchase (item + custom) sends an embed with the player, the item and the price.

## Sections rarely modified

The sections below the configuration are reserved for fine-tuning (van skin, ped, animations, voice, 3D preview, NUI theme). See the comments in the file.
