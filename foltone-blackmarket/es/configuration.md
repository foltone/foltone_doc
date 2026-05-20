---
title: "Configuracion"
description: "Guia de configuracion del script foltone_blackmarket"
script: "foltone-blackmarket"
section: "Blackmarket"
order: 2
version: "1.1.1"
---

# Configuracion

Toda la configuracion se hace en `config.lua`. Las opciones estan organizadas de mas a menos modificadas. Esta pagina documenta **todas** las opciones disponibles para que no tengas que escarbar en el archivo.

## Ajustes basicos

```lua
Config.Locale = 'en'                  -- 'fr' | 'en' | 'es' | 'de'
Config.Debug  = true                  -- logs de consola
```

| Opcion | Tipo | Descripcion |
|---|---|---|
| `Config.Locale` | string | Codigo de idioma. Debe coincidir con un archivo `locales/<code>.lua`. Si el idioma no existe, fallback automatico a `en` con una advertencia en consola. |
| `Config.Debug` | bool | Activa logs detallados (util para ciblage / animacion / phone). |

### Framework e inventario

```lua
Config.FrameworkOverride = nil        -- 'esx' | 'qbcore' | 'qbox' | 'standalone' | nil (auto)
Config.InventoryOverride = nil        -- 'ox_inventory' | 'qs-inventory' | 'esx' | 'qb' | nil (auto)
```

| Valor | Efecto |
|---|---|
| `nil` | Deteccion automatica del framework / inventario activo. |
| `'esx'` | Fuerza ESX (`es_extended`). |
| `'qbcore'` | Fuerza QBCore (`qb-core`). |
| `'qbox'` | Fuerza QBox (`qbx_core`). |
| `'standalone'` | Sin framework. Bridge minimo (notificaciones via `lib.notify`). |

### Menu e interaccion

```lua
Config.MenuType     = 'nui'           -- 'rageui' (in-game) | 'nui' (HTML)
Config.TargetSystem = 'auto'          -- 'auto' | 'ox_target' | 'qb-target' | 'qtarget' | 'none'
Config.UseTextUI    = true            -- fallback textUI si TargetSystem='none'
Config.UseOxTarget  = true            -- legacy : false fuerza el fallback textUI
```

#### Tipos de menu (`Config.MenuType`)

| Valor | Descripcion |
|---|---|
| `'nui'` | Menu HTML/CSS pantalla completa, sidebar izquierda + preview 3D del arma en el maletero del van. Camara scripted, drag de raton para rotar, rueda para zoom. |
| `'rageui'` | Menu in-game estilo GTA V usando la libreria integrada `src/*`. Ver la seccion **Apariencia del menu RageUI** abajo para los temas. |

#### Sistemas de target (`Config.TargetSystem`)

| Valor | Descripcion |
|---|---|
| `'auto'` | Deteccion automatica en este orden : ox_target → qb-target → qtarget → fallback textUI. |
| `'ox_target'` | BoxZone alrededor del vendedor (el ped esta vinculado al van, raycast directo puede fallar). |
| `'qb-target'` | AddTargetEntity sobre el ped. |
| `'qtarget'` | AddTargetEntity sobre el ped. |
| `'none'` | Sin target ; muestra un textUI `[E] Hablar con el vendedor` cuando el jugador esta a `Config.InteractDistance`. |

### Dinero y trabajos

```lua
Config.MoneyAccount  = 'cash'         -- cuenta de dinero usada (ESX/QBCore)
Config.MoneyItemName = 'money'        -- nombre item para ox_inventory standalone

Config.PoliceJobs = { 'police', 'lspd', 'sasp', 'bcso' }
```

| Opcion | Descripcion |
|---|---|
| `Config.MoneyAccount` | Cuenta ESX (`money`, `bank`, `black_money`...) o QBCore (`cash`, `bank`...). |
| `Config.MoneyItemName` | Nombre del item usado para retiradas via `ox_inventory` en modo standalone. |
| `Config.PoliceJobs` | Lista de `job.name` considerados como policia (el vendedor huye si se acercan, si `Config.CopFleeMode = true`). |

## Apariencia del menu RageUI

Estas opciones solo se aplican si `Config.MenuType = 'rageui'`. Para el modo NUI, ver **Apariencia del menu NUI** mas abajo.

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

### Temas disponibles

| Tema | Estilo visual | Usalo si... |
|---|---|---|
| `'classic'` | Estilo GTA V original : degradado azul/blanco, sprites animados, fondo dinamico, subtitulo negro mayusculas. | Quieres la apariencia GTA estandar, coherente con los menus nativos. |
| `'modern'` | Estilo oscuro moderno : rectangulos planos, barra de acento coloreada en el item activo, fondo solido, animacion de relleno progresiva. | Quieres un look UI moderno con tu color de marca. |

> El tema por defecto es `'classic'`. Para cambiarlo, modifica `Config.RageUI.Theme`. El tema se carga al iniciar el resource.

### Opciones comunes

| Opcion | Se aplica a | Descripcion |
|---|---|---|
| `AccentColor` | `modern` | Color RGBA de la barra lateral en el item seleccionado. |
| `AnimationEnabled` | `modern` | Activa/desactiva la animacion de relleno del item activo. |
| `AnimationSpeed` | `modern` | Velocidad de animacion (1-15, mayor = mas rapido). |
| `BannerDict` / `BannerTexture` | ambos | Banner grafico arriba del menu. |

### Banners disponibles

Presets recomendados (siempre disponibles, no requieren DLC) :

| Dict | Texture | Apariencia |
|---|---|---|
| `shopui_title_gunclub_shop` | `shopui_title_gunclub_shop` | Banner Ammu-Nation clasico. |
| `shopui_title_gunmod_shop` | `shopui_title_gunmod_shop` | Banner taller de armas. |
| `shopui_title_gunrunning` | `shopui_title_gunrunning` | Banner DLC Gunrunning (siempre disponible). |
| `shopui_title_gunvan` | `shopui_title_gunvan` | Banner Gun Van (Drug Wars DLC, fallback automatico si ausente). |

### Colores avanzados del tema modern

Los colores detallados (texto, subtitulo, descripcion, slider, navigation, etc.) son ajustables en `src/config.lua` :

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

## Apariencia del menu NUI

Se aplica si `Config.MenuType = 'nui'`. El menu usa variables CSS modificables en caliente.

```lua
Config.Theme = {
    ['--bg-base']      = '#0b0f1a',   -- fondo principal
    ['--bg-panel']     = '#0e1322',   -- fondo panel sidebar
    ['--bg-card']      = '#121829',   -- fondo carta item
    ['--bg-hover']     = '#161d32',   -- fondo item con hover
    ['--accent']       = '#3b82f6',   -- color de acento (boton comprar)
    ['--accent-light'] = '#60a5fa',   -- acento claro (hover)
    ['--text-primary'] = '#e2e8f0',   -- texto principal
    ['--text-muted']   = '#d3d3d3',   -- texto secundario
    ['--red']          = '#f87171',   -- color error / out of stock
    ['--green']        = '#4ade80',   -- color exito
}
```

### Preview 3D del arma (solo NUI)

```lua
Config.PreviewCamOffset     = vector3(0.75, -2.60, 0.80)   -- posicion camara (offset local del van)
Config.PreviewCamLookOffset = vector3(-0.05, -1.10, 0.50)  -- punto mirado (offset local del van)
Config.PreviewCamFov        = 32.0                          -- FOV inicial
Config.PreviewZoomStep      = 2.0                           -- paso de zoom (rueda)
Config.PreviewMinFov        = 12.0                          -- zoom max
Config.PreviewMaxFov        = 55.0                          -- zoom min
Config.PreviewSensitivity   = 0.6                           -- sensibilidad drag raton
Config.PreviewAutoSpin      = true                          -- auto-rotacion tras 1.8s inactivo
Config.PreviewAutoSpinSpeed = 20.0                          -- velocidad auto-rotacion
Config.PreviewWeaponLight   = true                          -- luz azul + blanca en el arma

Config.WeaponDisplayOffset   = vector3(0.0, -1.10, 0.55)    -- posicion arma (offset local del van)
Config.WeaponDisplayRotation = vector3(0.0, 0.0, 0.0)       -- rotacion inicial arma
```

## Ciclo de vida del van

```lua
Config.FirstSpawnDelaySeconds = 5  * 60   -- 1er spawn tras inicio del servidor
Config.LifetimeSeconds        = 30 * 60   -- duracion del van
Config.RespawnCooldownSeconds = 45 * 60   -- pausa antes del nuevo spawn
Config.AvoidPreviousLocation  = true      -- evita respawn en mismo sitio
```

Ciclo automatico : `spawn` → espera `LifetimeSeconds` o stock total agotado → `despawn` → espera `RespawnCooldownSeconds` → `spawn` en la siguiente ubicacion.

## Blip mapa (permanente)

```lua
Config.ShowBlip           = false  -- no recomendado en RP (usar telefono cifrado)
Config.RequireContactItem = false  -- blip solo si jugador tiene bm_contact
Config.ContactItemName    = 'bm_contact'

Config.BlipSprite = 110
Config.BlipColor  = 1
Config.BlipScale  = 0.85
Config.BlipName   = nil            -- nil = usa la traduccion _U('blip_name')
```

## Telefono cifrado

```lua
Config.EncryptedPhone = {
    enable          = true,
    itemName        = 'bm_encrypted_phone',
    cooldownSeconds = 30,

    callAnimDurationMs = 4500,   -- duracion de la animacion "haciendo una llamada" cliente

    -- Fase 1 : blip de busqueda parpadeante
    searchBlipSprite      = 161,
    searchBlipColor       = 1,
    searchBlipScale       = 1.2,
    searchBlipFlash       = true,
    searchBlipDuration    = 20,    -- segundos
    searchBlipStartRadius = 300.0, -- radio inicial alrededor de la posicion real
    searchBlipEndRadius   = 30.0,  -- radio final (se cierra progresivamente)
    searchBlipUpdateMs    = 1200,  -- frecuencia de actualizacion del blip
    searchBlipJitter      = 12.0,  -- temblor aleatorio (efecto busqueda)

    -- Fase 2 : posicion precisa del van
    vanBlipSprite   = 110,
    vanBlipColor    = 5,
    vanBlipScale    = 0.95,
    vanBlipDuration = 60,          -- segundos
}
```

Cuando el jugador usa el item, aparece un blip parpadeante durante `searchBlipDuration` segundos en una posicion aleatoria que progresivamente se acerca a la real, luego la posicion precisa del van durante `vanBlipDuration` segundos.

## Policia y heat

```lua
Config.CopFleeMode       = true     -- el vendedor huye si policia cerca
Config.CopFleeRadius     = 80.0     -- en metros
Config.PoliceAlertChance = 0.10     -- 10% probabilidad de alerta por compra

Config.HeatSystem         = true    -- acumulacion de heat en el van
Config.HeatThreshold      = 8       -- despawn forzado por encima
Config.HeatDecayPerMinute = 1
```

## Economia

```lua
Config.StockVariance = 0.30   -- variacion stock entre vans (+/-30%)
Config.PriceVariance = 0.10   -- variacion precio entre vans (+/-10%)

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
    { coords = vector3(-318.9387, -2214.3159, 8.3723), heading = 235.3325, label = 'Elysian Island' },
    { coords = vector3(849.5719, -2180.7517, 30.2998), heading =  37.0987, label = 'Cypress Flats' },
    -- ... anada las que quiera
}
```

El servidor elige aleatoriamente una ubicacion. Con `AvoidPreviousLocation = true`, evita repetir la anterior (si hay al menos 2 ubicaciones).

## Categorias de items

```lua
Config.Categories = {
    { key = 'weapons',    labelKey = 'ui_cat_weapons',    icon = 'crosshair' },
    { key = 'items',      labelKey = 'ui_cat_items',      icon = 'box' },
    { key = 'protection', labelKey = 'ui_cat_protection', icon = 'shield' },
    { key = 'customs',    labelKey = 'ui_cat_customs',    icon = 'wrench' },
}
Config.DefaultCategory = 'weapons'
```

| Campo | Descripcion |
|---|---|
| `key` | Clave de la categoria (referenciada por cada item via su campo `category`). |
| `labelKey` | Clave de traduccion (ver `locales/*.lua`). |
| `icon` | Icono SVG embebido. Valores soportados : `'crosshair'`, `'box'`, `'shield'`, `'wrench'`. |

Categoria especial `'customs'` : automatica, solo aparece si el jugador posee al menos un arma listada en `Config.WeaponCustoms`.

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
        scratched = true,
    },
    -- ...
}
```

### Parametros de un item

| Campo | Tipo | Descripcion |
|---|---|---|
| `key` | string | Clave unica (para stock y price modifier). |
| `category` | string | `'weapons'` \| `'items'` \| `'protection'` (la categoria `customs` se autogenera). |
| `invName` | string | Nombre del item en el inventario. |
| `isWeapon` | bool | `true` para usar AddWeapon (solo 1 unidad). |
| `weaponHash` | hash | Usado para preview 3D (`prop_*` autorizado para items no-arma). |
| `label` | string | Nombre mostrado en el menu. |
| `description` | string | Descripcion mostrada bajo el item. |
| `price` | number | Precio base ($), modulado por `PriceVariance`. |
| `stock` | number | Cantidad max por van, modulada por `StockVariance`. |
| `minRep` | number | Reputacion minima requerida (0 = ninguna). |
| `heat` | number | Puntos de heat generados al comprar. |
| `stats` | table | Stats mostradas en el menu (`damage`, `range`, `fireRate`, `accuracy`, 0-100). |
| `scratched` | bool | Pone `metadata.serial = 'SCRATCHED'` en ox_inventory. |

## Personalizacion de armas

```lua
Config.WeaponCustoms = {
    ['WEAPON_PISTOL'] = {
        weaponHash = `WEAPON_PISTOL`,
        label      = '9mm Pistol',
        components = {
            { key = 'p_supp', label = 'Silenciador', price = 800,
              component = `COMPONENT_AT_PI_SUPP_02`, metaName = 'at_suppressor_light' },
            -- ...
        },
        tints = {
            { key = 't_norm', label = 'Standard', price = 0,    tint = 0 },
            { key = 't_gold', label = 'Oro',      price = 1200, tint = 2 },
        },
    },
}
```

Los customs solo se ofrecen si el jugador **ya posee** el arma. El `metaName` corresponde a la entrada en `metadata.components` de ox_inventory.

## Modelo de van

```lua
Config.VanModel      = `burrito3`
Config.VanLockDoors  = true       -- puertas bloqueadas para todos
Config.VanInvincible = true

Config.VanCustom = {
    enable          = true,
    primaryColor    = 12,          -- color id GTA V
    secondaryColor  = 84,
    pearlescent     = 12,
    wheelColor      = 0,
    windowTint      = 1,           -- 0 a 4
    plateText       = 'BLK MKT',
    plateIndex      = 3,
    dirtLevel       = 4.0,
    wheelType       = 7,
    wheelMod        = 6,           -- -1 para ninguno
    livery          = -1,          -- -1 para ninguna
    neonEnable      = false,
    neonR = 59, neonG = 130, neonB = 246,
}

Config.VanProps = {
    { model = `ch_prop_ch_crate_full_01a`, offset = vector3(0.0, -0.50, -0.30), rot = vector3(0.0, 0.0, 0.0) },
    { model = `ch_prop_box_ammo01b`,       offset = vector3(0.30, -1.20, -0.30), rot = vector3(0.0, 0.0, 90.0) },
    { model = `prop_box_ammo07b`,          offset = vector3(0.30, -1.20, -0.10), rot = vector3(0.0, 0.0, 0.0) },
}
```

Los `VanProps` son props vinculados al van con un offset local (X=derecha, Y=adelante, Z=arriba). Dan el aspecto "mercancia en el maletero".

## Comportamiento de las puertas

```lua
Config.DoorIndices       = { 2, 3 }    -- indices de puertas a abrir/cerrar
Config.DoorOpenDistance  = 6.0         -- distancia de apertura (metros)
Config.DoorCloseDistance = 8.5         -- distancia de cierre
Config.DoorCheckInterval = 250         -- ms entre verificaciones
Config.DoorAnimStep      = 0.015       -- paso animacion (menor = mas fluido)
Config.DoorMaxAngle      = 1.0         -- angulo max apertura (1.0 = abierta de par en par)
```

## Vendedor (PED)

```lua
Config.PedModels        = { `IG_GunVanSeller` }   -- aleatorio si hay varios
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

Config.PedDoorOpenDelayMs = 550     -- delay entre saludo y apertura de puertas
Config.PedThankCooldownMs = 2500    -- cooldown anti-spam del gesto agradecimiento
```

## Admin

```lua
Config.AdminAce    = 'foltone_blackmarket.admin'
Config.AdminGroups = { 'admin', 'superadmin', 'god', 'owner' }
```

Los jugadores con el ace o uno de los grupos pueden usar comandos admin (`/bm_spawn`, `/bm_despawn`).

## Webhook de Discord

```lua
Config.Webhook         = ''                          -- vacio = desactivado
Config.WebhookUsername = 'Foltone Blackmarket'
Config.WebhookColor    = 0x3b82f6
```

Cada compra (item + custom) envia un embed con el jugador, el item y el precio.

## Hook de notificacion personalizado

```lua
Config.Notification = function(msg, kind)
    if lib and lib.notify then
        lib.notify({ description = msg, type = kind or 'inform' })
        return
    end
    -- fallback segun framework...
end
```

Puedes reemplazar esta funcion con tu propio sistema de notificacion (Okok, etc.).
