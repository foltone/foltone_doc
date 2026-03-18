---
title: "Registro de cambios"
description: "Registro de cambios de Foltone CCTV"
script: "foltone-cctv"
section: "Foltone CCTV"
order: 99
version: "1.0.0"
---

# Registro de cambios — foltone_cctv

## 1.0.0 — 2026-03-18

- Lanzamiento inicial
- 5 tipos de camara: Standard, Dome, Bullet, Mini Bullet, PTZ Pro
- Tienda de camaras con interfaz de tarjetas en cuadricula, precios por tipo e imagenes SVG
- Sistema de colocacion con ajuste a paredes usando normales de superficie
- Vista de camara con rotacion por raton, zoom con scroll y atajos de teclado
- Efectos visuales CCTV: filtro timecycle, vineta, grano, lineas de escaneo, marcadores de esquina
- Intensidad de efectos configurable mediante Config.CameraEffect
- Activacion de vision nocturna (tecla N)
- Captura de pantalla mediante screenshot-basic
- Deteccion de movimiento con radio y tiempo de espera configurables
- Destruccion de camaras por disparos/golpes (impactos y armas configurables)
- Sistema de grupos de trabajo: asigna camaras a un empleo para acceso compartido
- Compartir individualmente mediante ID de servidor del jugador
- Objeto tablet con animacion de sujecion y prop
- Objeto estacion de monitoreo con prop_cctv_unit_01
- Terminales de ordenador fijos
- Efectos de sonido para todas las acciones de camara
- Herramienta de depuracion de camaras (/cctv_debug) para calibracion de offsets
- Soporte multi-framework: ESX, QBCore, QBX
- Soporte multi-idioma: Ingles, Frances
- Migracion automatica de base de datos al iniciar
- Endurecimiento de maquina de estados: todos los estados de la interfaz correctamente protegidos
