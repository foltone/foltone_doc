---
title: "Utilizacion"
description: "Guia de uso del script foltone_gruppe6"
script: "foltone-gruppe6"
section: "Gruppe6"
order: 3
version: "1.0.0"
---

# Uso de foltone_gruppe6

## Sistema dual: Empleo + Robo

Este script ofrece dos mecanicas independientes segun el rol del jugador.

---

## Sistema de empleo (Empleados Gruppe6)

### Iniciar servicio

1. Vaya al punto de servicio con el trabajo `gruppe6`
2. Abra el menu RageUI
3. Seleccione **Iniciar servicio** para ponerse el uniforme

### Misiones

1. Una vez en servicio, acepte una mision desde el menu
2. Suba al vehiculo blindado en el punto indicado
3. Siga los puntos GPS para completar la entrega / recoleccion
4. Regrese al deposito para validar la mision y recibir su recompensa

### Finalizar servicio

Regrese al punto de servicio y seleccione **Finalizar servicio** para quitarse el uniforme.

---

## Sistema de robo (Criminales)

### Requisitos

- Un numero minimo de policias debe estar en servicio (configurable)
- El jugador debe tener el item explosivo en su inventario
- El tiempo de espera del ultimo robo debe haber pasado

### Procedimiento

1. Acerquese a la furgoneta blindada
2. Interactue para iniciar el robo
3. Use el explosivo en la puerta trasera de la furgoneta
4. Recoja el dinero del interior
5. Escape antes de que llegue la policia

### Notificaciones

- La policia recibe una alerta automatica cuando se inicia el robo
- Un temporizador de espera impide repetir el robo inmediatamente

---

## Comandos

No se necesitan comandos de servidor. Toda la interaccion se realiza a traves del menu RageUI y los puntos de interaccion en el juego.
