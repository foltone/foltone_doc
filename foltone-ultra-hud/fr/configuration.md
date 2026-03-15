---
title: "Configuration"
description: "Reference de configuration Ultra HUD"
script: "foltone-ultra-hud"
section: "foltone_ultra_hud"
order: 2
version: "1.0.0"
---

# Configuration — foltone_ultra_hud

Tous les parametres sont dans `config.lua`. La plupart peuvent etre modifies en jeu via le panneau admin.

## Langue

```lua
Config.locale = "en" -- "en", "fr", etc.
```

Les fichiers de traduction sont dans `locales/en.lua`, `locales/fr.lua`. Vous pouvez ajouter votre propre langue en creant un nouveau fichier (ex : `locales/de.lua`).

## General

| Option | Type | Defaut | Description |
|---|---|---|---|
| `disableMinimap` | boolean | `false` | Cacher entierement la minimap GTA |
| `disableMinimapHealtharmour` | boolean | `true` | Cacher les barres vie/armure de la minimap GTA |
| `disableNoMoney` | boolean | `true` | Cacher les champs argent quand le solde est 0 |
| `disableArmour` | boolean | `true` | Cacher auto la barre d'armure quand la valeur est 0 |
| `disableApnea` | boolean | `true` | Cacher auto la barre d'apnee quand pleine (pas sous l'eau) |
| `disableStamina` | boolean | `true` | Cacher auto la barre de stamina quand pleine (pas en sprint) |

## Visibilite

Chaque element du HUD peut etre active/desactive individuellement. Ces valeurs servent de defaut et peuvent etre modifiees via le panneau admin.

| Option | Type | Defaut | Description |
|---|---|---|---|
| `id` | boolean | `true` | Afficher l'ID serveur du joueur |
| `job` | boolean | `true` | Afficher le metier et le grade |
| `job2` | boolean | `false` | Afficher le 2e metier / gang (ESX: job2, QB: gang) |
| `money` | boolean | `true` | Afficher l'argent liquide |
| `bank` | boolean | `true` | Afficher le solde bancaire |
| `black_money` | boolean | `true` | Afficher l'argent sale (ESX: black_money, QB: crypto) |
| `position` | boolean | `true` | Afficher le nom de la rue |
| `health` | boolean | `true` | Afficher la barre de vie |
| `armour` | boolean | `true` | Afficher la barre d'armure |
| `hunger` | boolean | `true` | Afficher la barre de faim |
| `thirst` | boolean | `true` | Afficher la barre de soif |
| `stamina` | boolean | `true` | Afficher la barre de stamina |
| `apnea` | boolean | `true` | Afficher la barre d'apnee |
| `speedometer` | boolean | `true` | Afficher le compteur de vitesse en vehicule |

## Affichage

| Option | Type | Defaut | Description |
|---|---|---|---|
| `type_needs_display` | string | `"bar"` | Mode d'affichage des statuts : `"bar"`, `"circle"`, `"square"`, `"hexagon"`, `"text"` |
| `shape_fill_mode` | string | `"stroke"` | Style de remplissage : `"stroke"` (contour) ou `"fill"` (remplissage solide bas vers haut) |
| `metric` | string | `"kmh"` | Unite de vitesse : `"kmh"` ou `"mph"` |

## Couleurs par defaut

Les couleurs sont definies en tableaux RGBA `{R, G, B, A}` avec des valeurs de 0 a 255.

```lua
Config.colorText    = {255, 255, 255, 255}  -- Blanc
Config.healthColor  = {53, 154, 71, 255}    -- Vert
Config.armourColor  = {51, 131, 236, 255}   -- Bleu
Config.hungerColor  = {245, 166, 35, 255}   -- Orange
Config.thirstColor  = {0, 168, 255, 255}    -- Cyan
Config.staminaColor = {245, 220, 63, 255}   -- Jaune
Config.apneaColor   = {123, 153, 229, 255}  -- Bleu clair
Config.fuelColor    = {255, 0, 0, 255}      -- Rouge
```

> Toutes les couleurs peuvent etre changees via les selecteurs de couleur du panneau admin.

## Notifications

Ces valeurs servent de defaut. Elles peuvent etre modifiees via le panneau admin.

| Option | Type | Defaut | Description |
|---|---|---|---|
| `notifPosition` | string | `"top-center"` | Position des notifications a l'ecran |
| `notifWidth` | number | `25` | Largeur en unites `vw` (largeur du viewport) |
| `notifScale` | number | `1.0` | Multiplicateur de taille (0.5 a 2.0) |

Positions disponibles : `"top-left"`, `"top-center"`, `"top-right"`, `"bottom-left"`, `"bottom-center"`, `"bottom-right"`

> En `bottom-left`, les notifications se positionnent automatiquement au-dessus de la minimap GTA et s'adaptent a sa largeur (15vw).

## Menu Admin

| Option | Type | Defaut | Description |
|---|---|---|---|
| `adminCommand` | string | `"hudadmin"` | Commande chat pour ouvrir le panneau admin |
| `adminGroups` | table | `{"admin", "superadmin", "god"}` | Groupes framework autorises a acceder au panneau |

Pour le standalone, vous pouvez definir une verification personnalisee :

```lua
Config.customAdminCheck = function(src)
    return IsPlayerAceAllowed(src, "admin")
end
```

Ordre de verification des permissions :
1. **Groupe framework** — ESX: groupe `admin`, `superadmin`, `god` / QBCore: permission `admin`, `god`
2. **Groupes personnalises** — Tout groupe liste dans `Config.adminGroups`
3. **Fallback ACE** — Permission `command.hudadmin`
