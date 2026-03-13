---
title: "Configuration"
description: "Configuration du script Elevator Builder"
script: "foltone-elevator-builder"
section: "foltone_elevator_builder"
order: 2
version: "1.0.0"
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
Config.marker_type = 20
Config.marker_red = 114
Config.marker_green = 204
Config.marker_blue = 114
Config.marker_alpha = 250
Config.marker_scaleX = 1.0
Config.marker_scaleY = 1.0
Config.marker_scaleZ = 1.0
```

| Paramètre | Description |
|-----------|-------------|
| `marker_type` | Type de marqueur GTA V (voir [wiki FiveM](https://docs.fivem.net/docs/game-references/markers/)) |
| `marker_red/green/blue` | Couleur RGB du marqueur |
| `marker_alpha` | Opacité (0-255) |
| `marker_scaleX/Y/Z` | Taille du marqueur |

Des paramètres avancés sont aussi disponibles : `marker_dirX/Y/Z`, `marker_rotX/Y/Z`, `marker_bobUpAndDown`, `marker_faceCamera`, `marker_rotate`.

## Distances

```lua
Config.marker_render_distance = 10.0
Config.interaction_distance = 1.0
```

| Paramètre | Description |
|-----------|-------------|
| `marker_render_distance` | Distance (en mètres) à laquelle le marqueur est affiché |
| `interaction_distance` | Distance à laquelle le joueur peut interagir (touche E ou ox_target) |

## Système de ciblage (ox_target)

```lua
Config.use_target = false
```

| Valeur | Comportement |
|--------|-------------|
| `false` | Interaction via la **touche E** (comportement par défaut) |
| `true` | Interaction via **ox_target** (nécessite ox_target installé) |

> Si ox_target n'est pas détecté, le script utilise automatiquement la touche E comme fallback.

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
