---
title: "Changelog"
description: "Historial de cambios del script foltone_blackmarket"
script: "foltone-blackmarket"
section: "Blackmarket"
order: 4
version: "1.1.0"
---

# Changelog

## v1.1.0 — Robustez i18n + correcciones

### Anadido
- Locales **aleman** (`de.lua`) y **espanol** (`es.lua`) completos
- Nuevas claves de traduccion : `rui_price_format`, `rui_price_stock_format`, `rui_component_suffix`, `rui_tint_suffix`, `rui_weapon_list_title`, `ui_html_title`, `ui_close_tooltip`, `ui_select_weapon` (reemplazan strings hardcodeados en RageUI y NUI)
- Soporte del atributo HTML `data-i18n-title` en el NUI (tooltips traducibles)
- `configuration.md` reescrita con **todas** las opciones Config : modos `MenuType` (nui/rageui), variantes `TargetSystem`, temas RageUI (`classic`/`modern`) con descripciones visuales, banners disponibles, opciones NUI Preview 3D, VanCustom, comportamiento de puertas, animaciones del ped, parametros del telefono (radios / jitter), categorias, etc.
- `version.json` consumido por el version check (`raw.githubusercontent.com/foltone/foltone_doc/main/foltone-blackmarket/version.json`)

### Corregido
- **NUI** : `RESOURCE_NAME` ahora resuelto via `GetParentResourceName()` → todos los callbacks JS↔Lua siguen funcionando si el owner del servidor renombra la carpeta del resource (sino menu inerte, /restart obligatorio para liberar el focus NUI)
- **NUI** : `state.customWeaponFilter` se resetea en cada apertura (evita referencia stale a un arma vendida/eliminada si `DefaultCategory = 'customs'`)
- **NUI** : guard `NUI.opening` contra doble apertura rapida (dos `getCatalog` en vuelo)
- **Servidor** : `getCatalog` ahora envia un payload locale **mergeado** (en como base + locale activa como override), asi una clave faltante en una locale parcial cae sobre el ingles en vez de mostrar la clave bruta en la UI
- **Servidor** : hot reload (`ensure foltone_blackmarket` con jugadores conectados) re-broadcastea estado a jugadores ya conectados
- **Servidor** : `BM_State.heat` se resetea en cada spawn (persistia entre ciclos de van)
- **Cliente** : timeout 30s + limpieza de callbacks servidor huerfanos en network drop, pcall alrededor del callback para mantener la cola sana
- **Cliente** : log consola una vez cuando `Config.Locale` apunta a una locale ausente, listando lo disponible
- **RageUI** : `fmtMoney` usa separador de miles (`$1,234,567`) como el NUI
- **Bridge** : `Bridge.HasItem` (ESX/QB) mas robusto cuando el player object falta
- **Version check** : movido a un endpoint JSON (`json.decode` nativo + fallback regex)

### Menor / seguridad
- `playerDropped` captura `source` en una variable local (buena practica)
- `applyCustomToOxInventory` : eliminado un retorno multi-valor sin uso

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
