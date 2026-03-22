---
title: "Registro de cambios"
description: "Registro de cambios de Foltone CCTV"
script: "foltone-cctv"
section: "Foltone CCTV"
order: 99
version: "1.1.0"
---

# Registro de cambios — foltone_cctv

## 1.1.0 — 2026-03-22

### Adiciones
- Accesorios de tienda: tablet y estacion de monitoreo disponibles para compra
- La estacion de monitoreo es ahora un objeto colocable (como las camaras) que abre la interfaz al interactuar
- Lightbox de capturas: haz clic en una captura para verla en pantalla completa con nombre de camara y fecha
- Parametros de offset `propPitch` y `propRoll` para correccion de rotacion de props
- Campos `wallOffset` e `image` en la configuracion de tipos de camara
- Seccion `Config.ShopAccessories` para accesorios de tienda

### Cambios
- Tipos de camara actualizados: 4 tipos (Standard, Bullet, Mini Bullet, Shop Cam) reemplazando los 5 anteriores
- Las imagenes de la tienda ahora usan archivos PNG desde el campo `image` del config en lugar de SVG
- Sistema de notificaciones refactorizado: `ClientNotification` en config.lua (lado cliente, personalizable) + el servidor dispara evento cliente
- SQL getCameras optimizado: reemplazo de consultas N+1 por una sola subconsulta IN
- install.sql actualizado con tabla de estaciones, todas las columnas e indices
- Tiempo de espera entre compras reducido
- Todas las cadenas de UI traducidas al ingles

### Correcciones
- Corregido requestCapture que no validaba propiedad/acceso a la camara
- Corregido destroyCamera que permitia abuso remoto (agregada verificacion de distancia)
- Corregida vulnerabilidad XSS: reemplazo de onclick inline por data-attributes + event delegation
- Corregida fuga de memoria motionCooldowns al eliminar camaras
- Corregidas entradas de acceso no limpiadas al eliminar una camara
- Corregidas migraciones ALTER TABLE usando async en lugar de await
- Corregido desajuste CAM_TYPE_ICONS (eliminados dome/ptz, agregado shop_cam)
- Corregida alineacion icono+texto de botones en toda la interfaz
- Corregida compra del monitor en tienda que otorgaba el objeto incorrecto
- Corregido error de contenido mixto HTTPS de screenshot-basic
- Comando cctv_debug movido detras de verificacion de permisos de admin

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
