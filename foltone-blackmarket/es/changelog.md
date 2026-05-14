---
title: "Changelog"
description: "Historial de cambios del script foltone_blackmarket"
script: "foltone-blackmarket"
section: "Blackmarket"
order: 4
version: "1.0.0"
---

# Changelog

## v1.0.0 — Lanzamiento inicial

### Anadido
- Van movil de armas ilegales con ciclo de spawn aleatorio
- Ubicaciones de spawn configurables (10 presets LS / campo)
- Soporte multi-framework (ESX / QBCore / QBox / standalone)
- Soporte multi-inventario (ox_inventory / qs-inventory / esx / qb)
- Soporte multi-target (ox_target / qb-target / qtarget) + fallback textUI
- Doble menu : RageUI (in-game) y NUI (HTML/CSS) elegible via `Config.MenuType`
- Preview 3D de los items con zoom de rueda
- Pestana de customizacion de armas (componentes + tints) para armas poseidas
- Preview en tiempo real al pasar por encima de un custom
- Selector de armas con flechas en la pestana customs
- Persistencia metadata ox_inventory (components + tint)
- Item telefono cifrado con sistema de blip de dos fases (busqueda 161 luego van 110)
- Sistema policia & heat (alertas, despawn automatico al umbral)
- Deteccion de policias cerca : el vendedor huye si hay policia cerca (radio 80m)
- Varianza de stock y precio por van (+/-30% / +/-10%)
- Gate de reputacion (opcional, hook `GetPlayerReputation`)
- Protecciones anti-cheat : check de distancia, cooldown, validacion source, transacciones atomicas
- Verificacion de posesion del arma en servidor para los customs
- Logging webhook de Discord en cada compra
- Comando admin `bm_van spawn/despawn/status`
- Soporte multi-idioma (fr / en / es)
- Verificacion de version automatica al inicio
