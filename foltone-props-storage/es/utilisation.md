---
title: "Uso"
description: "Guía de uso del script Props Storage"
script: "foltone-props-storage"
section: "Props Storage"
order: 3
version: "1.0.0"
---

# Uso — foltone_props_storage

## Funcionamiento general

El script permite a los jugadores colocar cajas fuertes físicas en el mundo del juego. Cada caja fuerte está protegida por un código PIN y solo el propietario puede recogerla.

## Colocar un almacén

1. **Obtener el item** — Un jugador necesita un item de caja fuerte (`big_safe` o `safe`) en su inventario
2. **Usar el item** — Al usar el item, aparece la interfaz de colocación
3. **Posicionar la caja fuerte**:
   - **Flechas del teclado** — Mover la caja fuerte (adelante/atrás/izquierda/derecha)
   - **Teclas A / E** — Rotar la caja fuerte
   - **Enter** — Confirmar la colocación
4. **Establecer el código PIN** — Un diálogo pide un PIN (mínimo 4 dígitos, códigos simples prohibidos)

La caja fuerte se coloca en el mundo y se guarda en la base de datos.

## Acceder al almacén

### Sin ox_inventory (RageUI)

1. Acércate a la caja fuerte (distancia configurable, por defecto 2.5m)
2. Presiona **E** para interactuar
3. Introduce el **código PIN**
4. El menú RageUI se abre con las opciones:
   - **Depositar/Retirar items**
   - **Depositar/Retirar dinero** (efectivo + dinero negro)
   - **Depositar/Retirar armas** (con munición)
   - **Cambiar PIN** *(solo propietario)*
   - **Recoger caja fuerte** *(solo propietario, debe estar vacía)*

### Con ox_inventory

1. Acércate a la caja fuerte
2. Usa **ox_target** para interactuar
3. Introduce el **código PIN**
4. La interfaz de **ox_inventory** se abre como un stash normal
5. Arrastra y suelta los items normalmente

## Sistema de peso

Cada caja fuerte tiene una capacidad máxima de peso:

| Tipo | Modelo | Capacidad |
|------|--------|-----------|
| Caja Fuerte Grande | `p_v_43_safe_s` | 50.000 |
| Caja Fuerte | `prop_ld_int_safe_01` | 30.000 |

Los items tienen un peso definido en ESX/ox_inventory. Las armas tienen un peso configurable en `config.lua`.

## Seguridad PIN

- El PIN debe tener **mínimo 4 dígitos**
- Los códigos simples están **prohibidos**: `0000`, `1111`, `2222`, ..., `9999`, `1234`
- Solo el **propietario** puede cambiar el PIN
- Solo el **propietario** puede recoger la caja fuerte

## Cambiar el código PIN

1. Abre la caja fuerte con tu PIN actual
2. Selecciona **"Cambiar PIN"** en el menú
3. Introduce tu nuevo código PIN

> **Nota**: Esta opción solo es visible para el propietario de la caja fuerte.

## Recoger un almacén

1. Abre la caja fuerte con tu PIN
2. **Vacía completamente** la caja fuerte (items, dinero, armas)
3. Selecciona **"Recoger caja fuerte"**
4. El item de caja fuerte vuelve a tu inventario
5. La caja fuerte se elimina del mundo y de la base de datos

## Instancias / Buckets

El script soporta los **routing buckets** de FiveM. Las cajas fuertes colocadas en una instancia específica solo son visibles dentro de esa instancia.

Para sincronizar la instancia de un jugador desde otro script:

```lua
TriggerClientEvent("foltone_props_storage:updatePlayerInstance", playerId, instanceId)
```

## Logs de Discord

Todas las acciones se registran mediante un webhook de Discord:

- Colocación de una nueva caja fuerte
- Apertura de una caja fuerte
- Depósito / retiro de items
- Depósito / retiro de dinero
- Depósito / retiro de armas
- Cambio de PIN
- Recogida de una caja fuerte

## Events disponibles

### Events del servidor

```lua
-- Colocar una caja fuerte (se activa automáticamente al usar el item)
TriggerServerEvent("foltone_props_storage:addNewPropStorage", ...)

-- Depósito/Retiro
TriggerServerEvent("foltone_props_storage:putPropMoney", id, type, amount)
TriggerServerEvent("foltone_props_storage:takePropMoney", id, type, amount)
TriggerServerEvent("foltone_props_storage:putPropItem", id, itemName, count)
TriggerServerEvent("foltone_props_storage:takePropItem", id, itemName, count)
TriggerServerEvent("foltone_props_storage:putPropWeapon", id, weaponName, ammo)
TriggerServerEvent("foltone_props_storage:takePropWeapon", id, weaponName)
```

### Callbacks del servidor

```lua
-- Verificar PIN y abrir caja fuerte
ESX.TriggerServerCallback("foltone_props_storage:tryOpenProp", function(success)
    -- success: true/false
end, propId, pin)

-- Obtener datos del inventario
ESX.TriggerServerCallback("foltone_props_storage:getPropData", function(data)
    -- data: inventory, weight, etc.
end, propId)

-- Verificar si el jugador es propietario
ESX.TriggerServerCallback("foltone_props_storage:isOwner", function(isOwner)
    -- isOwner: true/false
end, propId)
```

### Events del cliente

```lua
-- Sincronizar instancia del jugador
TriggerClientEvent("foltone_props_storage:updatePlayerInstance", playerId, instanceId)
```
