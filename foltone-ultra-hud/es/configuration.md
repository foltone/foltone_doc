---
title: "Configuración"
description: "Referencia de configuración de Ultra HUD"
script: "foltone-ultra-hud"
section: "Ultra HUD"
order: 2
version: "1.0.0"
---

# Configuración — foltone_ultra_hud

Todos los ajustes están en `config.lua`. La mayoría de estos pueden ser modificados en tiempo real a través del panel de administración.

## Idioma

```lua
Config.locale = "en" -- "en", "fr", etc.
```

Los archivos de traducción están en `locales/en.lua`, `locales/fr.lua`. Puedes agregar tu propio idioma creando un nuevo archivo (ej. `locales/de.lua`).

## General

| Opción | Tipo | Por defecto | Descripción |
|---|---|---|---|
| `disableMinimap` | boolean | `false` | Ocultar completamente el minimapa de GTA |
| `disableMinimapHealtharmour` | boolean | `true` | Ocultar las barras predeterminadas de salud/armadura de GTA en el minimapa |
| `disableNoMoney` | boolean | `true` | Ocultar campos de dinero cuando el saldo es 0 |
| `disableArmour` | boolean | `true` | Ocultar automáticamente la barra de armadura cuando el valor es 0 |
| `disableApnea` | boolean | `true` | Ocultar automáticamente la barra de apnea cuando está llena (no bajo el agua) |
| `disableStamina` | boolean | `true` | Ocultar automáticamente la barra de resistencia cuando está llena (no corriendo) |

## Visibilidad

Cada elemento del HUD puede activarse o desactivarse individualmente. Estos sirven como valores predeterminados y pueden ser modificados a través del panel de administración.

| Opción | Tipo | Por defecto | Descripción |
|---|---|---|---|
| `id` | boolean | `true` | Mostrar ID del jugador en el servidor |
| `job` | boolean | `true` | Mostrar nombre del trabajo y rango |
| `job2` | boolean | `false` | Mostrar segundo trabajo / banda (ESX: job2, QB: gang) |
| `money` | boolean | `true` | Mostrar efectivo (ESX: money, QB: cash) |
| `bank` | boolean | `true` | Mostrar saldo bancario |
| `black_money` | boolean | `true` | Mostrar dinero sucio (ESX: black_money, QB: crypto) |
| `position` | boolean | `true` | Mostrar nombre de la calle |
| `health` | boolean | `true` | Mostrar barra de salud |
| `armour` | boolean | `true` | Mostrar barra de armadura |
| `hunger` | boolean | `true` | Mostrar barra de hambre |
| `thirst` | boolean | `true` | Mostrar barra de sed |
| `stamina` | boolean | `true` | Mostrar barra de resistencia |
| `apnea` | boolean | `true` | Mostrar barra de apnea |
| `speedometer` | boolean | `true` | Mostrar velocímetro en vehículo |

## Pantalla

| Opción | Tipo | Por defecto | Descripción |
|---|---|---|---|
| `type_needs_display` | string | `"bar"` | Modo de visualización de estado: `"bar"`, `"circle"`, `"square"`, `"hexagon"`, `"text"` |
| `shape_fill_mode` | string | `"stroke"` | Estilo de relleno de forma: `"stroke"` (progreso de contorno) o `"fill"` (relleno sólido de abajo hacia arriba) |
| `metric` | string | `"kmh"` | Unidad de velocidad: `"kmh"` o `"mph"` |

## Colores Predeterminados

Los colores se definen como arrays RGBA `{R, G, B, A}` con valores de 0 a 255.

```lua
Config.colorText    = {255, 255, 255, 255}  -- Blanco
Config.healthColor  = {53, 154, 71, 255}    -- Verde
Config.armourColor  = {51, 131, 236, 255}   -- Azul
Config.hungerColor  = {245, 166, 35, 255}   -- Naranja
Config.thirstColor  = {0, 168, 255, 255}    -- Cian
Config.staminaColor = {245, 220, 63, 255}   -- Amarillo
Config.apneaColor   = {123, 153, 229, 255}  -- Azul claro
Config.fuelColor    = {255, 0, 0, 255}      -- Rojo
```

> Todos los colores se pueden cambiar a través de los selectores de color del panel de administración.

## Notificaciones

Estos sirven como valores predeterminados. Pueden ser modificados a través del panel de administración.

| Opción | Tipo | Por defecto | Descripción |
|---|---|---|---|
| `notifPosition` | string | `"top-center"` | Posición de las notificaciones en pantalla |
| `notifWidth` | number | `25` | Ancho en unidades `vw` (ancho del viewport) |
| `notifScale` | number | `1.0` | Multiplicador de escala (0.5 a 2.0) |

Posiciones disponibles: `"top-left"`, `"top-center"`, `"top-right"`, `"bottom-left"`, `"bottom-center"`, `"bottom-right"`

> Cuando se establece en `bottom-left`, las notificaciones se posicionan automáticamente encima del minimapa de GTA y coinciden con su ancho (15vw).

## Menú de Administración

| Opción | Tipo | Por defecto | Descripción |
|---|---|---|---|
| `adminCommand` | string | `"hudadmin"` | Comando de chat para abrir el panel de administración |
| `adminGroups` | table | `{"admin", "superadmin", "god"}` | Grupos del framework con acceso al panel |

Para standalone, puedes definir una verificación de administrador personalizada:

```lua
Config.customAdminCheck = function(src)
    return IsPlayerAceAllowed(src, "admin")
end
```

El permiso de administrador se verifica en este orden:
1. Verificación de grupo del framework (grupo ESX, permiso QBCore)
2. Respaldo de permiso ACE (`command.<adminCommand>`)
