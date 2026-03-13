---
title: "Configuración"
description: "Guía de configuración del script Props Storage"
script: "foltone-props-storage"
section: "foltone_props_storage"
order: 2
version: "1.0.0"
---

# Configuración — foltone_props_storage

Toda la configuración se realiza en el archivo `config.lua` en la raíz del script.

## Idioma

```lua
Config.Locale = "fr" -- "fr" o "en"
```

Las traducciones están en la carpeta `locales/`. Puedes añadir tus propios idiomas creando un nuevo archivo (ej: `locales/de.lua`).

## Inventario

```lua
Config.useOxInventory = GetResourceState("ox_inventory") ~= "missing"
```

El script detecta automáticamente si **ox_inventory** está instalado:
- **Con ox_inventory**: usa el sistema de stash nativo + ox_target para la interacción
- **Sin ox_inventory**: usa el menú RageUI integrado + tecla E para interactuar

## Guardado en base de datos

```lua
Config.saveToDBWithInterval = true
Config.saveToDBInterval = 60 * 1000 -- 1 minuto
```

| Opción | Descripción |
|--------|-------------|
| `saveToDBWithInterval = true` | Guardado periódico (recomendado para servidores con muchos jugadores) |
| `saveToDBWithInterval = false` | Guardado en cada acción (depósito/retiro) |

> **Nota**: Cuando `useOxInventory` está activado, `saveToDBWithInterval` se fuerza a `true`.

## Distancia de interacción

```lua
Config.distance = 2.5
```

Distancia máxima (en metros) a la que un jugador puede interactuar con un almacén.

## Códigos PIN prohibidos

```lua
Config.forbidenPIN = {
    0000, 1111, 2222, 3333, 4444,
    5555, 6666, 7777, 8888, 9999,
    1234,
}
```

Los jugadores no podrán usar estos códigos PIN. El PIN debe tener al menos 4 dígitos.

## Tipos de almacenes

```lua
Config.propsList = {
    ["p_v_43_safe_s"] = {
        capacity = 50000,      -- Capacidad de peso
        itemName = "big_safe", -- Nombre del item ESX requerido
        itemLabel = "Caja Fuerte Grande",
    },
    ["prop_ld_int_safe_01"] = {
        capacity = 30000,
        itemName = "safe",
        itemLabel = "Caja Fuerte",
    },
}
```

Puedes añadir tantos tipos de almacenes como quieras. Cada entrada usa el **nombre del modelo GTA** como clave.

### Añadir un nuevo tipo de almacén

1. Encuentra el nombre del modelo del prop GTA V que deseas
2. Añade una entrada en `propsList`:

```lua
["nombre_del_modelo"] = {
    capacity = 40000,
    itemName = "mi_caja_fuerte",
    itemLabel = "Mi Caja Fuerte Custom",
},
```

3. No olvides añadir el item correspondiente en tu base de datos ESX

## Grados de jefe

```lua
Config.bossGrades = {
    ["boss"] = true,
    ["underboss"] = true,
    ["capodecina"] = true,
    ["consigliere"] = true,
    ["don"] = true,
}
```

Grados de trabajo que tienen permisos especiales (permisos de jefe).

## Pesos de armas

```lua
Config.defaultWeaponWeight = 3

Config.weaponWeight = {
    ["WEAPON_KNIFE"] = 2,
    ["WEAPON_PISTOL"] = 4,
    ["WEAPON_ASSAULTRIFLE"] = 8,
    ["WEAPON_RPG"] = 10,
    -- ... ver config.lua para la lista completa
}
```

Las armas no listadas usan `defaultWeaponWeight`. Más de 40 armas están preconfiguradas.

## Notificaciones

```lua
Config.Notification = function(text)
    SetNotificationTextEntry("STRING")
    AddTextComponentString(text)
    DrawNotification(false, true)
end
```

Reemplaza esta función con tu sistema de notificaciones preferido (ej: okokNotify, ox_lib notify, etc.).

## Texto de ayuda

```lua
Config.DisplayHelpText = function(text)
    SetTextComponentFormat("STRING")
    AddTextComponentString(text)
    DisplayHelpTextFromStringLabel(0, 0, 1, -1)
end
```

Personaliza la visualización del texto de ayuda (se muestra cuando un jugador está cerca de un almacén).

## Webhook de Discord

En `server/sv_editable.lua`, configura tu webhook de Discord para los logs:

```lua
PerformHttpRequest("https://discord.com/api/webhooks/TU_ID/TU_TOKEN", ...)
```

Todas las acciones (colocación, apertura, depósito, retiro, eliminación) se registran en Discord.
