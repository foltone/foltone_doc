---
title: "Configuration"
description: "Guide de configuration de Foltone CCTV"
script: "foltone-cctv"
section: "Foltone CCTV"
order: 2
version: "1.0.0"
---

# Configuration — foltone_cctv

Toute la configuration se fait dans le fichier `config.lua`.

## Framework et Langue

```lua
Config.Framework = "esx"       -- "esx", "qbcore" ou "qbx"
Config.Locale = "en"           -- "en" ou "fr"
Config.InteractionType = "ox_target" -- "ox_target", "drawtext" ou "marker"
Config.Debug = false
```

| Parametre | Type | Description |
|-----------|------|-------------|
| `Framework` | string | Framework du serveur |
| `Locale` | string | Langue des notifications et de l'interface |
| `InteractionType` | string | Methode d'interaction avec les PNJ et stations |
| `Debug` | boolean | Activer les messages de debug en console |

## Items

```lua
Config.TabletItem = "cctv_tablet"
Config.StationItem = "cctv_station"
Config.StationProp = "prop_cctv_unit_01"
```

| Parametre | Type | Description |
|-----------|------|-------------|
| `TabletItem` | string | Nom de l'item tablette dans l'inventaire |
| `StationItem` | string | Nom de l'item station de surveillance |
| `StationProp` | string | Modele du prop GTA pour les stations fixes |

## Types de cameras

```lua
Config.MaxCamerasPerPlayer = 10
Config.PlacementDistance = 8.0
```

| Parametre | Type | Description |
|-----------|------|-------------|
| `MaxCamerasPerPlayer` | number | Nombre maximum de cameras par joueur |
| `PlacementDistance` | number | Distance maximale (metres) pour placer une camera |

### Structure d'un type de camera

Chaque entree dans `Config.CameraTypes` definit un modele de camera :

```lua
{
    id = "standard",
    item = "cctv_cam_standard",
    label = "Standard",
    description = "Camera murale classique.",
    specs = { "FOV 70", "ZOOM x4", "60 FPS" },
    prop = "prop_cctv_cam_01a",
    price = 3000,
    offset = {
        pos = vector3(-0.13, 0.61, 0.21),
        pitch = -16.9,
        yaw = 40.0,
        propYaw = 180.0,
    },
    fov = { default = 70.0, min = 25.0, max = 100.0 },
    zoomStep = 5.0,
    rotationSpeed = 2.0,
    maxVertAngle = 60.0,
},
```

| Parametre | Type | Description |
|-----------|------|-------------|
| `id` | string | Identifiant unique (stocke en base de donnees) |
| `item` | string | Nom de l'item inventaire pour ce type |
| `label` | string | Nom affiche dans la boutique |
| `description` | string | Description affichee dans la boutique |
| `specs` | table | Badges de specs affiches dans la boutique |
| `prop` | string | Nom du modele prop GTA |
| `price` | number | Prix d'achat en boutique |
| `offset.pos` | vector3 | Offset de position de la vue camera (avant, gauche, haut) |
| `offset.pitch` | number | Offset de pitch de la vue (degres) |
| `offset.yaw` | number | Offset de yaw de la vue (degres) |
| `offset.propYaw` | number | Offset de rotation du prop par rapport a la direction de vue (degres) |
| `fov.default` | number | Champ de vision par defaut (degres) |
| `fov.min` | number | FOV minimum (zoom max) |
| `fov.max` | number | FOV maximum (dezoom max) |
| `zoomStep` | number | Changement de FOV par cran de scroll |
| `rotationSpeed` | number | Sensibilite de rotation a la souris |
| `maxVertAngle` | number | Angle de rotation vertical maximum (degres) |

### Types par defaut

| ID | Prop | Prix | FOV | Description |
|----|------|------|-----|-------------|
| `standard` | `prop_cctv_cam_01a` | $3 000 | 70 | Camera murale classique |
| `dome` | `prop_cctv_cam_02a` | $5 500 | 90 | Dome grand angle 360 |
| `bullet` | `prop_cctv_cam_04b` | $4 000 | 55 | Longue portee, zoom puissant |
| `mini_bullet` | `hei_prop_bank_cctv_02` | $3 500 | 55 | Compacte et discrete |
| `ptz` | `prop_cctv_cam_05a` | $8 000 | 60 | Pan-Tilt-Zoom professionnelle |

### Calibrer les offsets

Utilisez la commande de debug en jeu pour calibrer les offsets :

```
/cctv_debug
```

1. Approchez-vous d'une camera placee (< 15m)
2. Lancez la commande — entre en vue camera debug
3. Ajustez avec les controles :
   - **Souris** — offset pitch / yaw
   - **Scroll** — rotation du prop (propYaw)
   - **Fleches** — offset de position (avant/arriere/gauche/droite)
   - **E / Q** — offset de position (haut/bas)
   - **Backspace** — quitter et afficher les valeurs
4. Copiez les valeurs affichees dans `Config.CameraTypes[x].offset`

## Permissions

```lua
Config.AllowedJobs = {
    "police",
    "ambulance",
}
```

| Parametre | Type | Description |
|-----------|------|-------------|
| `AllowedJobs` | table | Jobs autorises a poser des cameras. Table vide = tout le monde |

## Detection de mouvement

```lua
Config.MotionDetection = {
    Radius = 15.0,
    Cooldown = 60,
    Default = true,
}
```

| Parametre | Type | Description |
|-----------|------|-------------|
| `Radius` | number | Rayon de detection en metres |
| `Cooldown` | number | Secondes entre les alertes pour la meme camera |
| `Default` | boolean | Detection activee par defaut sur les nouvelles cameras |

## Destruction

```lua
Config.DestructionHits = 3

Config.DestructionWeapons = {
    "WEAPON_CROWBAR",
    "WEAPON_PISTOL",
    -- ...
}
```

| Parametre | Type | Description |
|-----------|------|-------------|
| `DestructionHits` | number | Nombre de coups/tirs necessaires pour detruire une camera |
| `DestructionWeapons` | table | Liste des armes pouvant endommager les cameras |

## Effets visuels

```lua
Config.CameraEffect = {
    timecycle = "CAMERA_secuirity",
    strength = 0.6,
    vignette = 1.0,
    grain = 1.0,
    scanline = 1.0,
}
```

| Parametre | Type | Description |
|-----------|------|-------------|
| `timecycle` | string | Nom du timecycle modifier GTA |
| `strength` | number | Intensite du filtre (0.0 = desactive, 1.0 = max) |
| `vignette` | number | Intensite du vignetage (0.0 = desactive, 1.0 = max) |
| `grain` | number | Intensite du grain (0.0 = desactive, 1.0 = max) |
| `scanline` | number | Intensite de la scanline (0.0 = desactive, 1.0 = max) |

Timecycles disponibles : `CAMERA_secuirity` (defaut), `CAMERA_BW` (noir et blanc), `NG_filmic08` (cinematique), `phone_cam3` (look webcam).

## Captures

```lua
Config.MaxCaptures = 20
```

Nombre maximum de captures sauvegardees par joueur. Quand la limite est atteinte, la plus ancienne est automatiquement supprimee.

> Necessite `screenshot-basic` et `set screenshot_basic_allow_fs_write "true"` dans server.cfg.

## PNJ vendeur

```lua
Config.Ped = {
    model = "s_m_y_ammucity_01",
    scenario = "WORLD_HUMAN_STAND_IMPATIENT",
}
```

## Positions

### Boutiques

```lua
Config.ShopPositions = {
    {
        pos = vector3(72.25, -1399.10, 29.38),
        heading = 270.0,
        blip = { sprite = 689, color = 3, scale = 0.7, label = "Security Shop" },
    },
}
```

### Ordinateurs fixes

```lua
Config.ComputerPositions = {
    { pos = vector3(441.81, -982.08, 30.69), heading = 0.0, label = "computer_label" },
}
```

### Postes de surveillance

```lua
Config.StationPositions = {
    { pos = vector3(441.81, -982.08, 30.69), heading = 0.0 },
}
```

## Interaction

```lua
Config.InteractionDistance = 2.5

Config.Marker = {
    type = 1,
    scale = vector3(1.0, 1.0, 0.5),
    color = { r = 59, g = 130, b = 246, a = 120 },
}
```

## Notifications

```lua
function Notification(source, message, type)
```

Surchargez cette fonction dans `config.lua` pour utiliser votre propre systeme de notification.
