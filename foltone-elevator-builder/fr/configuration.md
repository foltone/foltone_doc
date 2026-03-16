---
title: "Configuration"
description: "Configuration du script Elevator Builder"
script: "foltone-elevator-builder"
section: "Elevator Builder"
order: 2
version: "1.1.0"
---

# Configuration — foltone_elevator_builder

Toute la configuration se fait dans le fichier `Config.lua` à la racine du script. Certains paramètres sont également modifiables en jeu via le panneau de configuration du menu admin.

## Langue

```lua
Config.Locale = 'fr' -- 'fr', 'en' ou 'es'
```

Trois langues sont incluses : français, anglais et espagnol. Les traductions sont dans le dossier `locales/`. Vous pouvez ajouter vos propres langues en créant un nouveau fichier.

## Marqueur

Le marqueur indique les positions d'étages aux joueurs.

```lua
Config.marker_type = 25
Config.marker_scale = 0.8
Config.marker_red = 114
Config.marker_green = 204
Config.marker_blue = 114
Config.marker_alpha = 180
Config.marker_bob = false
Config.marker_spin = true
```

| Paramètre | Description |
|-----------|-------------|
| `marker_type` | Type de marqueur GTA V (voir [wiki FiveM](https://docs.fivem.net/docs/game-references/markers/)) — types supportés : 1, 2, 6, 20, 25, 27, 29 |
| `marker_scale` | Taille du marqueur |
| `marker_red/green/blue` | Couleur RGB du marqueur |
| `marker_alpha` | Opacité (0-255) |
| `marker_bob` | Active/désactive l'animation de rebond |
| `marker_spin` | Active/désactive l'animation de rotation |

> Chaque ascenseur peut également avoir son propre style de marqueur personnalisé, configurable via le menu admin lors de la création ou de la modification.

## Distances

```lua
Config.marker_render_distance = 10.0
Config.interaction_distance = 3.5
```

| Paramètre | Description |
|-----------|-------------|
| `marker_render_distance` | Distance (en mètres) à laquelle le marqueur est affiché |
| `interaction_distance` | Distance à laquelle le joueur peut interagir (touche E ou système de ciblage) |

## Système de ciblage

```lua
Config.use_target = 'auto'
```

| Valeur | Comportement |
|--------|-------------|
| `'auto'` | **Détection automatique** — utilise le premier système de ciblage disponible (comportement par défaut) |
| `'ox_target'` | Force l'utilisation d'**ox_target** |
| `'qb-target'` | Force l'utilisation de **qb-target** |
| `'interact'` | Force l'utilisation d'**interact** (Renewed) |
| `false` | Désactivé — interaction via la **touche E** uniquement |

L'ordre de détection en mode `'auto'` est : ox_target → qb-target → interact.

> Si le système de ciblage configuré n'est pas détecté, le script utilise automatiquement la touche E comme fallback.

## Animation de téléportation

```lua
Config.teleport_animation = true
Config.teleport_duration = 2000
Config.teleport_fade_duration = 500
```

| Paramètre | Description |
|-----------|-------------|
| `teleport_animation` | Active/désactive l'animation de fondu noir lors de la téléportation |
| `teleport_duration` | Durée totale de la transition en millisecondes |
| `teleport_fade_duration` | Durée du fondu noir (entrée et sortie) en millisecondes |

Quand l'animation est activée, le joueur voit :
1. Fondu noir (fermeture des portes)
2. Téléportation + attente (simulation du déplacement)
3. Fondu clair (ouverture des portes)

## Sons

```lua
Config.sounds_enabled = true
Config.sound_volume = 0.5
```

| Paramètre | Description |
|-----------|-------------|
| `sounds_enabled` | Active/désactive les effets sonores |
| `sound_volume` | Volume des sons (0.0 à 1.0) |

Sons joués :
- **Ding** — À l'arrivée à l'étage
- **Portes** — À l'ouverture/fermeture du panneau
- **Déplacement** — Pendant la transition entre étages

## Apparence du panneau

Personnalisez l'interface du panneau d'ascenseur affichée aux joueurs.

```lua
Config.panel_accent_r = 255
Config.panel_accent_g = 180
Config.panel_accent_b = 0
Config.panel_scale = 1.0
Config.panel_side = 'right'
```

| Paramètre | Description |
|-----------|-------------|
| `panel_accent_r/g/b` | Couleur d'accentuation du panneau d'ascenseur (RGB) — doré par défaut |
| `panel_scale` | Multiplicateur de taille du panneau (plage recommandée : 0.7 à 1.3) |
| `panel_side` | Position du panneau à l'écran : `'left'` ou `'right'` |

> Chaque ascenseur peut avoir son propre style de panneau personnalisé, configurable lors de la création ou de la modification.

## Panneau de configuration en jeu

Tous les paramètres ci-dessus sont également modifiables **en jeu** via le panneau de configuration accessible depuis le menu admin (`/fab` → bouton Configuration). Les changements sont appliqués immédiatement et diffusés à tous les clients connectés.

## Personnalisation de la commande

Dans `client/cl_editable.lua`, vous pouvez modifier la commande d'accès au menu admin :

```lua
RegisterCommand("fab", function(source, args)
    TriggerEvent("foltone_ascenseur:open_menu")
end)
```

Remplacez `"fab"` par le nom de commande souhaité.
