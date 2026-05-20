---
title: "Configuration"
description: "Guide de configuration du script foltone_blackmarket"
script: "foltone-blackmarket"
section: "Blackmarket"
order: 2
version: "1.1.0"
---

# Configuration

Toute la configuration se fait dans `config.lua`. Les options sont organisees du plus modifie au moins modifie. Cette page documente **toutes** les options disponibles afin que vous n'ayez pas a fouiller le fichier.

## Reglages de base

```lua
Config.Locale = 'en'                  -- 'fr' | 'en' | 'es' | 'de'
Config.Debug  = true                  -- logs console
```

| Option | Type | Description |
|---|---|---|
| `Config.Locale` | string | Code langue. Doit correspondre a un fichier `locales/<code>.lua`. Si la langue n'existe pas, fallback automatique vers `en` avec un avertissement console. |
| `Config.Debug` | bool | Active les logs detailles (utile pour le ciblage / animation / phone). |

### Framework & inventaire

```lua
Config.FrameworkOverride = nil        -- 'esx' | 'qbcore' | 'qbox' | 'standalone' | nil (auto)
Config.InventoryOverride = nil        -- 'ox_inventory' | 'qs-inventory' | 'esx' | 'qb' | nil (auto)
```

| Valeur | Effet |
|---|---|
| `nil` | Detection automatique du framework / inventaire actif. |
| `'esx'` | Force ESX (`es_extended`). |
| `'qbcore'` | Force QBCore (`qb-core`). |
| `'qbox'` | Force QBox (`qbx_core`). |
| `'standalone'` | Aucun framework. Bridge minimal (notifications via `lib.notify`). |

### Menu & interaction

```lua
Config.MenuType     = 'nui'           -- 'rageui' (in-game) | 'nui' (HTML)
Config.TargetSystem = 'auto'          -- 'auto' | 'ox_target' | 'qb-target' | 'qtarget' | 'none'
Config.UseTextUI    = true            -- fallback textUI si TargetSystem='none'
Config.UseOxTarget  = true            -- legacy : false force le fallback textUI
```

#### Types de menu (`Config.MenuType`)

| Valeur | Description |
|---|---|
| `'nui'` | Menu HTML/CSS plein ecran, sidebar gauche + preview 3D de l'arme dans le coffre du van. Camera scriptee, drag souris pour faire tourner l'arme, molette pour zoomer. |
| `'rageui'` | Menu in-game style GTA V utilisant la librairie integree `src/*`. Voir la section **Apparence du menu RageUI** ci-dessous pour les themes. |

#### Systemes de target (`Config.TargetSystem`)

| Valeur | Description |
|---|---|
| `'auto'` | Detection automatique dans cet ordre : ox_target → qb-target → qtarget → fallback textUI. |
| `'ox_target'` | BoxZone autour du vendeur (le ped est attache au van, raycast direct sur le ped peut echouer). |
| `'qb-target'` | AddTargetEntity sur le ped. |
| `'qtarget'` | AddTargetEntity sur le ped. |
| `'none'` | Aucun target ; affiche un textUI `[E] Parler au vendeur` quand le joueur est dans `Config.InteractDistance`. |

### Argent & jobs

```lua
Config.MoneyAccount  = 'cash'         -- compte d'argent utilise (ESX/QBCore)
Config.MoneyItemName = 'money'        -- nom item pour ox_inventory standalone

Config.PoliceJobs = { 'police', 'lspd', 'sasp', 'bcso' }
```

| Option | Description |
|---|---|
| `Config.MoneyAccount` | Compte ESX (`money`, `bank`, `black_money`...) ou QBCore (`cash`, `bank`...). |
| `Config.MoneyItemName` | Nom d'item utilise pour les retraits via `ox_inventory` en mode standalone. |
| `Config.PoliceJobs` | Liste des `job.name` consideres comme police (le vendeur fuit s'ils s'approchent, si `Config.CopFleeMode = true`). |

## Apparence du menu RageUI

Ces options ne s'appliquent **que** si `Config.MenuType = 'rageui'`. Pour le mode NUI, voir la section **Apparence du menu NUI** plus bas.

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

### Themes disponibles

| Theme | Description visuelle | A utiliser si... |
|---|---|---|
| `'classic'` | Style GTA V d'origine : gradient bleu/blanc, sprites animes, fond dynamique, sous-titre noir uppercase. | Vous voulez l'apparence GTA standard, coherente avec les menus natifs. |
| `'modern'` | Style sombre moderne : rectangles plats, barre d'accent coloree sur l'item actif, fond solide, animation de remplissage progressive. | Vous voulez un look UI moderne avec votre couleur de marque. |

> Le theme par defaut est `'classic'`. Pour changer, modifiez `Config.RageUI.Theme`. Le theme est charge au demarrage du resource.

### Options communes

| Option | S'applique a | Description |
|---|---|---|
| `AccentColor` | `modern` | Couleur RGBA de la barre laterale sur l'item selectionne. |
| `AnimationEnabled` | `modern` | Active/desactive l'animation de remplissage de l'item actif. |
| `AnimationSpeed` | `modern` | Vitesse de l'animation (1-15, plus haut = plus rapide). |
| `BannerDict` / `BannerTexture` | les deux | Banniere graphique en haut du menu. |

### Bannieres disponibles

Presets recommandes (toujours disponibles, pas de DLC requis) :

| Dict | Texture | Apparence |
|---|---|---|
| `shopui_title_gunclub_shop` | `shopui_title_gunclub_shop` | Banniere Ammu-Nation classique. |
| `shopui_title_gunmod_shop` | `shopui_title_gunmod_shop` | Banniere atelier d'armes. |
| `shopui_title_gunrunning` | `shopui_title_gunrunning` | Banniere DLC Gunrunning (toujours disponible). |
| `shopui_title_gunvan` | `shopui_title_gunvan` | Banniere Gun Van (Drug Wars DLC, fallback automatique si absent). |

### Couleurs avancees du theme modern

Les couleurs detaillees (texte, sous-titre, description, slider, navigation, etc.) sont reglables dans `src/config.lua` :

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

## Apparence du menu NUI

S'applique si `Config.MenuType = 'nui'`. Le menu utilise des variables CSS modifiables a chaud.

```lua
Config.Theme = {
    ['--bg-base']      = '#0b0f1a',   -- fond principal
    ['--bg-panel']     = '#0e1322',   -- fond panneau sidebar
    ['--bg-card']      = '#121829',   -- fond carte item
    ['--bg-hover']     = '#161d32',   -- fond item survole
    ['--accent']       = '#3b82f6',   -- couleur d'accent (bouton acheter)
    ['--accent-light'] = '#60a5fa',   -- accent clair (hover)
    ['--text-primary'] = '#e2e8f0',   -- texte principal
    ['--text-muted']   = '#d3d3d3',   -- texte secondaire
    ['--red']          = '#f87171',   -- couleur erreur / out of stock
    ['--green']        = '#4ade80',   -- couleur succes
}
```

### Preview 3D de l'arme (NUI uniquement)

```lua
Config.PreviewCamOffset     = vector3(0.75, -2.60, 0.80)   -- position camera (offset local du van)
Config.PreviewCamLookOffset = vector3(-0.05, -1.10, 0.50)  -- point regarde (offset local du van)
Config.PreviewCamFov        = 32.0                          -- FOV initial
Config.PreviewZoomStep      = 2.0                           -- pas de zoom (molette)
Config.PreviewMinFov        = 12.0                          -- zoom max
Config.PreviewMaxFov        = 55.0                          -- zoom min
Config.PreviewSensitivity   = 0.6                           -- sensibilite drag souris
Config.PreviewAutoSpin      = true                          -- auto-rotation apres 1.8s d'inactivite
Config.PreviewAutoSpinSpeed = 20.0                          -- vitesse auto-rotation
Config.PreviewWeaponLight   = true                          -- lumiere bleue + blanche sur l'arme

Config.WeaponDisplayOffset   = vector3(0.0, -1.10, 0.55)    -- position arme (offset local du van)
Config.WeaponDisplayRotation = vector3(0.0, 0.0, 0.0)       -- rotation arme initiale
```

## Cycle de vie du van

```lua
Config.FirstSpawnDelaySeconds = 5  * 60   -- 1er spawn apres demarrage du serveur
Config.LifetimeSeconds        = 30 * 60   -- duree de presence du van
Config.RespawnCooldownSeconds = 45 * 60   -- pause avant un nouveau spawn
Config.AvoidPreviousLocation  = true      -- evite de respawn au meme endroit
```

Cycle automatique : `spawn` → attend `LifetimeSeconds` ou stock total epuise → `despawn` → attend `RespawnCooldownSeconds` → `spawn` au prochain emplacement.

## Blip carte (permanent)

```lua
Config.ShowBlip           = false  -- deconseille en RP (utiliser le telephone crypte)
Config.RequireContactItem = false  -- blip seulement si le joueur a bm_contact
Config.ContactItemName    = 'bm_contact'

Config.BlipSprite = 110
Config.BlipColor  = 1
Config.BlipScale  = 0.85
Config.BlipName   = nil            -- nil = utilise la traduction _U('blip_name')
```

## Telephone crypte

```lua
Config.EncryptedPhone = {
    enable          = true,
    itemName        = 'bm_encrypted_phone',
    cooldownSeconds = 30,

    callAnimDurationMs = 4500,   -- duree de l'animation "passer un appel" cote client

    -- Phase 1 : blip de recherche clignotant
    searchBlipSprite      = 161,
    searchBlipColor       = 1,
    searchBlipScale       = 1.2,
    searchBlipFlash       = true,
    searchBlipDuration    = 20,    -- secondes
    searchBlipStartRadius = 300.0, -- rayon initial autour de la vraie position
    searchBlipEndRadius   = 30.0,  -- rayon final (se resserre progressivement)
    searchBlipUpdateMs    = 1200,  -- frequence de mise a jour du blip
    searchBlipJitter      = 12.0,  -- tremblement aleatoire (effet recherche)

    -- Phase 2 : position precise du van
    vanBlipSprite   = 110,
    vanBlipColor    = 5,
    vanBlipScale    = 0.95,
    vanBlipDuration = 60,          -- secondes
}
```

Quand le joueur utilise l'item, un blip clignotant apparait pendant `searchBlipDuration` secondes a une position aleatoire qui se rapproche progressivement de la vraie position, puis la position precise du van pendant `vanBlipDuration` secondes.

## Police & heat

```lua
Config.CopFleeMode       = true     -- le vendeur fuit si un flic approche
Config.CopFleeRadius     = 80.0     -- en metres
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
    { coords = vector3(-318.9387, -2214.3159, 8.3723), heading = 235.3325, label = 'Elysian Island' },
    { coords = vector3(849.5719, -2180.7517, 30.2998), heading =  37.0987, label = 'Cypress Flats' },
    -- ... ajoutez-en autant que voulu
}
```

Le serveur choisit aleatoirement un emplacement. Avec `AvoidPreviousLocation = true`, il evite de reprendre le precedent (si au moins 2 emplacements).

## Categories d'items

```lua
Config.Categories = {
    { key = 'weapons',    labelKey = 'ui_cat_weapons',    icon = 'crosshair' },
    { key = 'items',      labelKey = 'ui_cat_items',      icon = 'box' },
    { key = 'protection', labelKey = 'ui_cat_protection', icon = 'shield' },
    { key = 'customs',    labelKey = 'ui_cat_customs',    icon = 'wrench' },
}
Config.DefaultCategory = 'weapons'
```

| Champ | Description |
|---|---|
| `key` | Cle de la categorie (referencee par chaque item via son champ `category`). |
| `labelKey` | Cle de traduction (voir `locales/*.lua`). |
| `icon` | Icone SVG embarquee. Valeurs supportees : `'crosshair'`, `'box'`, `'shield'`, `'wrench'`. |

Categorie speciale `'customs'` : automatique, n'apparait que si le joueur possede au moins une arme listee dans `Config.WeaponCustoms`.

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
        scratched = true,
    },
    -- ...
}
```

### Parametres d'un item

| Champ | Type | Description |
|---|---|---|
| `key` | string | Cle unique (utilisee pour le stock et le price modifier). |
| `category` | string | `'weapons'` \| `'items'` \| `'protection'` (les categories `customs` sont generees). |
| `invName` | string | Nom de l'item dans l'inventaire. |
| `isWeapon` | bool | `true` pour utiliser AddWeapon (1 unite uniquement). |
| `weaponHash` | hash | Utilise pour la preview 3D (`prop_*` autorise pour les items non-arme). |
| `label` | string | Nom affiche dans le menu. |
| `description` | string | Description affichee sous l'item. |
| `price` | number | Prix de base ($), modifie par `PriceVariance`. |
| `stock` | number | Quantite max par van, modifie par `StockVariance`. |
| `minRep` | number | Reputation minimale requise (0 = aucune). |
| `heat` | number | Points de chaleur generes a l'achat. |
| `stats` | table | Stats affichees dans le menu (`damage`, `range`, `fireRate`, `accuracy`, 0-100). |
| `scratched` | bool | Met `metadata.serial = 'SCRATCHED'` dans ox_inventory. |

## Customisation d'armes

```lua
Config.WeaponCustoms = {
    ['WEAPON_PISTOL'] = {
        weaponHash = `WEAPON_PISTOL`,
        label      = '9mm Pistol',
        components = {
            { key = 'p_supp', label = 'Silencieux', price = 800,
              component = `COMPONENT_AT_PI_SUPP_02`, metaName = 'at_suppressor_light' },
            -- ...
        },
        tints = {
            { key = 't_norm', label = 'Standard', price = 0,    tint = 0 },
            { key = 't_gold', label = 'Or',       price = 1200, tint = 2 },
        },
    },
}
```

Les customs sont proposes uniquement si le joueur **possede deja** l'arme. Le `metaName` correspond a l'entree dans `metadata.components` d'ox_inventory.

## Modele de van

```lua
Config.VanModel      = `burrito3`
Config.VanLockDoors  = true       -- portes verrouillees pour tous
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
    wheelMod        = 6,           -- -1 pour aucun
    livery          = -1,          -- -1 pour aucune
    neonEnable      = false,
    neonR = 59, neonG = 130, neonB = 246,
}

Config.VanProps = {
    { model = `ch_prop_ch_crate_full_01a`, offset = vector3(0.0, -0.50, -0.30), rot = vector3(0.0, 0.0, 0.0) },
    { model = `ch_prop_box_ammo01b`,       offset = vector3(0.30, -1.20, -0.30), rot = vector3(0.0, 0.0, 90.0) },
    { model = `prop_box_ammo07b`,          offset = vector3(0.30, -1.20, -0.10), rot = vector3(0.0, 0.0, 0.0) },
}
```

Les `VanProps` sont des props attaches au van avec un offset local (X=droite, Y=avant, Z=haut). Ils donnent l'aspect "marchandise dans le coffre".

## Comportement des portes

```lua
Config.DoorIndices       = { 2, 3 }    -- indices des portes a ouvrir/fermer
Config.DoorOpenDistance  = 6.0         -- distance d'ouverture (en metres)
Config.DoorCloseDistance = 8.5         -- distance de fermeture
Config.DoorCheckInterval = 250         -- ms entre verifications
Config.DoorAnimStep      = 0.015       -- pas d'animation (plus petit = plus fluide)
Config.DoorMaxAngle      = 1.0         -- angle max d'ouverture (1.0 = grand ouvert)
```

## Vendeur (PED)

```lua
Config.PedModels        = { `IG_GunVanSeller` }   -- aleatoire si plusieurs
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

Config.PedDoorOpenDelayMs = 550     -- delai entre salut et ouverture portes
Config.PedThankCooldownMs = 2500    -- cooldown anti-spam du remerciement
```

## Admin

```lua
Config.AdminAce    = 'foltone_blackmarket.admin'
Config.AdminGroups = { 'admin', 'superadmin', 'god', 'owner' }
```

Les joueurs avec l'ace ou un des groupes peuvent utiliser les commandes admin (`/bm_spawn`, `/bm_despawn`).

## Webhook Discord

```lua
Config.Webhook         = ''                          -- vide = desactive
Config.WebhookUsername = 'Foltone Blackmarket'
Config.WebhookColor    = 0x3b82f6
```

Chaque achat (item + custom) envoie un embed avec le joueur, l'item et le prix.

## Hook de notification personnalise

```lua
Config.Notification = function(msg, kind)
    if lib and lib.notify then
        lib.notify({ description = msg, type = kind or 'inform' })
        return
    end
    -- fallback selon framework...
end
```

Vous pouvez remplacer cette fonction par votre propre systeme de notification (Okok, etc.).
