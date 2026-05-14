---
title: "Uso"
description: "Guia de uso del script foltone_blackmarket"
script: "foltone-blackmarket"
section: "Blackmarket"
order: 3
version: "1.0.0"
---

# Uso

## Encontrar el van

El van aparece automaticamente segun el ciclo de spawn del servidor (`FirstSpawnDelaySeconds` luego `LifetimeSeconds` / `RespawnCooldownSeconds`). Elige una ubicacion aleatoria en `Config.SpawnLocations`.

Varias formas de encontrarlo :

1. **Item telefono cifrado** : el jugador usa `bm_encrypted_phone` desde su inventario. Un blip 161 parpadeante aparece durante 20 segundos (zona aproximada), luego la posicion precisa del van durante 60 segundos.
2. **Blip permanente** : si `Config.ShowBlip = true`. Opcionalmente bloqueado por `Config.RequireContactItem`.
3. **Roleplay** : el jugador descubre la ubicacion mediante otros jugadores, contactos, etc.

## Interactuar con el vendedor

Acerquese al van. Segun `Config.TargetSystem` :

- **ox_target / qb-target / qtarget** : aparece una opcion target alrededor del vendedor (zona 2m×2m alrededor del asiento del vendedor).
- **none / fallback** : un textUI propone pulsar **E** a corta distancia.

El menu de la tienda se abre (RageUI in-game o NUI HTML, segun `Config.MenuType`).

## Flujo de compra

El menu propone varias categorias :

1. **Armas** — pistolas, SMG, escopeta, etc. Cada una con su preview 3D, sus stats y un marcador "serial scratched".
2. **Items** — municiones.
3. **Proteccion** — chalecos antibalas, chaleco pesado, kit de salud.
4. **Customs** — componentes (silenciador, mira, cargador extendido...) y tints. Solo las armas que el jugador **ya posee** aparecen aqui.

Preview 3D : cuando un item es destacado, el modelo se muestra delante del van. **La rueda del raton** permite zoom in/out.

Para los customs : un selector de armas con flechas permite cambiar entre las armas customizables que posees.

## Riesgo y heat

- Cada compra tiene una probabilidad (`PoliceAlertChance`, 10% por defecto) de disparar una alerta policial con las coordenadas del comprador.
- Cada compra anade **calor** al van. Por encima del umbral (8 por defecto), el van despawn automaticamente y la policia recibe un blip temporal.
- Un policia que entra en un radio de 80m **hace huir al vendedor** (van + ped desaparecen).

## Comandos admin

El comando `bm_van` esta disponible para los admins (ACE o grupo). Requiere que `Bridge.IsAdmin` devuelva true.

| Comando | Descripcion |
|---|---|
| `bm_van spawn [idx]` | Fuerza el spawn del van (idx opcional para elegir la ubicacion) |
| `bm_van despawn` | Fuerza el despawn inmediato |
| `bm_van status` | Muestra el estado del van (ubicacion, heat) en la consola |

## Permisos

| Accion | Requerido |
|---|---|
| Encontrar via blip permanente | `Config.ShowBlip = true` |
| Encontrar via telefono | Item `bm_encrypted_phone` en el inventario |
| Comprar un arma | Dinero suficiente + reputacion minima si `minRep > 0` |
| Comprar un custom | Poseer ya el arma + dinero suficiente |
| Comandos `bm_van` | ACE `foltone_blackmarket.admin` o grupo en `Config.AdminGroups` |

## Reputacion (opcional)

Si define una funcion `GetPlayerReputation(src)` en un archivo del servidor, los items con `minRep > 0` se bloquearan para los jugadores por debajo del umbral. Sin esta funcion definida, no se aplica gate de reputacion.

## Actualizacion

En cada inicio, el servidor verifica su version contra la version remota. Si hay una nueva version disponible, aparece un mensaje amarillo en la consola con las instrucciones.
