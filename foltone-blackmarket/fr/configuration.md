---
title: "Configuration"
description: "Guide de configuration du script foltone_blackmarket"
script: "foltone-blackmarket"
section: "Blackmarket"
order: 2
version: "1.0.0"
---

# Configuration

Toute la configuration se fait dans `config.lua`. Les options sont organisees du plus modifie au moins modifie.

## Reglages de base

```lua
Config.Locale = 'en'                  -- 'fr' | 'en' | 'es'
Config.Debug  = true                  -- logs console

Config.FrameworkOverride = nil        -- 'esx' | 'qbcore' | 'qbox' | 'standalone' | nil (auto)
Config.InventoryOverride = nil        -- 'ox_inventory' | 'qs-inventory' | 'esx' | 'qb' | nil (auto)

Config.MenuType     = 'rageui'        -- 'rageui' (in-game) ou 'nui' (HTML)
Config.TargetSystem = 'auto'          -- 'auto' | 'ox_target' | 'qb-target' | 'qtarget' | 'none'
Config.UseTextUI    = true            -- fallback textUI si TargetSystem='none'

Config.MoneyAccount  = 'cash'         -- compte d'argent utilise
Config.MoneyItemName = 'money'        -- item money pour ox_inventory

Config.PoliceJobs = { 'police', 'lspd', 'sasp', 'bcso' }
```

## Apparence du menu RageUI

```lua
Config.RageUI = {
    Theme = 'modern',                 -- 'classic' (GTA V) | 'modern' (sombre)

    AccentColor = { R = 59, G = 130, B = 246, A = 200 },

    AnimationEnabled = true,
    AnimationSpeed   = 7,

    BannerDict    = 'shopui_title_gunvan',
    BannerTexture = 'shopui_title_gunvan',
}
```

Presets de banniere disponibles : `shopui_title_gunvan` (DLC Drug Wars), `shopui_title_gunclub_shop`, `shopui_title_gunmod_shop`, `shopui_title_gunrunning` (toujours disponible). Les couleurs detaillees du theme modern sont reglables dans `src/config.lua`.

## Cycle de vie du van

```lua
Config.FirstSpawnDelaySeconds = 5  * 60   -- 1er spawn apres demarrage du serveur
Config.LifetimeSeconds        = 30 * 60   -- duree de presence du van
Config.RespawnCooldownSeconds = 45 * 60   -- pause avant un nouveau spawn
Config.AvoidPreviousLocation  = true      -- evite de respawn au meme endroit
```

## Blip carte (permanent)

```lua
Config.ShowBlip           = false  -- deconseille en RP (utiliser le telephone crypte)
Config.RequireContactItem = false  -- blip seulement si le joueur a bm_contact
Config.ContactItemName    = 'bm_contact'
Config.BlipSprite = 110
Config.BlipColor  = 1
Config.BlipScale  = 0.85
```

## Telephone crypte

```lua
Config.EncryptedPhone = {
    enable          = true,
    itemName        = 'bm_encrypted_phone',
    cooldownSeconds = 30,

    -- Phase 1 : blip de recherche clignotant
    searchBlipSprite   = 161,
    searchBlipColor    = 1,
    searchBlipScale    = 1.2,
    searchBlipFlash    = true,
    searchBlipDuration = 20,

    -- Phase 2 : position precise du van
    vanBlipSprite      = 110,
    vanBlipColor       = 5,
    vanBlipScale       = 0.95,
    vanBlipDuration    = 60,
}
```

Quand le joueur utilise l'item, un blip 161 clignotant apparait pendant 20 secondes, puis la position precise du van pendant 60 secondes.

## Police & heat

```lua
Config.CopFleeMode       = true     -- le marchand fuit si un flic approche
Config.CopFleeRadius     = 80.0
Config.PoliceAlertChance = 0.10     -- 10% de chance d'alerte par achat

Config.HeatSystem         = true    -- accumulation de chaleur sur le van
Config.HeatThreshold      = 8       -- despawn force au-dela
Config.HeatDecayPerMinute = 1
```

## Economie

```lua
Config.StockVariance = 0.30   -- variation stock entre vans (+/-30%)
Config.PriceVariance = 0.10   -- variation prix entre vans (+/-10%)

Config.MaxBuyDistance     = 5.0
Config.BuyCooldownSeconds = 3
```

## Interaction

```lua
Config.InteractDistance = 3.5

-- BoxZone pour ox_target (le ped est attache au van : pas de raycast)
Config.TargetZoneOffset = vector3(0.0, -2.6, 0.5)
Config.TargetZoneSize   = vector3(2.2, 2.2, 2.0)
```

## Emplacements de spawn

```lua
Config.SpawnLocations = {
    { coords = vector3(1726.13, 3284.20, 41.22), heading = 200.0, label = 'Sandy Shores - Entrepot' },
    -- ... ajoutez-en autant que voulu (~10 presets par defaut commentes)
}
```

## Items et armes

Chaque item a une cle, un invName (nom inventaire), une categorie, un prix, un stock, etc.

```lua
Config.Items = {
    {
        key = 'weapon_pistol', category = 'weapons',
        invName = 'WEAPON_PISTOL', weaponHash = `WEAPON_PISTOL`, isWeapon = true,
        label = '9mm Pistol', description = 'Compact, reliable, traceable... maybe.',
        price = 4500, stock = 5, minRep = 0, heat = 1,
        stats = { damage = 35, range = 40, fireRate = 55, accuracy = 60 },
        scratched = true,        -- si true : numero de serie 'SCRATCHED' dans la metadata ox_inventory
    },
    -- ...
}
```

### Parametres d'un item

| Champ | Type | Description |
|---|---|---|
| `key` | string | Cle unique (utilisee pour le stock et le price modifier) |
| `category` | string | `'weapons'` \| `'items'` \| `'protection'` \| `'customs'` |
| `invName` | string | Nom de l'item dans l'inventaire |
| `isWeapon` | bool | `true` pour utiliser AddWeapon (1 unite uniquement) |
| `weaponHash` | hash | Utilise pour la preview 3D (`prop_*` autorise pour les items) |
| `price` | number | Prix de base ($) |
| `stock` | number | Quantite max par van (modulee par StockVariance) |
| `minRep` | number | Reputation minimale requise (0 = aucune) |
| `heat` | number | Points de chaleur generes a l'achat |
| `stats` | table | Stats affichees dans le menu (cosmetique) |
| `scratched` | bool | Met `metadata.serial = 'SCRATCHED'` dans ox_inventory |

## Customisation d'armes

```lua
Config.WeaponCustoms = {
    ['WEAPON_PISTOL'] = {
        weaponHash = `WEAPON_PISTOL`,
        label      = '9mm Pistol',
        components = {
            { key = 'p_supp', label = 'Silencieux', price = 800,
              component = `COMPONENT_AT_PI_SUPP_02`, metaName = 'at_pi_supp_02' },
            -- ...
        },
        tints = {
            { key = 't_norm', label = 'Standard', price = 0,    tint = 0 },
            { key = 't_gold', label = 'Or',       price = 1200, tint = 2 },
            -- ...
        },
    },
}
```

Les customs sont proposes uniquement si le joueur **possede deja** l'arme. Le `metaName` correspond a l'entree dans `metadata.components` d'ox_inventory.

## Admin

```lua
Config.AdminAce    = 'foltone_blackmarket.admin'
Config.AdminGroups = { 'admin', 'superadmin', 'god', 'owner' }
```

## Webhook Discord

```lua
Config.Webhook         = ''                          -- vide = desactive
Config.WebhookUsername = 'Foltone Blackmarket'
Config.WebhookColor    = 0x3b82f6
```

Chaque achat (item + custom) envoie un embed avec le joueur, l'item et le prix.

## Sections rarement modifiees

Les sections en bas du fichier de configuration sont reservees aux reglages fins (skin du van, ped, animations, voix, preview 3D, theme NUI). Voir les commentaires dans le fichier.
