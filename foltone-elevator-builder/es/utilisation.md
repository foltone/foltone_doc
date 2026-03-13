---
title: "Uso"
description: "Guía de uso del script Elevator Builder"
script: "foltone-elevator-builder"
section: "foltone_elevator_builder"
order: 3
version: "1.1.0"
---

# Uso — foltone_elevator_builder

## Funcionamiento general

Elevator Builder permite crear y gestionar ascensores en el juego a través de una interfaz NUI. Los ascensores están compuestos por pisos con un nombre y una posición. Los jugadores pueden teletransportarse entre pisos usando un panel de ascensor interactivo.

## Menú de administración

### Abrir el menú

Escribe `/fab` en el chat para abrir el menú de administración NUI.

### Crear un ascensor

1. Abre el menú de administración (`/fab`)
2. Haz clic en **"Crear un ascensor"**
3. Define el **nombre del ascensor**
4. Elige el **número de pisos** (1 a 20)
5. Para cada piso:
   - Haz clic en **"Definir nombre"** e introduce el nombre (ej: "Planta Baja", "Piso 1", "Azotea")
   - Haz clic en **"Definir posición"** — el menú se cierra, tu posición actual se registra
6. Personaliza el **estilo del ascensor** (color de acento del panel, escala, lado, apariencia del marcador)
7. Haz clic en **"Crear el ascensor"** para confirmar

> Los marcadores de previsualización aparecen en verde durante la creación para verificar las posiciones.

### Editar un ascensor

1. Abre el menú de administración (`/fab`)
2. Haz clic en **"Editar un ascensor"**
3. Selecciona el ascensor a editar
4. Puedes:
   - **Renombrar el ascensor** — Haz clic en el botón de renombrar
   - **Editar un piso** — Selecciona el piso, luego modifica su nombre o posición
   - **Eliminar un piso** — Selecciona el piso, luego haz clic en "Eliminar"
   - **Eliminar el ascensor** — Elimina el ascensor y todos sus pisos

### Personalización del estilo del ascensor

Durante la creación o edición, puedes personalizar la apariencia de cada ascensor:

- **Color de acento del panel** (RGB) — el color de acento del panel NUI
- **Escala del panel** — tamaño del panel (0.7 a 1.3)
- **Lado del panel** — mostrar a la izquierda o derecha de la pantalla
- **Tipo, escala, color, opacidad del marcador** — apariencia de los marcadores de piso
- **Rebote/Rotación del marcador** — opciones de animación

Se muestra una vista previa en tiempo real mientras ajustas la configuración.

### Panel de configuración

Desde el menú de administración, accede al panel de configuración para modificar los ajustes globales en tiempo real:

- Color y tipo del marcador
- Distancias de renderizado e interacción
- Activación/desactivación de ox_target
- Animación de teletransporte (duración, fundido)
- Sonidos (activación, volumen)

Los cambios se aplican inmediatamente para todos los jugadores.

## Uso del jugador

### Sin ox_target (tecla E)

1. Acércate a un marcador de ascensor (distancia configurable, por defecto 3.5m)
2. El texto **"Pulse E para acceder al ascensor"** aparece
3. Presiona **E**
4. El panel de ascensor NUI se abre, mostrando el piso actual y los pisos disponibles
5. Haz clic en el piso deseado para teletransportarte

### Con ox_target

1. Apunta a un punto de ascensor con ox_target
2. Haz clic en la opción del ascensor
3. El panel se abre — selecciona tu piso

### Cerrar el panel

Presiona **Escape** o haz clic en el botón de cierre.

## Interfaz del panel de ascensor

El panel muestra:
- El **piso actual** en tiempo real (indicador digital)
- La **lista de pisos disponibles** con sus nombres
- **Botones** para cada piso

El indicador de piso se actualiza automáticamente cuando el jugador se mueve entre las posiciones de los pisos.

## Animación de teletransporte

Cuando la animación está activada, el proceso es:
1. Sonido de cierre de puertas
2. Fundido negro
3. Teletransporte + sonido de movimiento
4. Fundido claro + sonido de llegada (ding)
5. Sonido de apertura de puertas

## Almacenamiento de datos

Los ascensores se guardan en el archivo `json/data.json`. Este archivo es leído/escrito automáticamente por el servidor. Formato:

```json
[
    {
        "label": "Ascensor Principal",
        "floors": [
            { "idEtage": 1, "name": "Planta Baja", "position": { "x": 0.0, "y": 0.0, "z": 0.0 } },
            { "idEtage": 2, "name": "Piso 1", "position": { "x": 0.0, "y": 0.0, "z": 10.0 } }
        ],
        "style": {
            "panel_accent_r": 255,
            "panel_accent_g": 180,
            "panel_accent_b": 0,
            "panel_scale": 1,
            "panel_side": "right",
            "marker_type": 25,
            "marker_scale": 0.8,
            "marker_red": 114,
            "marker_green": 204,
            "marker_blue": 114,
            "marker_alpha": 180,
            "marker_bob": false,
            "marker_spin": true
        }
    }
]
```

Cada ascensor almacena su propio objeto `style` con la personalización del panel y del marcador. Si no se especifica, se utilizan los valores por defecto de `Config.lua`.

## Exports disponibles

El script expone exports para la integración con otros scripts:

### openElevator

Abre el panel de ascensor para un ascensor específico.

```lua
-- Abre el ascensor con ID 1
local success = exports['foltone-elevator-builder']:openElevator(1)
```

### teleportToFloor

Teletransporta directamente al jugador a un piso específico.

```lua
-- Teletransporta al piso 2 del ascensor 1
local success = exports['foltone-elevator-builder']:teleportToFloor(1, 2)
```

### getElevators

Obtiene la lista de todos los ascensores y sus pisos.

```lua
local elevators = exports['foltone-elevator-builder']:getElevators()
-- Retorna: { { id = 1, label = "...", floors = { { idEtage = 1, name = "Planta Baja" }, ... } }, ... }
```

### getCurrentFloor

Obtiene el nombre del piso más cercano al jugador.

```lua
local floorName = exports['foltone-elevator-builder']:getCurrentFloor()
-- Retorna: "Planta Baja" o nil si no hay piso cercano
```
