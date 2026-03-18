---
title: "Registro de cambios"
description: "Historial de versiones de Foltone Race Builder"
script: "foltone-racebuilder"
section: "Race Builder"
order: 99
version: "1.1.0"
---

# Registro de cambios

## v1.1.0 — 2026-03-16

### Mejoras del editor
- Editar propiedades de carrera (nombre, vehiculo, tipo, vueltas, jugadores maximos) en carreras existentes desde el gestor de checkpoints
- Editar una carrera ahora abre directamente el gestor de checkpoints en lugar del modo de colocacion
- Vista previa del marcador de salida/meta visible en tiempo real durante la colocacion del punto de aparicion
- Vista previa mejorada de la parrilla de salida con marcadores circulares y posiciones numeradas
- Posiciones de la parrilla alejadas de la linea de salida (opcion de configuracion `StartOffset`)
- Cerrar el gestor de checkpoints (X o cerrar) ahora regresa al modo de colocacion de checkpoints

### Correcciones de errores
- Corregido que los marcadores de checkpoint no aparecian despues de reiniciar el script (compatibilidad entero/flotante de Lua 5.4 con el nativo DrawMarker)
- Corregido error nil en `restorePlayerBucket` causado por el orden de declaracion de funciones
- Corregido que el callback `getRaces` no devolvia datos de checkpoints, causando lista de checkpoints vacia al editar carreras
- Corregidas inconsistencias de estado NUI al navegar entre el formulario del editor y el gestor de checkpoints
- Corregido artefacto de checkpoint de vista previa al cerrar el gestor de checkpoints
- Corregido que `editorNpcPoint` no se guardaba/restauraba durante la carrera de prueba
- Prevenidos hilos duplicados del bucle de colocacion con flag de proteccion

## v1.0.0 — 2026-03-10
- Lanzamiento inicial
- Sistema completo de creacion de carreras
- Editor de checkpoints en el juego
- Tablas de clasificacion y temporizadores
- Soporte para QB-Core y ESX
