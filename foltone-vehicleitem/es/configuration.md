---
title: "Configuracion"
description: "Guia de configuracion del script foltone_vehicleitem"
script: "foltone-vehicleitem"
section: "Vehicle Item"
order: 2
version: "1.0.0"
---

# Configuracion

Todos los parametros configurables se encuentran en la carpeta `shared/`.

## Lista de vehiculos

Configure los vehiculos disponibles para compra:

```lua
Config.Vehicles = {
    {
        model = 'bmx',
        label = 'BMX',
        item = 'bmx_item',
        price = 500
    },
    {
        model = 'cruiser',
        label = 'Cruiser',
        item = 'cruiser_item',
        price = 800
    },
    {
        model = 'scorcher',
        label = 'Scorcher',
        item = 'scorcher_item',
        price = 1000
    }
}
```

### Parametros de cada vehiculo

| Parametro | Tipo   | Descripcion                                    |
|-----------|--------|------------------------------------------------|
| `model`   | string | Nombre del modelo GTA (spawn name)             |
| `label`   | string | Nombre mostrado en el menu                     |
| `item`    | string | Nombre del item en la base de datos            |
| `price`   | number | Precio de compra en dolares                    |

Cada `item` debe corresponder a una entrada en su tabla `items` de la base de datos.

## Posicion de la tienda

```lua
Config.Shop = {
    coords = vector3(x, y, z),
    heading = 0.0,
    blip = {
        enabled = true,
        sprite = 226,
        scale = 0.8,
        color = 3,
        label = "Vehiculos"
    },
    ped = {
        model = 's_m_y_shop_mid',
        heading = 0.0
    }
}
```

## Configuracion de spawn

```lua
Config.Spawn = {
    offset = vector3(2.0, 0.0, 0.0), -- desplazamiento respecto al jugador
    deleteOnStore = true -- eliminar el vehiculo al guardarlo
}
```

### Opciones de spawn

- `offset`: posicion relativa al jugador donde aparece el vehiculo.
- `deleteOnStore`: si es `true`, el vehiculo se elimina del mundo cuando el jugador lo guarda (vuelve a ser item).

## Configuraciones adicionales

```lua
Config.UseRageUI = true -- usar RageUI para los menus
Config.Locale = 'es' -- idioma por defecto
```
