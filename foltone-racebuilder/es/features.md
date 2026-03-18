---
title: "Caracteristicas"
description: "Resumen de caracteristicas de Race Builder"
script: "foltone-racebuilder"
section: "Race Builder"
order: 3
version: "1.1.0"
---

# Caracteristicas — foltone_racebuilder

## Editor de carreras (`/raceeditor`)

- **Camara noclip** — Vuela por el mapa para colocar checkpoints
- **Colocacion de NPC** — Coloca un NPC interactivo con vista previa
- **Punto de aparicion / Parrilla de salida** — Parrilla escalonada estilo F1 para carreras multijugador
- **Colocacion de checkpoints** — Clic para colocar, clic derecho para agarrar y mover los existentes
- **Tamano de checkpoint ajustable** — Rueda del raton para redimensionar cada checkpoint individualmente
- **Rotacion de checkpoint** — Teclas Q/E para rotar la orientacion del checkpoint
- **Gestor de checkpoints** — La tecla Enter abre un menu para reordenar, teletransportar y eliminar checkpoints
- **Editar propiedades de carrera** — Cambiar nombre, vehiculo, tipo de carrera, vueltas y jugadores maximos en carreras existentes desde el gestor de checkpoints
- **Vista previa del marcador de salida/meta** — Marcador de checkpoint visible en tiempo real durante la colocacion del punto de aparicion
- **Vista previa mejorada de la parrilla** — Marcadores circulares con posiciones numeradas para la parrilla de salida
- **Carrera de prueba** — Prueba tu carrera directamente desde el editor
- **Editar carreras existentes** — Carga cualquier carrera guardada, abre directamente el gestor de checkpoints
- **Deteccion automatica AZERTY/QWERTY**

## Modos de carrera

### Contrarreloj individual
- El jugador corre solo contra el reloj
- Los mejores tiempos se guardan en la tabla de clasificacion
- Records personales registrados por jugador

### Multijugador (Simultaneo)
- Sistema de lobby con controles del anfitrion
- Parrilla de salida estilo F1 con posiciones escalonadas
- Seguimiento de posicion en tiempo real durante la carrera
- Clasificacion en tiempo real transmitida a todos los jugadores
- Pantalla de resultados finales con clasificaciones

### Ambos
- La carrera soporta tanto el modo individual como el multijugador

## Caracteristicas de la carrera

- **Circuitos en bucle** — La linea de salida es tambien la meta, con multiples vueltas
- **Seguimiento de tiempos por vuelta** — Tiempos de vuelta individuales mostrados en el HUD
- **Ruta GPS** — Blip con ruta GPS hacia el siguiente checkpoint
- **Congelacion en cuenta regresiva** — Vehiculo congelado durante la cuenta regresiva
- **Deteccion de salida del vehiculo** — Descalificacion despues de un tiempo configurable
- **Deteccion de muerte** — La carrera termina si el jugador muere
- **Confirmacion de abandono** — F5 para abandonar con dialogo de confirmacion
- **Carreras instanciadas** — Routing buckets de FiveM para instancias de carrera aisladas

## Sistema de vehiculos

- **Vehiculo obligatorio** — La carrera puede requerir un modelo de vehiculo especifico
- **Multiples vehiculos** — Lista separada por comas, seleccion aleatoria o eleccion del jugador
- **Eleccion libre** — Dejar vacio para cualquier vehiculo
- **Interfaz de seleccion de vehiculos** — Seleccion visual de vehiculos con imagenes desde `config_vehicles.lua`

## Comandos de administrador

| Comando | Descripcion |
|---------|-------------|
| `/raceeditor` | Abrir el editor de carreras (requiere permisos de administrador) |
| `/cancelrace [raceId]` | Cancelar una carrera/lobby activo |
| `/kickrace [playerId]` | Expulsar a un jugador de su carrera actual |

## Sistemas de interaccion

El script soporta multiples metodos de interaccion (deteccion automatica):

1. **ox_target** — Interaccion 3D con el NPC
2. **qb-target** — Interaccion 3D con el NPC
3. **Tecla E como alternativa** — Interaccion por proximidad si no hay sistema de target instalado
