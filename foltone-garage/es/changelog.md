---
title: "Registro de cambios"
description: "Historial de versiones de Foltone Garage"
script: "foltone-garage"
section: "Foltone Garage"
order: 99
version: "2.0.0"
---

# Registro de cambios

## v2.0.0 — 2026-03-16

### Agregado
- Reescritura completa del script (arquitectura, seguridad, diseno)
- Nuevo panel NUI con 4 pestanas (vehiculos, almacenar, deposito, etiqueta)
- Modo alternativo RageUI configurable via `Config.MenuType`
- Soporte multi-target: ox_target, qb-target, interact, drawtext, marker
- Sistema de deposito con precios dinamicos (basePrice + pricePerHour, limite min/max)
- Etiquetas personalizadas de vehiculos (exclusivo NUI, maximo 30 caracteres)
- Vehiculos de servicio para garajes de trabajo (lista de modelos generables)
- Soporte nativo de QBX junto con ESX y QBCore
- Sistema seguro de callbacks personalizados (`RegisterServerFoltoneGRCallback`)
- Limitacion de frecuencia en todos los eventos del servidor
- Validacion del lado del servidor en todas las operaciones

### Cambiado
- Configuracion del garaje movida a `config_garage.lua` (separacion de configuracion y logica)
- Precio del deposito calculado del lado del servidor (previene manipulacion del lado del cliente)
- Vehiculos organizados por tipo (car, boat, plane, heli) con activacion individual
