---
title: "Instalacion"
description: "Guia de instalacion de Foltone CCTV"
script: "foltone-cctv"
section: "Foltone CCTV"
order: 1
version: "1.1.0"
---

# Instalacion — foltone_cctv

## Requisitos

- **ESX Legacy**, **QBCore** o **QBX** — Framework de FiveM
- **oxmysql** — Libreria MySQL

### Dependencias opcionales

| Dependencia | Proposito | Requerida para |
|-----------|---------|-------------|
| `ox_target` | Interaccion con objetivo 3D | Si `Config.InteractionType = "ox_target"` |
| `screenshot-basic` | Captura de pantalla de camaras | Funcion de captura en la vista de camara |

## Descarga

Descarga el script desde tu cuenta de Tebex y coloca la carpeta `foltone_cctv` en tu directorio `resources/`.

## Configuracion del servidor

Agrega a tu `server.cfg`:

```ini
set screenshot_basic_allow_fs_write "true"

ensure oxmysql
ensure es_extended      # o qb-core / qbx_core
ensure screenshot-basic # opcional, para capturas
ensure foltone_cctv
```

> **Importante**: `foltone_cctv` debe iniciarse **despues** de tu framework y `oxmysql`. La variable `screenshot_basic_allow_fs_write` es necesaria para que la funcion de captura funcione.

## Framework

El script soporta 3 frameworks:

| Framework | Valor de Config | Dependencias |
|-----------|-------------|-------------|
| ESX Legacy | `"esx"` | `es_extended`, `oxmysql` |
| QBCore | `"qbcore"` | `qb-core`, `oxmysql` |
| QBX | `"qbx"` | `qbx_core`, `oxmysql` |

Configura el framework en `config.lua`:

```lua
Config.Framework = "esx" -- "esx", "qbcore" o "qbx"
```

## Base de datos

### Instalacion nueva

Ejecuta el archivo `sql/install.sql` en tu base de datos MySQL:

```bash
mysql -u root -p your_database < sql/install.sql
```

Tambien puedes copiar el contenido del archivo y ejecutarlo en phpMyAdmin o HeidiSQL.

> El script agrega automaticamente las columnas faltantes (`camera_type`, `job_group`) en el primer inicio. No se necesita migracion manual.

## Objetos de inventario

Necesitas registrar los siguientes objetos en tu sistema de inventario (ox_inventory, qb-inventory, etc.):

| Nombre del objeto | Proposito |
|-----------|---------|
| `cctv_tablet` | Tablet de vigilancia — abre el panel de camaras |
| `cctv_station` | Estacion de monitoreo — objeto colocable que abre el panel de camaras |
| `cctv_cam_standard` | Camara Standard — CCTV clasica de pared |
| `cctv_cam_bullet` | Camara Bullet — zoom de largo alcance |
| `cctv_cam_mini` | Camara Mini Bullet — compacta y discreta |
| `cctv_cam_shop` | Camara Shop Cam — PTZ 360 para tiendas |

> Cada tipo de camara tiene su propio objeto. Usar el objeto inicia el modo de colocacion para ese tipo especifico de camara. El objeto de estacion tambien inicia un modo de colocacion en el suelo.

## Verificacion

Despues de reiniciar el servidor:

1. Conectate al servidor con un personaje
2. Ve a la posicion del PED de la tienda configurada en `Config.ShopPositions`
3. Interactua con el vendedor para abrir la tienda
4. Compra una camara, luego usa el objeto para entrar en modo de colocacion
5. Coloca la camara en una pared, ponle un nombre y luego usa la tablet para verla
