---
title: "Configuracion"
description: "Guia de configuracion del script foltone_charactercreator"
script: "foltone-charactercreator"
section: "Character Creator"
order: 2
version: "1.0.0"
---

# Configuracion

Toda la configuracion se realiza en el archivo `config.lua`.

## Parametros generales

```lua
Config.Locale = 'es'                    -- Idioma (fr, en, es)
Config.CameraPosition = vector3(0, 0, 0) -- Posicion de la camara durante la creacion
```

## Opciones de personalizacion

### Forma del rostro

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

### Cabello

```lua
Config.HairOptions = {
    maxMaleHair = 36,        -- Numero de cortes masculinos
    maxFemaleHair = 38,      -- Numero de cortes femeninos
    maxHairColors = 64,      -- Numero de colores
    maxHighlightColors = 64, -- Numero de colores de mechas
}
```

### Ropa

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

### Valores predeterminados

```lua
Config.DefaultSkin = {
    sex = 0,            -- 0 = hombre, 1 = mujer
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

## Herencia

```lua
Config.EnableHeritage = true  -- Activar el sistema de padres (mezcla de rostros)
Config.MaxFathers = 45        -- Numero de modelos de padres
Config.MaxMothers = 45        -- Numero de modelos de madres
```

El sistema de herencia mezcla los rasgos de dos padres para crear un rostro unico con un control deslizante de parecido.
