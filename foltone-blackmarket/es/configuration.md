---
title: "Configuracion"
description: "Guia de configuracion del script foltone_blackmarket"
script: "foltone-blackmarket"
section: "Blackmarket"
order: 2
version: "1.0.0"
---

# Configuracion

Toda la configuracion se hace en `config.lua`. Las opciones estan organizadas de mas a menos modificadas.

## Ajustes basicos

```lua
Config.Locale = 'en'                  -- 'fr' | 'en' | 'es'
Config.Debug  = true                  -- logs de consola

Config.FrameworkOverride = nil        -- 'esx' | 'qbcore' | 'qbox' | 'standalone' | nil (auto)
Config.InventoryOverride = nil        -- 'ox_inventory' | 'qs-inventory' | 'esx' | 'qb' | nil (auto)

Config.MenuType     = 'rageui'        -- 'rageui' (in-game) o 'nui' (HTML)
Config.TargetSystem = 'auto'          -- 'auto' | 'ox_target' | 'qb-target' | 'qtarget' | 'none'
Config.UseTextUI    = true            -- fallback textUI si TargetSystem='none'

Config.MoneyAccount  = 'cash'         -- cuenta de dinero usada
Config.MoneyItemName = 'money'        -- item de dinero para ox_inventory

Config.PoliceJobs = { 'police', 'lspd', 'sasp', 'bcso' }
```

## Apariencia del menu RageUI

```lua
Config.RageUI = {
    Theme = 'modern',                 -- 'classic' (GTA V) | 'modern' (oscuro)

    AccentColor = { R = 59, G = 130, B = 246, A = 200 },

    AnimationEnabled = true,
    AnimationSpeed   = 7,

    BannerDict    = 'shopui_title_gunvan',
    BannerTexture = 'shopui_title_gunvan',
}
```

Presets de banner disponibles : `shopui_title_gunvan` (DLC Drug Wars), `shopui_title_gunclub_shop`, `shopui_title_gunmod_shop`, `shopui_title_gunrunning` (siempre disponible). Los colores detallados del tema modern son ajustables en `src/config.lua`.

## Ciclo de vida del van

```lua
Config.FirstSpawnDelaySeconds = 5  * 60   -- 1er spawn tras inicio del servidor
Config.LifetimeSeconds        = 30 * 60   -- duracion de presencia del van
Config.RespawnCooldownSeconds = 45 * 60   -- pausa antes del nuevo spawn
Config.AvoidPreviousLocation  = true      -- evita respawn en mismo sitio
```

## Blip mapa (permanente)

```lua
Config.ShowBlip           = false  -- no recomendado en RP (usar telefono cifrado)
Config.RequireContactItem = false  -- blip solo si el jugador tiene bm_contact
Config.ContactItemName    = 'bm_contact'
Config.BlipSprite = 110
Config.BlipColor  = 1
Config.BlipScale  = 0.85
```

## Telefono cifrado

```lua
Config.EncryptedPhone = {
    enable          = true,
    itemName        = 'bm_encrypted_phone',
    cooldownSeconds = 30,

    -- Fase 1 : blip de busqueda parpadeante
    searchBlipSprite   = 161,
    searchBlipColor    = 1,
    searchBlipScale    = 1.2,
    searchBlipFlash    = true,
    searchBlipDuration = 20,

    -- Fase 2 : posicion precisa del van
    vanBlipSprite      = 110,
    vanBlipColor       = 5,
    vanBlipScale       = 0.95,
    vanBlipDuration    = 60,
}
```

Cuando el jugador usa el item, aparece un blip 161 parpadeante durante 20 segundos, luego la posicion precisa del van durante 60 segundos.

## Policia & heat

```lua
Config.CopFleeMode       = true     -- el vendedor huye si hay policia cerca
Config.CopFleeRadius     = 80.0
Config.PoliceAlertChance = 0.10     -- 10% de probabilidad de alerta por compra

Config.HeatSystem         = true    -- acumulacion de calor en el van
Config.HeatThreshold      = 8       -- despawn forzado por encima
Config.HeatDecayPerMinute = 1
```

## Economia

```lua
Config.StockVariance = 0.30   -- variacion de stock entre vans (+/-30%)
Config.PriceVariance = 0.10   -- variacion de precio entre vans (+/-10%)

Config.MaxBuyDistance     = 5.0
Config.BuyCooldownSeconds = 3
```

## Interaccion

```lua
Config.InteractDistance = 3.5

-- BoxZone para ox_target (el ped esta vinculado al van : sin raycast)
Config.TargetZoneOffset = vector3(0.0, -2.6, 0.5)
Config.TargetZoneSize   = vector3(2.2, 2.2, 2.0)
```

## Ubicaciones de spawn

```lua
Config.SpawnLocations = {
    { coords = vector3(1726.13, 3284.20, 41.22), heading = 200.0, label = 'Sandy Shores - Almacen' },
    -- ... anada las que quiera (~10 presets por defecto comentados)
}
```

## Items y armas

Cada item tiene una clave, un invName (nombre inventario), una categoria, un precio, un stock, etc.

```lua
Config.Items = {
    {
        key = 'weapon_pistol', category = 'weapons',
        invName = 'WEAPON_PISTOL', weaponHash = `WEAPON_PISTOL`, isWeapon = true,
        label = '9mm Pistol', description = 'Compact, reliable, traceable... maybe.',
        price = 4500, stock = 5, minRep = 0, heat = 1,
        stats = { damage = 35, range = 40, fireRate = 55, accuracy = 60 },
        scratched = true,        -- si true : numero de serie 'SCRATCHED' en la metadata de ox_inventory
    },
    -- ...
}
```

### Parametros de un item

| Campo | Tipo | Descripcion |
|---|---|---|
| `key` | string | Clave unica (usada para stock y price modifier) |
| `category` | string | `'weapons'` \| `'items'` \| `'protection'` \| `'customs'` |
| `invName` | string | Nombre del item en el inventario |
| `isWeapon` | bool | `true` para usar AddWeapon (solo 1 unidad) |
| `weaponHash` | hash | Usado para preview 3D (`prop_*` autorizado para items) |
| `price` | number | Precio base ($) |
| `stock` | number | Cantidad max por van (modulada por StockVariance) |
| `minRep` | number | Reputacion minima requerida (0 = ninguna) |
| `heat` | number | Puntos de calor generados al comprar |
| `stats` | table | Stats mostradas en el menu (cosmetica) |
| `scratched` | bool | Pone `metadata.serial = 'SCRATCHED'` en ox_inventory |

## Personalizacion de armas

```lua
Config.WeaponCustoms = {
    ['WEAPON_PISTOL'] = {
        weaponHash = `WEAPON_PISTOL`,
        label      = '9mm Pistol',
        components = {
            { key = 'p_supp', label = 'Silenciador', price = 800,
              component = `COMPONENT_AT_PI_SUPP_02`, metaName = 'at_pi_supp_02' },
            -- ...
        },
        tints = {
            { key = 't_norm', label = 'Standard', price = 0,    tint = 0 },
            { key = 't_gold', label = 'Oro',      price = 1200, tint = 2 },
            -- ...
        },
    },
}
```

Los customs solo se ofrecen si el jugador **ya posee** el arma. El `metaName` corresponde a la entrada en `metadata.components` de ox_inventory.

## Admin

```lua
Config.AdminAce    = 'foltone_blackmarket.admin'
Config.AdminGroups = { 'admin', 'superadmin', 'god', 'owner' }
```

## Webhook de Discord

```lua
Config.Webhook         = ''                          -- vacio = desactivado
Config.WebhookUsername = 'Foltone Blackmarket'
Config.WebhookColor    = 0x3b82f6
```

Cada compra (item + custom) envia un embed con el jugador, el item y el precio.

## Secciones raramente modificadas

Las secciones al final del archivo de configuracion estan reservadas para los ajustes finos (skin del van, ped, animaciones, voz, preview 3D, tema NUI). Vea los comentarios en el archivo.
