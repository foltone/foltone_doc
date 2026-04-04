---
title: "Uso"
description: "Guia de uso del script foltone_ammunation"
script: "foltone-ammunation"
section: "Ammunation"
order: 3
version: "1.0.0"
---

# Uso

## Compra de armas

1. Dirijase a una tienda Ammu-Nation (icono en el mapa).
2. Acerquese al NPC vendedor.
3. Presione la tecla de interaccion para abrir el menu RageUI.
4. Navegue por los pasillos (pistolas, rifles, municiones, etc.).
5. Seleccione un articulo y confirme la compra.

### Licencia de armas

Algunas armas requieren una licencia. Si no tiene una:

- El menu le ofrecera comprar una licencia al precio configurado.
- Una vez obtenida, las armas restringidas estaran disponibles.
- La licencia es permanente (a menos que un administrador la revoque).

## Robo

### Requisitos

- Un numero minimo de policias debe estar en servicio (configurable).
- El tiempo de espera entre robos debe haber pasado.
- Debe estar cerca del NPC.

### Funcionamiento

1. Acerquese al NPC y seleccione la opcion de robo.
2. Aparecera una barra de progreso durante el robo.
3. Permanezca cerca del NPC -- alejarse cancela el robo.
4. No mate al NPC -- su muerte cancela el robo.
5. Una vez completado, recibira un monto aleatorio (dentro del rango configurado).

### Alertas

Durante un robo:
- Los policias en servicio reciben una alerta con su foto y la ubicacion de la tienda.
- Un blip temporal aparece en el mapa policial.

## Comandos

No se necesitan comandos. Toda la interaccion se realiza a traves del menu RageUI cerca del NPC.

## Permisos

| Accion | Requisito |
|---|---|
| Comprar armas libres | Ninguno |
| Comprar armas restringidas | Licencia de armas requerida |
| Robar la tienda | Cantidad minima de policias alcanzada |
