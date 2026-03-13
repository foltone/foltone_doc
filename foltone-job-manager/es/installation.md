---
title: "Instalación"
description: "Guía de instalación del script Job Manager"
script: "foltone-job-manager"
section: "foltone_job_manager"
order: 1
version: "1.0.0"
---

# Instalación — foltone_job_manager

## Requisitos

- **ESX Legacy** o **QBCore** o **Standalone**
- **oxmysql** — Librería MySQL
- **esx_addonaccount** *(solo ESX)* — Para la gestión de cuentas de sociedad

## Descarga

Descarga el script desde tu cuenta Tebex y coloca la carpeta en tu directorio `resources/`.

## Configuración del servidor

Añade en tu `server.cfg`:

```ini
ensure oxmysql
ensure es_extended # o qb-core
ensure foltone_job_manager
```

> **Importante**: `foltone_job_manager` debe iniciarse **después** de tu framework (`es_extended` o `qb-core`) y `oxmysql`.

## Framework

El script soporta 3 modos:

| Framework | Valor config | Dependencias |
|-----------|-------------|--------------|
| ESX Legacy | `"esx"` | `es_extended`, `oxmysql`, `esx_addonaccount` |
| QBCore | `"qbcore"` | `qb-core`, `oxmysql`, `qb-banking` |
| Standalone | `"standalone"` | Configuración manual requerida |

Configura el framework en `config.lua`:

```lua
Config.Framework = "esx" -- "esx", "qbcore" o "standalone"
```

## Verificación

Después de reiniciar el servidor:

1. Conéctate con un personaje que tenga el grado **boss** de un trabajo configurado
2. Ve al marcador de la sociedad (posición configurada en `config.lua`)
3. Presiona **E** para abrir la interfaz de gestión
4. La interfaz de tablet debería aparecer con las pestañas: Dinero, Empleados, Salarios, Transferencias
