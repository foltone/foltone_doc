---
title: "Utilizacion"
description: "Guia de utilizacion del script foltone_vehicleitem"
script: "foltone-vehicleitem"
section: "Vehicle Item"
order: 3
version: "1.0.0"
---

# Utilizacion

## Presentacion

El script Vehicle Item permite comprar vehiculos como items de inventario. Los jugadores pueden luego spawnar estos vehiculos desde su inventario y guardarlos en cualquier momento.

## Compra de un vehiculo

1. Dirijase a la tienda de vehiculos (marcada por un blip en el mapa si esta activado).
2. Interactue con el NPC vendedor para abrir el menu de compra (RageUI).
3. Explore la lista de vehiculos disponibles con sus precios.
4. Seleccione el vehiculo deseado.
5. Si tiene suficiente dinero, el vehiculo se agrega a su inventario como item.

## Uso de un vehiculo

### Sacar un vehiculo (spawn)

1. Abra su inventario.
2. Use el item del vehiculo (ej: "BMX").
3. El vehiculo aparece cerca de su personaje.
4. El item se retira de su inventario.

### Guardar un vehiculo (store)

1. Acerquese a su vehiculo spawneado.
2. Use la interaccion para guardar el vehiculo.
3. El vehiculo desaparece del mundo y vuelve a su inventario como item.

## Casos de uso tipicos

### Bicicletas y vehiculos pequenos

El sistema es ideal para bicicletas (BMX, Cruiser, Scorcher) que los jugadores quieren transportar facilmente.

### Vehiculos temporales

Permite dar vehiculos como recompensa en forma de items intercambiables entre jugadores.

### Comercio entre jugadores

Los items de vehiculos se pueden intercambiar o vender entre jugadores como cualquier otro item de inventario.

## Consejos

- Asegurese de tener suficiente espacio en su inventario antes de comprar.
- Solo se puede spawnar un vehiculo a la vez por item.
- Si se desconecta con un vehiculo spawneado, sera eliminado. Recuerde guardarlo antes.
- Los items de vehiculos son compatibles con los sistemas estandar de drop e intercambio.
