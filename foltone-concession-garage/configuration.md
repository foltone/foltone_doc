---
title: "Configuration"
description: "Configuration de Concession & Garage V2"
script: "foltone-concession-garage"
section: "foltone_concession-garage"
order: 2
---

# Configuration — Concession & Garage V2

## Langue

```lua
Config.Locale = 'fr' -- 'fr' ou 'en'
```

## Points de vente

```lua
Config.Concessions = {
    {
        name = "Premium Deluxe Motorsport",
        type = "car",
        coords = vector3(-56.49, -1098.84, 26.42),
        blip = { sprite = 326, color = 3, scale = 0.8 },
        categories = { "compacts", "sedans", "sports", "super" }
    },
    -- Ajoutez autant de concessions que vous voulez
}
```

## Garages

```lua
Config.Garages = {
    {
        name = "Garage Centre",
        type = "car",
        coords = vector3(215.83, -810.12, 30.73),
        spawn = vector4(219.5, -803.2, 30.5, 155.0)
    },
}
```

## Prix et véhicules

Les véhicules et leurs prix sont configurés dans `vehicles.lua`. Format :

```lua
Config.Vehicles = {
    { model = "adder", label = "Adder", price = 150000, category = "super" },
    { model = "zentorno", label = "Zentorno", price = 120000, category = "super" },
}
```
