---
title: "Uso"
description: "Guia de uso de Foltone CCTV"
script: "foltone-cctv"
section: "Foltone CCTV"
order: 3
version: "1.1.0"
---

# Uso — foltone_cctv

## Descripcion general

Foltone CCTV es un sistema completo de camaras de vigilancia para FiveM. Los jugadores pueden comprar, colocar y gestionar camaras de seguridad con visualizacion en tiempo real, deteccion de movimiento, uso compartido por empleo y captura de pantalla. El script soporta 4 tipos de camara, cada uno con props, opticas y precios unicos.

## Comprar camaras

### Tienda

Interactua con el PED de la tienda en las posiciones configuradas para abrir la tienda de camaras.

La tienda muestra todos los tipos de camara disponibles en una cuadricula de tarjetas:
- **Imagen de la camara** y nombre del modelo
- **Descripcion** y especificaciones tecnicas (FOV, zoom, etc.)
- **Precio** y boton de compra

Cada tipo de camara otorga un objeto de inventario diferente al comprarse.

### Metodos de acceso

| Modo | Como interactuar |
|------|----------------|
| `ox_target` | Apunta al PED con el cursor de objetivo |
| `drawtext` | Acercate al PED y presiona **E** |
| `marker` | Entra en el marcador y presiona **E** |

## Colocar camaras

1. Usa el objeto de camara desde tu inventario
2. Aparece el **HUD de colocacion** (esquina inferior izquierda) con instrucciones:
   - **Clic izquierdo** — Colocar la camara
   - **Clic derecho** — Cancelar
   - **Scroll** — Rotar la camara
3. Apunta a una pared o superficie — la camara fantasma se ajusta a la normal de la superficie
4. El indicador de estado muestra **LISTO** (verde) o **MUY LEJOS** (rojo)
5. Haz clic para confirmar — aparece una entrada de nombre en el centro de la pantalla
6. Ingresa un nombre y presiona **OK** — la camara queda instalada

> Las camaras se orientan automaticamente contra la superficie de la pared. El offset de rotacion permite ajustar con precision el angulo de vision.

## Ver camaras

### Tablet

Usa el objeto `cctv_tablet` para abrir el panel de vigilancia. El jugador reproduce una animacion de sujecion de tablet con un prop.

### Terminales de ordenador

Interactua con las posiciones fijas de ordenadores para abrir el panel. El jugador reproduce una animacion de escritura.

### Estaciones de monitoreo

Las estaciones de monitoreo se pueden comprar en la tienda y colocar en el mundo usando el objeto. Tambien se pueden configurar en posiciones fijas en el config. Interactua con ellas para abrir el panel de camaras. Misma funcionalidad que las tablets.

## Panel de vigilancia

El panel tiene **4 pestanas**:

### Cuadricula

Muestra todas las camaras accesibles en una vista de cuadricula con:
- **Vista previa animada de ruido CCTV** por camara
- **Nombre de la camara** e insignias de estado (ACTIVA, MOVIMIENTO, EMPLEO, COMPARTIDA)
- **Indicador REC** y marca de tiempo en vivo
- **Boton VER** para entrar a la camara

### Gestion

Lista todas las camaras que posees con controles:
- **Deteccion de movimiento** interruptor (activado/desactivado)
- **Asignar a empleo** — comparte la camara con todos los jugadores de tu empleo actual
- **Renombrar** — cambiar el nombre para mostrar de la camara
- **Eliminar** — eliminar permanentemente la camara

### Compartir

Comparte tus camaras con jugadores especificos:
- Ingresa un **ID de servidor del jugador** para otorgar acceso
- **Revocar** acceso para cualquier jugador compartido
- Los jugadores compartidos pueden ver tus camaras pero no gestionarlas

### Capturas

Ver y gestionar capturas de pantalla tomadas desde las camaras:
- Vista previa en miniatura (si `screenshot-basic` esta configurado)
- Nombre de la camara y marca de tiempo de la captura
- Boton **Eliminar** para borrar capturas
- **Haz clic en una captura** para verla en pantalla completa en un lightbox con nombre de camara y fecha

## Vista de camara

Al ver una camara, la pantalla muestra una superposicion CCTV con efectos visuales:

### Controles

| Tecla | Accion |
|-------|--------|
| **Raton** | Rotar camara (panoramica/inclinacion) |
| **Scroll** | Acercar/alejar zoom |
| **N** | Activar/desactivar vision nocturna |
| **E** | Tomar una captura de pantalla |
| **Flechas izquierda/derecha** | Camara anterior/siguiente |
| **Retroceso** | Volver al panel de cuadricula |
| **Escape** | Salir de la vista de camara |

### Efectos visuales

La vista de camara incluye efectos configurables:
- **Modificador timecycle** — filtro de camara de seguridad de GTA (desaturacion, contraste)
- **Vineta** — bordes oscurecidos
- **Grano de pelicula** — superposicion de ruido animado
- **Linea de escaneo** — linea de escaneo horizontal en movimiento
- **Marcadores de esquina** — esquinas de enfoque
- **Aberracion cromatica** — sutil desplazamiento de color

> Todos los efectos son configurables en `Config.CameraEffect`. Establece cualquier valor en `0.0` para desactivarlo.

### Vision nocturna

Presiona **N** para activar la vision nocturna (vista amplificada con tinte verde). Presiona de nuevo para volver a la vista CCTV normal.

### Efectos de sonido

El sistema de camaras reproduce sonidos nativos de GTA para:
- Abrir/cerrar la vista de camara
- Acercar/alejar zoom
- Rotar la camara
- Cambiar entre camaras
- Tomar capturas de pantalla
- Activar/desactivar vision nocturna

## Grupos de empleo

Los propietarios de camaras pueden asignar camaras a su grupo de empleo:

1. Abre la pestana de **Gestion**
2. Haz clic en **ASIGNAR A EMPLEO** en una camara
3. La camara ahora es accesible para **todos los jugadores con el mismo empleo**
4. Una insignia amarilla **EMPLEO** aparece en las camaras compartidas en la cuadricula
5. Haz clic en la insignia de empleo nuevamente para hacer la camara **privada**

> Solo el propietario de la camara puede asignar/eliminar el grupo de empleo. Los miembros del empleo pueden ver pero no gestionar.

## Destruccion de camaras

Las camaras pueden ser destruidas disparandoles o golpeandolas con armas configuradas.

| Parametro | Efecto |
|-----------|--------|
| `Config.DestructionHits` | Numero de impactos necesarios (predeterminado: 3) |
| `Config.DestructionWeapons` | Lista de armas que causan dano |

Cuando se destruye:
- El prop de la camara se elimina para todos los jugadores
- La camara se elimina de la base de datos
- El propietario recibe una notificacion

## Deteccion de movimiento

Cuando esta activada en una camara:
- Detecta jugadores dentro del radio configurado
- Envia una notificacion al propietario con el nombre de la camara y la hora
- Tambien notifica a jugadores con acceso compartido
- Respeta el tiempo de espera entre alertas

## Agregar tipos de camara

Para agregar un nuevo tipo de camara:

1. Agrega una nueva entrada a `Config.CameraTypes` en `config.lua`
2. Crea el objeto de inventario correspondiente en tu sistema de inventario
3. Opcionalmente agrega una imagen PNG en `client/nui/img/<image>.png` (correspondiente al campo `image` del config)
4. Usa `/cctv_debug` en el juego para calibrar el offset de la camara

La tienda y el sistema de colocacion detectan automaticamente los nuevos tipos desde la configuracion.
