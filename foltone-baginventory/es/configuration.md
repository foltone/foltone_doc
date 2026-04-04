---
title: "Configuracion"
description: "Guia de configuracion del script foltone_baginventory"
script: "foltone-baginventory"
section: "Bag Inventory"
order: 2
version: "1.0.0"
---

# Configuracion

Toda la configuracion se realiza en el archivo `config.lua`.

## Tipos de bolsas

```lua
Config.BagTypes = {
    ['bag_small'] = {
        label = "Bolsa pequena",
        model = 'prop_cs_heist_bag_01',
        weight = 10,       -- Peso maximo del contenido (kg)
        slots = 5,         -- Numero de espacios
    },
    ['bag_medium'] = {
        label = "Bolsa mediana",
        model = 'prop_poly_bag_01',
        weight = 25,
        slots = 10,
    },
    ['bag_large'] = {
        label = "Bolsa grande",
        model = 'prop_michael_backpack',
        weight = 50,
        slots = 20,
    },
}
```

### Parametros de cada bolsa

| Parametro | Tipo | Descripcion |
|---|---|---|
| `label` | string | Nombre mostrado |
| `model` | string | Modelo 3D para colocacion en el suelo |
| `weight` | number | Capacidad maxima de peso |
| `slots` | number | Numero de espacios disponibles |

## Comportamiento al morir

```lua
Config.DropOnDeath = true    -- Las bolsas caen al suelo cuando el jugador muere
Config.DropAllBags = true    -- Soltar todas las bolsas (true) o solo la equipada (false)
```

## Colocacion en el suelo

```lua
Config.PlaceDistance = 2.0   -- Distancia de colocacion de la bolsa
Config.PickupDistance = 2.0  -- Distancia para recoger una bolsa
```

## Notificaciones

```lua
Config.Notification = function(msg)
    ESX.ShowNotification(msg)
end
```

## Parametros generales

```lua
Config.Locale = 'es'              -- Idioma
Config.FoldBagItem = true         -- Permitir doblar la bolsa para guardarla
Config.MaxBagsPerPlayer = 3       -- Maximo de bolsas por jugador
```
