---
title: "Configuration"
description: "Configuration guide for foltone_blackmarket script"
script: "foltone-blackmarket"
section: "Blackmarket"
order: 2
version: "1.1.1"
---

# Configuration

All configuration is done in `config.lua`. Options are organized from most to least frequently modified. This page documents **every** available option so you don't have to dig through the file.

## Core settings

```lua
Config.Locale = 'en'                  -- 'fr' | 'en' | 'es' | 'de'
Config.Debug  = true                  -- console logs
```

| Option | Type | Description |
|---|---|---|
| `Config.Locale` | string | Language code. Must match a `locales/<code>.lua` file. If the language is missing, automatic fallback to `en` with a console warning. |
| `Config.Debug` | bool | Enables verbose logs (useful for targeting / animation / phone debugging). |

### Framework & inventory

```lua
Config.FrameworkOverride = nil        -- 'esx' | 'qbcore' | 'qbox' | 'standalone' | nil (auto)
Config.InventoryOverride = nil        -- 'ox_inventory' | 'qs-inventory' | 'esx' | 'qb' | nil (auto)
```

| Value | Effect |
|---|---|
| `nil` | Automatic detection of the active framework / inventory. |
| `'esx'` | Force ESX (`es_extended`). |
| `'qbcore'` | Force QBCore (`qb-core`). |
| `'qbox'` | Force QBox (`qbx_core`). |
| `'standalone'` | No framework. Minimal bridge (notifications via `lib.notify`). |

### Menu & interaction

```lua
Config.MenuType     = 'nui'           -- 'rageui' (in-game) | 'nui' (HTML)
Config.TargetSystem = 'auto'          -- 'auto' | 'ox_target' | 'qb-target' | 'qtarget' | 'none'
Config.UseTextUI    = true            -- textUI fallback when TargetSystem='none'
Config.UseOxTarget  = true            -- legacy : false forces textUI fallback
```

#### Menu types (`Config.MenuType`)

| Value | Description |
|---|---|
| `'nui'` | Full-screen HTML/CSS menu, left sidebar + 3D preview of the weapon in the van trunk. Scripted camera, mouse drag to rotate the weapon, scroll wheel to zoom. |
| `'rageui'` | In-game GTA V-style menu using the embedded `src/*` library. See **RageUI menu appearance** below for themes. |

#### Target systems (`Config.TargetSystem`)

| Value | Description |
|---|---|
| `'auto'` | Automatic detection in this order : ox_target → qb-target → qtarget → textUI fallback. |
| `'ox_target'` | BoxZone around the dealer (the ped is attached to the van, direct raycast on the ped may fail). |
| `'qb-target'` | AddTargetEntity on the ped. |
| `'qtarget'` | AddTargetEntity on the ped. |
| `'none'` | No target ; shows a textUI `[E] Talk to the dealer` when the player is within `Config.InteractDistance`. |

### Money & jobs

```lua
Config.MoneyAccount  = 'cash'         -- money account used (ESX/QBCore)
Config.MoneyItemName = 'money'        -- item name for ox_inventory standalone

Config.PoliceJobs = { 'police', 'lspd', 'sasp', 'bcso' }
```

| Option | Description |
|---|---|
| `Config.MoneyAccount` | ESX account (`money`, `bank`, `black_money`...) or QBCore (`cash`, `bank`...). |
| `Config.MoneyItemName` | Item name used for withdrawals via `ox_inventory` in standalone mode. |
| `Config.PoliceJobs` | List of `job.name` values considered as police (the dealer flees when they approach if `Config.CopFleeMode = true`). |

## RageUI menu appearance

These options only apply when `Config.MenuType = 'rageui'`. For NUI mode, see **NUI menu appearance** below.

```lua
Config.RageUI = {
    Theme = 'classic',                -- 'classic' | 'modern'

    AccentColor = { R = 59, G = 130, B = 246, A = 200 },

    AnimationEnabled = true,
    AnimationSpeed   = 7,

    BannerDict    = 'shopui_title_gunvan',
    BannerTexture = 'shopui_title_gunvan',
}
```

### Available themes

| Theme | Visual style | Use it when... |
|---|---|---|
| `'classic'` | Original GTA V style : blue/white gradient, animated sprites, dynamic background, black uppercase subtitle. | You want the standard GTA look, consistent with native menus. |
| `'modern'` | Dark modern style : flat rectangles, colored accent bar on the active item, solid background, progressive fill animation. | You want a modern UI look with your brand color. |

> The default theme is `'classic'`. To change it, edit `Config.RageUI.Theme`. The theme is loaded at resource startup.

### Common options

| Option | Applies to | Description |
|---|---|---|
| `AccentColor` | `modern` | RGBA color of the side bar on the selected item. |
| `AnimationEnabled` | `modern` | Enable/disable the fill animation of the active item. |
| `AnimationSpeed` | `modern` | Animation speed (1-15, higher = faster). |
| `BannerDict` / `BannerTexture` | both | Top-of-menu banner sprite. |

### Available banners

Recommended presets (always available, no DLC required) :

| Dict | Texture | Look |
|---|---|---|
| `shopui_title_gunclub_shop` | `shopui_title_gunclub_shop` | Classic Ammu-Nation banner. |
| `shopui_title_gunmod_shop` | `shopui_title_gunmod_shop` | Gun mod shop banner. |
| `shopui_title_gunrunning` | `shopui_title_gunrunning` | Gunrunning DLC banner (always available). |
| `shopui_title_gunvan` | `shopui_title_gunvan` | Gun Van banner (Drug Wars DLC, automatic fallback if missing). |

### Advanced colors for the modern theme

Detailed colors (text, subtitle, description, slider, navigation, etc.) are tunable in `src/config.lua` :

```lua
RageUIConfig.RageUI = {
    AccentWidth          = 3,
    ItemGap              = 2,
    ItemBackgroundColor  = { R = 28, G = 32, B = 40, A = 220 },
    MenuBackgroundColor  = { R = 16, G = 20, B = 26, A = 230 },
    TextActiveColor      = { R = 255, G = 255, B = 255, A = 255 },
    TextInactiveColor    = { R = 215, G = 220, B = 228, A = 240 },
    TextDisabledColor    = { R = 135, G = 140, B = 148, A = 200 },
    SubtitleTextColor    = { R = 255, G = 255, B = 255, A = 255 },
    SubtitleBgColor      = { R = 14, G = 18, B = 24, A = 230 },
    DescriptionTextColor = { R = 225, G = 230, B = 240, A = 240 },
    DescriptionBgColor   = { R = 14, G = 18, B = 24, A = 220 },
    MouseHoverColor      = { R = 255, G = 255, B = 255, A = 15 },
    SliderBgColor        = { R = 20, G = 24, B = 32, A = 140 },
    SliderFillColor      = { R = 28, G = 218, B = 236, A = 180 },
    SliderDividerColor   = { R = 80, G = 84, B = 92, A = 140 },
    NavigationBgColor    = { R = 20, G = 24, B = 28, A = 180 },
    NavigationHoverColor = { R = 40, G = 44, B = 52, A = 140 },
}
```

## NUI menu appearance

Applies when `Config.MenuType = 'nui'`. The menu uses CSS variables you can override at runtime.

```lua
Config.Theme = {
    ['--bg-base']      = '#0b0f1a',   -- main background
    ['--bg-panel']     = '#0e1322',   -- sidebar panel background
    ['--bg-card']      = '#121829',   -- item card background
    ['--bg-hover']     = '#161d32',   -- hovered item background
    ['--accent']       = '#3b82f6',   -- accent color (buy button)
    ['--accent-light'] = '#60a5fa',   -- light accent (hover)
    ['--text-primary'] = '#e2e8f0',   -- primary text
    ['--text-muted']   = '#d3d3d3',   -- secondary text
    ['--red']          = '#f87171',   -- error / out of stock color
    ['--green']        = '#4ade80',   -- success color
}
```

### 3D weapon preview (NUI only)

```lua
Config.PreviewCamOffset     = vector3(0.75, -2.60, 0.80)   -- camera position (van-local offset)
Config.PreviewCamLookOffset = vector3(-0.05, -1.10, 0.50)  -- look-at point (van-local offset)
Config.PreviewCamFov        = 32.0                          -- initial FOV
Config.PreviewZoomStep      = 2.0                           -- zoom step (mouse wheel)
Config.PreviewMinFov        = 12.0                          -- max zoom
Config.PreviewMaxFov        = 55.0                          -- min zoom
Config.PreviewSensitivity   = 0.6                           -- mouse drag sensitivity
Config.PreviewAutoSpin      = true                          -- auto rotate after 1.8s idle
Config.PreviewAutoSpinSpeed = 20.0                          -- auto rotation speed
Config.PreviewWeaponLight   = true                          -- blue + white glow on the weapon

Config.WeaponDisplayOffset   = vector3(0.0, -1.10, 0.55)    -- weapon position (van-local offset)
Config.WeaponDisplayRotation = vector3(0.0, 0.0, 0.0)       -- initial weapon rotation
```

## Van lifecycle

```lua
Config.FirstSpawnDelaySeconds = 5  * 60   -- first spawn after server start
Config.LifetimeSeconds        = 30 * 60   -- van duration
Config.RespawnCooldownSeconds = 45 * 60   -- pause before next spawn
Config.AvoidPreviousLocation  = true      -- avoid respawning at same place
```

Automatic cycle : `spawn` → wait `LifetimeSeconds` or all stock depleted → `despawn` → wait `RespawnCooldownSeconds` → `spawn` at the next location.

## Map blip (permanent)

```lua
Config.ShowBlip           = false  -- not recommended in RP (use the encrypted phone)
Config.RequireContactItem = false  -- blip only if player has bm_contact
Config.ContactItemName    = 'bm_contact'

Config.BlipSprite = 110
Config.BlipColor  = 1
Config.BlipScale  = 0.85
Config.BlipName   = nil            -- nil = use the _U('blip_name') translation
```

## Encrypted phone

```lua
Config.EncryptedPhone = {
    enable          = true,
    itemName        = 'bm_encrypted_phone',
    cooldownSeconds = 30,

    callAnimDurationMs = 4500,   -- duration of the "making a call" animation client-side

    -- Phase 1 : flashing search blip
    searchBlipSprite      = 161,
    searchBlipColor       = 1,
    searchBlipScale       = 1.2,
    searchBlipFlash       = true,
    searchBlipDuration    = 20,    -- seconds
    searchBlipStartRadius = 300.0, -- initial radius around true position
    searchBlipEndRadius   = 30.0,  -- final radius (closes in over time)
    searchBlipUpdateMs    = 1200,  -- blip update frequency
    searchBlipJitter      = 12.0,  -- random jitter (search effect)

    -- Phase 2 : precise van blip
    vanBlipSprite   = 110,
    vanBlipColor    = 5,
    vanBlipScale    = 0.95,
    vanBlipDuration = 60,          -- seconds
}
```

When the player uses the item, a flashing blip appears for `searchBlipDuration` seconds at a random position that progressively closes in on the real one, then the precise van location for `vanBlipDuration` seconds.

## Police & heat

```lua
Config.CopFleeMode       = true     -- the dealer flees if police nearby
Config.CopFleeRadius     = 80.0     -- in meters
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
    { coords = vector3(-318.9387, -2214.3159, 8.3723), heading = 235.3325, label = 'Elysian Island' },
    { coords = vector3(849.5719, -2180.7517, 30.2998), heading =  37.0987, label = 'Cypress Flats' },
    -- ... add as many as you like
}
```

The server picks a random location. With `AvoidPreviousLocation = true`, it skips the previous one (if at least 2 locations).

## Item categories

```lua
Config.Categories = {
    { key = 'weapons',    labelKey = 'ui_cat_weapons',    icon = 'crosshair' },
    { key = 'items',      labelKey = 'ui_cat_items',      icon = 'box' },
    { key = 'protection', labelKey = 'ui_cat_protection', icon = 'shield' },
    { key = 'customs',    labelKey = 'ui_cat_customs',    icon = 'wrench' },
}
Config.DefaultCategory = 'weapons'
```

| Field | Description |
|---|---|
| `key` | Category key (referenced by each item via its `category` field). |
| `labelKey` | Translation key (see `locales/*.lua`). |
| `icon` | Embedded SVG icon. Supported values : `'crosshair'`, `'box'`, `'shield'`, `'wrench'`. |

Special category `'customs'` : automatic, only shows up when the player owns at least one weapon listed in `Config.WeaponCustoms`.

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
        scratched = true,
    },
    -- ...
}
```

### Item parameters

| Field | Type | Description |
|---|---|---|
| `key` | string | Unique key (for stock and price modifier). |
| `category` | string | `'weapons'` \| `'items'` \| `'protection'` (the `customs` category is auto-generated). |
| `invName` | string | Item name in the inventory. |
| `isWeapon` | bool | `true` to use AddWeapon (1 unit only). |
| `weaponHash` | hash | Used for 3D preview (`prop_*` allowed for non-weapon items). |
| `label` | string | Name shown in the menu. |
| `description` | string | Description shown under the item. |
| `price` | number | Base price ($), modified by `PriceVariance`. |
| `stock` | number | Max quantity per van, modulated by `StockVariance`. |
| `minRep` | number | Minimum reputation required (0 = none). |
| `heat` | number | Heat points generated on purchase. |
| `stats` | table | Stats shown in the menu (`damage`, `range`, `fireRate`, `accuracy`, 0-100). |
| `scratched` | bool | Sets `metadata.serial = 'SCRATCHED'` in ox_inventory. |

## Weapon customs

```lua
Config.WeaponCustoms = {
    ['WEAPON_PISTOL'] = {
        weaponHash = `WEAPON_PISTOL`,
        label      = '9mm Pistol',
        components = {
            { key = 'p_supp', label = 'Suppressor', price = 800,
              component = `COMPONENT_AT_PI_SUPP_02`, metaName = 'at_suppressor_light' },
            -- ...
        },
        tints = {
            { key = 't_norm', label = 'Standard', price = 0,    tint = 0 },
            { key = 't_gold', label = 'Gold',     price = 1200, tint = 2 },
        },
    },
}
```

Customs are only offered if the player **already owns** the weapon. The `metaName` corresponds to the entry in `metadata.components` of ox_inventory.

## Van model

```lua
Config.VanModel      = `burrito3`
Config.VanLockDoors  = true       -- doors locked for everyone
Config.VanInvincible = true

Config.VanCustom = {
    enable          = true,
    primaryColor    = 12,          -- GTA V color id
    secondaryColor  = 84,
    pearlescent     = 12,
    wheelColor      = 0,
    windowTint      = 1,           -- 0 to 4
    plateText       = 'BLK MKT',
    plateIndex      = 3,
    dirtLevel       = 4.0,
    wheelType       = 7,
    wheelMod        = 6,           -- -1 for none
    livery          = -1,          -- -1 for none
    neonEnable      = false,
    neonR = 59, neonG = 130, neonB = 246,
}

Config.VanProps = {
    { model = `ch_prop_ch_crate_full_01a`, offset = vector3(0.0, -0.50, -0.30), rot = vector3(0.0, 0.0, 0.0) },
    { model = `ch_prop_box_ammo01b`,       offset = vector3(0.30, -1.20, -0.30), rot = vector3(0.0, 0.0, 90.0) },
    { model = `prop_box_ammo07b`,          offset = vector3(0.30, -1.20, -0.10), rot = vector3(0.0, 0.0, 0.0) },
}
```

`VanProps` are props attached to the van with a local offset (X=right, Y=forward, Z=up). They give the "merchandise in the trunk" look.

## Door behavior

```lua
Config.DoorIndices       = { 2, 3 }    -- door indices to open/close
Config.DoorOpenDistance  = 6.0         -- open distance (meters)
Config.DoorCloseDistance = 8.5         -- close distance
Config.DoorCheckInterval = 250         -- ms between checks
Config.DoorAnimStep      = 0.015       -- animation step (smaller = smoother)
Config.DoorMaxAngle      = 1.0         -- max opening angle (1.0 = wide open)
```

## Dealer (PED)

```lua
Config.PedModels        = { `IG_GunVanSeller` }   -- random pick if multiple
Config.PedInvincible    = true
Config.PedFleesOnAttack = false

Config.PedAttachOffset   = vector3(-0.65, -1.9, 0.15)
Config.PedAttachRotation = vector3(0.0, 0.0, -160.0)

Config.PedSitAnim = {
    dict = 'veh@van@rps_rear@base', name = 'sit', flag = 1,
}

Config.PedAnims = {
    hello  = { dict = 'gestures@m@standing@casual', name = 'gesture_hello',     duration = 2500 },
    bye    = { dict = 'gestures@m@standing@casual', name = 'gesture_bye_soft',  duration = 2500 },
    thanks = { dict = 'gestures@m@standing@casual', name = 'gesture_thank_you', duration = 2500 },
}

Config.PedSpeech = {
    hello = 'GENERIC_HI', bye = 'GENERIC_BYE', thanks = 'GENERIC_THANKS',
}

Config.PedDoorOpenDelayMs = 550     -- delay between greeting and doors opening
Config.PedThankCooldownMs = 2500    -- anti-spam cooldown for the thank-you gesture
```

## Admin

```lua
Config.AdminAce    = 'foltone_blackmarket.admin'
Config.AdminGroups = { 'admin', 'superadmin', 'god', 'owner' }
```

Players with the ace or one of the groups can use admin commands (`/bm_spawn`, `/bm_despawn`).

## Discord webhook

```lua
Config.Webhook         = ''                          -- empty = disabled
Config.WebhookUsername = 'Foltone Blackmarket'
Config.WebhookColor    = 0x3b82f6
```

Every purchase (item + custom) sends an embed with the player, the item and the price.

## Custom notification hook

```lua
Config.Notification = function(msg, kind)
    if lib and lib.notify then
        lib.notify({ description = msg, type = kind or 'inform' })
        return
    end
    -- framework fallback...
end
```

You can replace this function with your own notification system (Okok, etc.).
