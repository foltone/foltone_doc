---
title: "Instalacion"
description: "Guia de instalacion de Foltone Garage"
script: "foltone-garage"
section: "Foltone Garage"
order: 1
version: "2.0.0"
---

# Instalacion — foltone_garage

## Requisitos

- **ESX Legacy**, **QBCore** o **QBX** — Framework de FiveM
- **oxmysql** — Libreria MySQL

### Dependencias opcionales

| Dependencia | Proposito | Requerida para |
|-----------|---------|-------------|
| `ox_target` | Interaccion con target 3D | Si `Config.InteractionType = "ox_target"` |
| `qb-target` | Interaccion con target 3D | Si `Config.InteractionType = "qb-target"` |
| `interact` | Interaccion con target 3D | Si `Config.InteractionType = "interact"` |

## Descarga

Descarga el script desde tu cuenta de Tebex y coloca la carpeta `foltone_garage` en tu directorio `resources/`.

## Configuracion del servidor

Agrega a tu `server.cfg`:

```ini
ensure oxmysql
ensure es_extended      # o qb-core / qbx_core
ensure foltone_garage
```

> **Importante**: `foltone_garage` debe iniciarse **despues** de tu framework (`es_extended`, `qb-core` o `qbx_core`) y `oxmysql`.

## Framework

El script soporta 3 frameworks:

| Framework | Valor de Config | Dependencias |
|-----------|-------------|-------------|
| ESX Legacy | `"esx"` | `es_extended`, `oxmysql` |
| QBCore | `"qbcore"` | `qb-core`, `oxmysql` |
| QBX | `"qbx"` | `qbx_core`, `oxmysql` |

Configura el framework en `Config.lua`:

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

### Actualizacion desde una instalacion existente

Si estas actualizando desde una version anterior (antes de v2.0.0), ejecuta el archivo de migracion:

| Archivo | Contenido |
|------|---------|
| `sql/migrate_pound_time.sql` | Agrega la columna `pound_time` a los vehiculos existentes |

> **Importante**: Solo ejecuta `migrate_pound_time.sql` si tienes una instalacion existente. No lo ejecutes en una base de datos nueva.

## Verificacion

Despues de reiniciar el servidor:

1. Conectate al servidor con un personaje
2. Ve a una posicion de garaje configurada en `config_garage.lua`
3. Interactua con el PED (o marcador segun tu configuracion)
4. La interfaz NUI deberia aparecer con las pestanas Vehiculos, Almacenar, Deposito y Etiqueta
