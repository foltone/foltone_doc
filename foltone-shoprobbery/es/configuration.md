---
title: "Configuracion"
description: "Guia de configuracion del script foltone_shoprobbery"
script: "foltone-shoprobbery"
section: "Shop Robbery"
order: 2
version: "1.0.0"
---

# Configuracion de foltone_shoprobbery

## Archivo de configuracion

Toda la configuracion se realiza en `config.lua`.

## Posiciones de tiendas

```lua
Config.Shops = {
    {
        coords = vector3(25.7, -1347.3, 29.5),
        robbable = true,
        blip = true,
    },
    -- Agregue tantas tiendas como necesite
}
```

Cada tienda puede definirse como robable o no.

## Parametros del robo

```lua
Config.Robbery = {
    amount = {min = 500, max = 2000},
    requiredPolice = 2,
    cooldown = 1200, -- segundos (20 minutos)
    duration = 15000, -- duracion del robo en ms
}
```

| Parametro | Descripcion |
|-----------|-------------|
| `amount` | Rango de dinero obtenido del robo |
| `requiredPolice` | Numero minimo de policias en servicio |
| `cooldown` | Tiempo de espera entre dos robos de la misma tienda |
| `duration` | Duracion de la barra de progreso del robo |

## Condiciones de cancelacion

El robo se cancela automaticamente si:
- El jugador se mueve durante el robo
- El PNJ vendedor muere

## Articulos de la tienda

```lua
Config.ShopItems = {
    { item = "bread", label = "Pan", price = 10 },
    { item = "water", label = "Agua", price = 5 },
    -- Agregue sus articulos aqui
}
```

## Notificaciones policiales

```lua
Config.PoliceNotification = function(source, coords)
    -- Personalice el envio de notificacion aqui
    -- Incluye foto del sospechoso y geolocalizacion
end
```

Adapte esta funcion para su sistema de despacho. La notificacion incluye automaticamente una foto del sospechoso y la posicion GPS de la tienda.
