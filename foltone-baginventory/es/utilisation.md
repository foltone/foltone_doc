---
title: "Uso"
description: "Guia de uso del script foltone_baginventory"
script: "foltone-baginventory"
section: "Bag Inventory"
order: 3
version: "1.0.0"
---

# Uso

## Descripcion general

El sistema de bolsas permite a los jugadores transportar objetos adicionales en bolsas que pueden colocar en el suelo, llenar y recoger.

## Usar una bolsa

### Desplegar una bolsa

1. Abra su inventario y use un item de bolsa (ej: "Bolsa pequena").
2. La bolsa se despliega y aparece en su espalda o manos.
3. Ahora puede almacenar objetos dentro.

### Abrir el menu de la bolsa

1. Presione la tecla de interaccion cuando la bolsa este equipada.
2. El menu RageUI muestra el contenido de la bolsa.
3. Puede agregar o retirar objetos y armas.

### Colocar una bolsa en el suelo

1. Abra el menu de la bolsa.
2. Seleccione la opcion "Colocar en el suelo".
3. La bolsa aparece en el suelo en su posicion como un objeto 3D.
4. Otros jugadores pueden interactuar con la bolsa colocada.

### Recoger una bolsa

1. Acerquese a una bolsa colocada en el suelo.
2. Presione la tecla de interaccion.
3. La bolsa y su contenido se agregan a su inventario.

### Doblar una bolsa

Si esta habilitado en la configuracion:

1. Abra el menu de la bolsa.
2. Seleccione "Doblar bolsa".
3. La bolsa se guarda en su inventario como un item normal.

## Comportamiento al morir

Si `Config.DropOnDeath` esta activado:

- Todas sus bolsas (o solo la equipada) caen al suelo al morir.
- Cualquier jugador puede recoger estas bolsas.
- El contenido se conserva.

## Limites

- Cada bolsa tiene un peso y numero de espacios maximo.
- El numero de bolsas por jugador es limitado (configurable).
- Una bolsa no puede contener otra bolsa.
