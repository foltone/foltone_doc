---
title: "Uso"
description: "Guía de uso del script Vigneron"
script: "foltone-vigneron"
section: "Vigneron"
order: 3
version: "2.0.0"
---

# Uso — foltone_vigneron

## Entrar en servicio

Presione **F6** → **Activar/desactivar servicio**. Se envía un anuncio a todos los jugadores.

## Pipeline de producción

1. **Recolección**: Recolecte uvas en los puntos de cosecha
2. **Transformación**: Procese las uvas en jugo/vino
3. **Venta**: Venda los productos (dinero repartido entre jugador y sociedad)

Cada paso usa barras de progreso ox_lib con animaciones, cancelable en cualquier momento.

## Menú F6, Cofres, Vestuario, Garaje, Menú Jefe

Funciones estándar de trabajo. Consulte la documentación en francés para más detalles.

## Archivos editables

- `client/cl_editable.lua`: `OnVehicleSpawned()`, `SendBill()`
- `server/sv_editable.lua`: `OnHarvestComplete()`, `OnTransformComplete()`, `OnSellComplete()`

## Seguridad

Rate limiting, validación servidor, anti-cheat en montos de venta, logs Discord opcionales.
