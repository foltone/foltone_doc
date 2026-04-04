---
title: "Configuracion"
description: "Guia de configuracion del script foltone_territories"
script: "foltone-territories"
section: "Territories"
order: 2
version: "1.0.0"
---

# Configuracion de foltone_territories

## Archivo de configuracion

Toda la configuracion se realiza en `config.lua`.

## Definicion de zonas

```lua
Config.Zones = {
    {
        name = "Grove Street",
        position = vector3(95.0, -1960.0, 21.0),
        width = 200.0,
        height = 200.0,
        rotation = 0.0,
        capturePoints = 100, -- puntos necesarios para capturar
    },
    -- Agregue tantas zonas como necesite
}
```

| Parametro | Descripcion |
|-----------|-------------|
| `name` | Nombre de la zona mostrado |
| `position` | Coordenadas del centro de la zona |
| `width` | Ancho de la zona |
| `height` | Alto de la zona |
| `rotation` | Rotacion de la zona en grados |
| `capturePoints` | Numero de puntos necesarios para capturar la zona |

## Lista de drogas

```lua
Config.Drugs = {
    {
        item = "weed",
        label = "Marihuana",
        price = 50,
        capturePoints = 5,
        acceptRate = 0.6, -- 60% de probabilidad de aceptar
        rejectRate = 0.3, -- 30% de probabilidad de rechazar
        -- 10% restante = llamar a la policia
    },
    {
        item = "coke",
        label = "Cocaina",
        price = 120,
        capturePoints = 10,
        acceptRate = 0.4,
        rejectRate = 0.4,
    },
}
```

| Parametro | Descripcion |
|-----------|-------------|
| `item` | Nombre del item en el inventario |
| `price` | Precio de venta al PNJ |
| `capturePoints` | Puntos de captura ganados por venta |
| `acceptRate` | Probabilidad de que el PNJ acepte |
| `rejectRate` | Probabilidad de que el PNJ rechace |

La probabilidad restante (1 - acceptRate - rejectRate) es la posibilidad de que el PNJ llame a la policia.

## Trabajos de policia

```lua
Config.PoliceJobs = {"police", "fbi", "sheriff"}
```

Lista de trabajos considerados como fuerzas del orden para las alertas.

## PNJ excluidos

```lua
Config.BlacklistedPeds = {
    "s_m_y_cop_01",
    "s_f_y_cop_01",
    -- PNJ a los que no se puede vender
}
```

## Trabajos de pandilla

```lua
Config.GangJobs = {"ballas", "vagos", "families", "lost"}
```

Solo los jugadores con uno de estos trabajos pueden participar en el sistema de territorios.
