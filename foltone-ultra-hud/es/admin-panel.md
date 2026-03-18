---
title: "Panel de Administración"
description: "Guía de uso del panel de administración de Ultra HUD"
script: "foltone-ultra-hud"
section: "Ultra HUD"
order: 4
version: "1.0.0"
---

# Panel de Administración — foltone_ultra_hud

El panel de administración proporciona una interfaz de configuración completa dentro del juego. Los cambios se aplican a **todos los jugadores** del servidor y persisten tras los reinicios.

## Abrir el Panel

Escribe el comando de administración en el chat (por defecto: `/hudadmin`). Necesitas permisos de administrador para acceder.

### Orden de Verificación de Permisos

1. **Grupo del framework** — ESX: `admin`, `superadmin`, `god` / QBCore: permiso `admin`, `god`
2. **Grupos personalizados** — Cualquier grupo listado en `Config.adminGroups`
3. **Respaldo ACE** — Permiso ACE `command.hudadmin`

## Secciones del Panel

### Colores

Cambia el color de cada elemento del HUD usando selectores de color:

- Texto, Salud, Armadura, Hambre, Sed, Resistencia, Apnea, Combustible

Los colores se aplican a barras, círculos, cuadrados, hexágonos y sus efectos de brillo.

### Visibilidad

Activa o desactiva elementos individuales del HUD:

- ID, Trabajo, Trabajo 2/Banda, Dinero, Banco, Dinero Sucio, Posición, Salud, Armadura, Hambre, Sed, Resistencia, Apnea, Velocímetro

### Pantalla

| Ajuste | Opciones | Descripción |
|---|---|---|
| Visualización de Necesidades | Barra, Círculo, Cuadrado, Hexágono, Texto | Forma de los indicadores de estado |
| Relleno de Forma | Trazo, Relleno | Trazo = progreso de contorno, Relleno = relleno sólido de abajo hacia arriba |
| Unidad de Velocidad | KM/H, MPH | Unidad del velocímetro |

### Tamaño

Deslizadores de escala para cada grupo del HUD (0.5x a 1.5x):

- Cartera, Posición, Estado, Velocímetro

### Notificaciones

| Ajuste | Rango | Descripción |
|---|---|---|
| Posición | 6 posiciones | Dónde aparecen las notificaciones en la pantalla |
| Ancho | 15-40 vw | Ancho del contenedor de notificaciones |
| Escala | 0.5-2.0 | Multiplicador de escala de notificaciones |

## Modo Vista Previa

Haz clic en **PREVIEW** para ver todos los elementos del HUD con datos de demostración mientras el panel permanece abierto. Haz clic en **EXIT PREVIEW** para volver.

## Modo Organizar

Haz clic en **ARRANGE** para entrar en el modo de arrastrar y soltar:

1. El panel de administración se cierra y todos los elementos del HUD se vuelven arrastrables
2. Arrastra los elementos para reposicionarlos en cualquier lugar de la pantalla
3. Haz clic en **SAVE POSITIONS** para guardar la disposición para todos los jugadores
4. Haz clic en **CANCEL** para descartar los cambios
5. Haz clic en **RESET DEFAULT** para restaurar las posiciones originales

## Guardar

Haz clic en **SAVE** para guardar todos los ajustes (colores, visibilidad, pantalla, tamaño, notificaciones) en `settings.json`. Los cambios se transmiten inmediatamente a todos los jugadores conectados.

> Los ajustes se almacenan en el servidor en `settings.json` dentro de la carpeta del recurso. Persisten tras los reinicios del servidor y se aplican a todos los jugadores.
