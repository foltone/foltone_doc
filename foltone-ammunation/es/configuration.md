---
title: "Configuracion"
description: "Guia de configuracion del script foltone_ammunation"
script: "foltone-ammunation"
section: "Ammunation"
order: 2
version: "1.0.0"
---

# Configuracion

Toda la configuracion se realiza en el archivo `config.lua`.

## Parametros generales

```lua
Config.Locale = 'es'           -- Idioma (fr, en, es)
Config.PedModel = 's_m_y_ammucity_01' -- Modelo del NPC vendedor
```

## Blip en el mapa

```lua
Config.AmmunationBlip = {
    sprite = 110,    -- Icono del blip
    color = 1,       -- Color (1 = rojo)
    scale = 0.8      -- Tamano del blip
}
```

## Sistema de licencias

```lua
Config.LicensePrice = 5000  -- Precio de la licencia de armas ($)
```

Las armas que requieren licencia estan marcadas con `RequireLicense = true` en la configuracion de pasillos.

## Pasillos y productos

```lua
Config.AisleProductList = {
    {
        label = "Pistolas",
        RequireLicense = true,
        items = {
            { name = "WEAPON_PISTOL", label = "Pistola", price = 2500, type = "weapon" },
            { name = "WEAPON_COMBATPISTOL", label = "Pistola de combate", price = 3500, type = "weapon" },
        }
    },
    {
        label = "Municiones",
        RequireLicense = false,
        items = {
            { name = "ammo_pistol", label = "Municion de pistola", price = 100, type = "item" },
        }
    },
}
```

### Parametros de productos

| Parametro | Tipo | Descripcion |
|---|---|---|
| `name` | string | Nombre tecnico del arma/item |
| `label` | string | Nombre mostrado en el menu |
| `price` | number | Precio de venta |
| `type` | string | `"weapon"` o `"item"` |

## Ubicaciones de tiendas

```lua
Config.AmmunationsList = {
    vector4(-662.18, -935.3, 21.83, 174.89),
    vector4(810.25, -2157.6, 29.62, 0.72),
    -- Agregue mas posiciones...
}
```

## Configuracion de robo

```lua
Config.RobberyMinPolice = 2       -- Minimo de policias en servicio
Config.RobberyCooldown = 1800     -- Tiempo de espera entre robos (segundos)
Config.RobberyMinAmount = 5000    -- Monto minimo del robo
Config.RobberyMaxAmount = 15000   -- Monto maximo del robo
Config.RobberyDistance = 3.0      -- Distancia maxima antes de cancelacion
```

> El robo se cancela si el jugador se aleja del NPC o si el NPC muere.

## Notificaciones

```lua
Config.Notification = function(msg)
    -- Personalice su sistema de notificaciones
    ESX.ShowNotification(msg)
end

Config.DisplayHelpText = function(msg)
    -- Texto de ayuda contextual
    SetTextComponentFormat("STRING")
    AddTextComponentString(msg)
    DisplayHelpTextFromStringLabel(0, 0, 1, -1)
end
```

## Alertas policiales

Durante un robo, los policias reciben:
- Foto del sospechoso (mugshot)
- Geolocalizacion de la tienda
- Notificacion sonora
