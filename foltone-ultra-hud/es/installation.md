---
title: "Instalación"
description: "Guía de instalación de Ultra HUD"
script: "foltone-ultra-hud"
section: "Ultra HUD"
order: 1
version: "1.0.0"
---

# Instalación — foltone_ultra_hud

## Requisitos

- **ESX Legacy** o **QBCore** o **QBX** o **Standalone** — Framework (detección automática)

> No se requiere base de datos. Los ajustes se almacenan en un archivo JSON.

## Descarga

Descarga el script desde tu cuenta de [Tebex](https://foltone.tebex.io/) y coloca la carpeta `foltone_ultra_hud` en tu directorio `resources/`.

## Configuración del Servidor

Agrega a tu `server.cfg`:

```ini
ensure es_extended       # o qb-core / qbx_core (opcional para standalone)
ensure foltone_ultra_hud
```

> **Importante**: `foltone_ultra_hud` debe iniciarse **después** de tu framework. Si usas standalone, no se necesita dependencia de framework.

## Framework

El script **detecta automáticamente** tu framework al iniciar. No se necesita configuración manual.

| Framework | Detección | Fuente de Hambre/Sed |
|---|---|---|
| ESX Legacy | `es_extended` iniciado | `esx_status` |
| QBCore | `qb-core` iniciado | `PlayerData.metadata` |
| QBX | `qbx_core` iniciado | `PlayerData.metadata` |
| Standalone | Ningún framework encontrado | Devuelve `100, 100` |

El framework detectado se muestra en la consola del servidor:

```
[foltone_ultra_hud] Framework detected: esx
```

## Verificación

Después de reiniciar tu servidor:

1. Conéctate al servidor con un personaje
2. El HUD debería aparecer automáticamente con todas las barras de estado, información de cartera y posición
3. Prueba el comando de administración (por defecto: `/hudadmin`) para abrir el panel de configuración
4. Prueba `/testnotif all` para probar todos los tipos de notificación

> Si el HUD no aparece, revisa la consola del servidor (F8) y la consola del cliente en busca de errores. Asegúrate de que tu framework se inicie antes que `foltone_ultra_hud`.
