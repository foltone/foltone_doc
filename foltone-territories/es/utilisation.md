---
title: "Utilizacion"
description: "Guia de uso del script foltone_territories"
script: "foltone-territories"
section: "Territories"
order: 3
version: "1.0.0"
---

# Uso de foltone_territories

## Presentacion

Este script permite a las pandillas capturar territorios vendiendo drogas a los PNJ. Los territorios capturados ofrecen mejores precios de venta. Los PNJ pueden aceptar, rechazar o llamar a la policia.

---

## Sistema de captura

### Como capturar un territorio

1. Tenga un trabajo de pandilla configurado
2. Vaya a una zona de territorio (visible en el mapa)
3. Acerquese a un PNJ en la zona
4. Abra el menu RageUI para venderle droga
5. Cada venta exitosa otorga **puntos de captura**
6. Acumule suficientes puntos para capturar la zona

### Progresion

- Cada tipo de droga otorga una cantidad diferente de puntos
- Las drogas mas riesgosas otorgan mas puntos
- El progreso se guarda en la base de datos
- Cuando se alcanza el umbral, el territorio es capturado por su pandilla

---

## Reacciones de los PNJ

Cuando se acerca a un PNJ para vender, tres reacciones son posibles:

### Aceptar
El PNJ compra la droga. Usted recibe dinero y puntos de captura.

### Rechazar
El PNJ rechaza la transaccion. No pasa nada, conserva su droga.

### Llamar a la policia
El PNJ rechaza y **llama a la policia**. Las fuerzas del orden reciben una alerta con su posicion. Huya rapidamente.

Las probabilidades de cada reaccion son configurables por tipo de droga.

---

## Beneficios de los territorios capturados

- **Mejores precios**: Las drogas se venden mas caro en un territorio controlado por su pandilla
- **Control de zona**: Su pandilla domina visualmente la zona en el mapa

---

## Venta de drogas

1. Asegurese de tener drogas en su inventario
2. Acerquese a un PNJ (que no este en la lista negra)
3. Interactue a traves del menu RageUI
4. Seleccione la droga a vender
5. Espere la reaccion del PNJ

### PNJ excluidos

Ciertos PNJ (policias, etc.) no pueden ser objetivo. Estan definidos en la lista negra de la configuracion.

---

## Comandos

No se necesitan comandos. Toda la interaccion se realiza a traves del menu RageUI y las zonas definidas en el mapa.
