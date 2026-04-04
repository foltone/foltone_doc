---
title: "Uso"
description: "Guia de uso del script foltone_drivingschool"
script: "foltone-drivingschool"
section: "Driving School"
order: 3
version: "1.0.0"
---

# Uso

## Acceder a la autoescuela

1. Dirijase a la ubicacion de la autoescuela marcada en el mapa.
2. Acerquese al NPC instructor.
3. Presione la tecla de interaccion para abrir el menu.

## Examen teorico (codigo de trafico)

### Funcionamiento

1. Seleccione "Examen teorico" en el menu.
2. Pague la tarifa de inscripcion.
3. Aparece una interfaz NUI con las preguntas.
4. Para cada pregunta:
   - Lea la pregunta y las respuestas propuestas.
   - Haga clic en la respuesta elegida.
   - Se muestra un temporizador (limite de tiempo por pregunta).
5. Al final del examen, se muestra su puntuacion.

### Resultado

- **Aprobado** (puntuacion >= umbral configurado): Puede pasar a los examenes practicos.
- **Reprobado**: Debe pagar nuevamente y repetir el examen.

## Examenes practicos

Tres tipos de examenes practicos estan disponibles:

### Examen de coche

1. Seleccione "Examen de coche" en el menu.
2. Pague la tarifa.
3. Aparece un vehiculo de examen.
4. Suba al vehiculo y siga la ruta (puntos de control).
5. Respete las reglas:
   - No exceda el limite de velocidad.
   - Evite colisiones.
   - Pase por todos los puntos de control en orden.
6. Al final de la ruta, se anuncia el resultado.

### Examen de moto

Mismo principio que el examen de coche, con un vehiculo de dos ruedas y una ruta dedicada.

### Examen de camion

Mismo principio, con un camion y una tolerancia de errores reducida.

## Otorgamiento de licencias

Al aprobar:

| Examen | Licencia otorgada |
|---|---|
| Coche | `drive` |
| Moto | `drive_bike` |
| Camion | `drive_truck` |

La licencia se agrega automaticamente a traves de esx_license y es permanente.

## Reprobado

Al reprobar un examen practico:

- El vehiculo de examen se elimina.
- Debe pagar nuevamente para reintentar.
- No se impone tiempo de espera (a menos que se configure).

## Consejos

- Revise las preguntas antes de tomar el examen teorico.
- Conduzca con cuidado durante los examenes practicos.
- Cuidado con los peatones: atropellar a un peaton causa reprobado inmediato.
