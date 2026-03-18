---
title: "Instalacion"
description: "Guia de instalacion de Race Builder"
script: "foltone-racebuilder"
section: "Race Builder"
order: 1
version: "1.1.0"
---

# Instalacion — foltone_racebuilder

## Requisitos

- **ESX Legacy** o **QBCore** o **Standalone** — Framework
- **oxmysql** — Driver de base de datos
- **ox_lib** *(opcional)* — Interfaz mejorada (menus contextuales, dialogos de entrada). Se incluye una alternativa integrada si ox_lib no esta instalado.
- **ox_target** o **qb-target** *(opcional)* — Interaccion 3D con el NPC. Si ninguno esta instalado, se usa la tecla E por proximidad.

## Base de datos

El script creara automaticamente las tablas necesarias en el primer inicio:

- `foltone_races` — Almacena datos de carreras (checkpoints, puntos de aparicion, ajustes)
- `foltone_race_leaderboard` — Mejores tiempos de jugadores por carrera
- `foltone_race_sessions` — Historial de sesiones multijugador

## Descarga

Descarga el script desde tu cuenta de [Tebex](https://foltone.tebex.io/) y coloca la carpeta `foltone_racebuilder` en tu directorio `resources/`.

## Configuracion del servidor

Agrega a tu `server.cfg`:

```ini
ensure oxmysql
ensure es_extended       # o qb-core (opcional para standalone)
ensure ox_lib            # opcional pero recomendado
ensure ox_target         # opcional (o qb-target)
ensure foltone_racebuilder
```

> **Importante**: `foltone_racebuilder` debe iniciarse **despues** de oxmysql y tu framework.

## Verificacion

Despues de reiniciar tu servidor:

1. Conectate al servidor
2. Usa `/raceeditor` para abrir el editor de carreras (requiere permisos de administrador)
3. Crea una carrera de prueba: coloca el NPC, punto de aparicion y al menos 2 checkpoints
4. Interactua con el NPC para abrir el menu de carreras e iniciar una contrarreloj individual
