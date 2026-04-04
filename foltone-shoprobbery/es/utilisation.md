---
title: "Utilizacion"
description: "Guia de uso del script foltone_shoprobbery"
script: "foltone-shoprobbery"
section: "Shop Robbery"
order: 3
version: "1.0.0"
---

# Uso de foltone_shoprobbery

## Presentacion

Este script combina un sistema de tienda y un sistema de robo. Los jugadores pueden comprar articulos en las tiendas de conveniencia o robarlas para obtener dinero. Mismo sistema que la armeria pero adaptado para tiendas.

---

## Tienda (Compra de articulos)

### Comprar articulos

1. Vaya a una tienda de conveniencia
2. Acerquese al PNJ vendedor
3. Abra el menu RageUI
4. Navegue por los articulos disponibles
5. Seleccione y confirme su compra

Los articulos y sus precios son configurables en el archivo de configuracion.

---

## Robo

### Requisitos previos

- Un numero minimo de policias debe estar en servicio
- El tiempo de espera de la tienda debe haber pasado
- El PNJ vendedor debe estar vivo

### Procedimiento del robo

1. Acerquese al PNJ vendedor en una tienda de conveniencia
2. Seleccione la opcion de robo en el menu
3. Aparece una barra de progreso - **no se mueva**
4. Espere a que se complete la progresion para recoger el dinero

### Cancelacion automatica

El robo se **cancela inmediatamente** si:
- Se mueve durante la barra de progreso
- El PNJ vendedor muere (no lo mate)

### Alertas policiales

Cuando se activa un robo:
- Todos los policias en servicio reciben una alerta
- La alerta incluye una **foto del sospechoso**
- La alerta incluye la **geolocalizacion** de la tienda
- La posicion exacta se marca en el mapa de la policia

### Tiempo de espera

Despues de un robo exitoso, la tienda entra en cooldown. Ningun otro robo puede realizarse en esa tienda hasta que expire el temporizador.

---

## Comandos

No se necesitan comandos. Toda la interaccion se realiza a traves del menu RageUI y los puntos de interaccion.
