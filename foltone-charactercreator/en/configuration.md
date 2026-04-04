---
title: "Configuration"
description: "Configuration guide for foltone_charactercreator script"
script: "foltone-charactercreator"
section: "Character Creator"
order: 2
version: "1.0.0"
---

# Configuration

All configuration is done in the `config.lua` file.

## General settings

```lua
Config.Locale = 'en'                    -- Language (fr, en, es)
Config.CameraPosition = vector3(0, 0, 0) -- Camera position during creation
```

## Customization options

### Face shape

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

### Hair

```lua
Config.HairOptions = {
    maxMaleHair = 36,        -- Number of male hairstyles
    maxFemaleHair = 38,      -- Number of female hairstyles
    maxHairColors = 64,      -- Number of colors
    maxHighlightColors = 64, -- Number of highlight colors
}
```

### Clothing

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

### Default values

```lua
Config.DefaultSkin = {
    sex = 0,            -- 0 = male, 1 = female
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
Config.EnableHeritage = true  -- Enable parent system (face blending)
Config.MaxFathers = 45        -- Number of father models
Config.MaxMothers = 45        -- Number of mother models
```

The heritage system blends traits from two parents to create a unique face using a resemblance slider.
