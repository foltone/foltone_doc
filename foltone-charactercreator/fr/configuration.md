---
title: "Configuration"
description: "Guide de configuration du script foltone_charactercreator"
script: "foltone-charactercreator"
section: "Character Creator"
order: 2
version: "1.0.0"
---

# Configuration

Toute la configuration se fait dans le fichier `config.lua`.

## Parametres generaux

```lua
Config.Locale = 'fr'                    -- Langue (fr, en, es)
Config.CameraPosition = vector3(0, 0, 0) -- Position de la camera lors de la creation
```

## Options de personnalisation

### Forme du visage

```lua
Config.FaceOptions = {
    noseWidth = { min = -1.0, max = 1.0 },
    noseHeight = { min = -1.0, max = 1.0 },
    noseBridge = { min = -1.0, max = 1.0 },
    cheekboneWidth = { min = -1.0, max = 1.0 },
    cheekboneHeight = { min = -1.0, max = 1.0 },
    jawWidth = { min = -1.0, max = 1.0 },
    jawHeight = { min = -1.0, max = 1.0 },
    chinLength = { min = -1.0, max = 1.0 },
    eyeOpening = { min = -1.0, max = 1.0 },
    lipThickness = { min = -1.0, max = 1.0 },
}
```

### Cheveux

```lua
Config.HairOptions = {
    maxMaleHair = 36,        -- Nombre de coupes homme
    maxFemaleHair = 38,      -- Nombre de coupes femme
    maxHairColors = 64,      -- Nombre de couleurs
    maxHighlightColors = 64, -- Nombre de couleurs de meches
}
```

### Vetements

```lua
Config.ClothingOptions = {
    enableTops = true,
    enablePants = true,
    enableShoes = true,
    enableHats = true,
    enableGlasses = true,
    enableEarrings = true,
    enableChains = true,
    enableWatches = true,
}
```

### Valeurs par defaut

```lua
Config.DefaultSkin = {
    sex = 0,            -- 0 = homme, 1 = femme
    face = 0,
    skin = 0,
    hair_1 = 0,
    hair_2 = 0,
    hair_color_1 = 0,
    hair_color_2 = 0,
    tshirt_1 = 0,
    torso_1 = 0,
    pants_1 = 0,
    shoes_1 = 0,
}
```

## Heritage

```lua
Config.EnableHeritage = true  -- Activer le systeme de parents (melange de visages)
Config.MaxFathers = 45        -- Nombre de modeles de peres
Config.MaxMothers = 45        -- Nombre de modeles de meres
```

Le systeme d'heritage permet de melanger les traits de deux parents pour creer un visage unique avec un curseur de ressemblance.
