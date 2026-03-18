---
title: "Exports y Eventos"
description: "Referencia de la API de Ultra HUD para desarrolladores"
script: "foltone-ultra-hud"
section: "Ultra HUD"
order: 3
version: "1.0.0"
---

# Exports y Eventos — foltone_ultra_hud

## Exports del Cliente

### Notify

Envía una notificación simple (sin imagen).

```lua
exports.foltone_ultra_hud:Notify(message, type, duration)
```

| Parámetro | Tipo | Requerido | Descripción |
|---|---|---|---|
| `message` | string | sí | Texto de la notificación |
| `type` | string | no | `"success"`, `"error"`, `"warning"`, `"info"` (por defecto: neutral) |
| `duration` | number | no | Duración en ms (por defecto: 5000) |

**Ejemplo:**

```lua
exports.foltone_ultra_hud:Notify("Has recibido $500", "success")
exports.foltone_ultra_hud:Notify("Acceso denegado", "error", 3000)
```

### AdvancedNotify

Envía una notificación con imagen (estilo GTA).

```lua
exports.foltone_ultra_hud:AdvancedNotify(image, title, message, subtitle, duration)
```

| Parámetro | Tipo | Requerido | Descripción |
|---|---|---|---|
| `image` | string | sí | URL o ruta de la imagen |
| `title` | string | sí | Texto del título en negrita |
| `message` | string | sí | Cuerpo del mensaje |
| `subtitle` | string | no | Subtítulo más pequeño debajo del título |
| `duration` | number | no | Duración en ms (por defecto: 5000) |

**Ejemplo:**

```lua
exports.foltone_ultra_hud:AdvancedNotify(
    "https://i.imgur.com/example.png",
    "LESTER CREST",
    "Tengo un trabajo para ti. Ven a verme.",
    "Nueva misión",
    7000
)
```

### ShowHud / HideHud

Mostrar u ocultar el HUD completo.

```lua
exports.foltone_ultra_hud:ShowHud()
exports.foltone_ultra_hud:HideHud()
```

**Ejemplo:**

```lua
-- Ocultar el HUD durante una cinemática
exports.foltone_ultra_hud:HideHud()
Wait(5000)
exports.foltone_ultra_hud:ShowHud()
```

## Eventos del Cliente

### foltone_ultra_hud:notify

Notificación simple a través de evento (utilizable desde el cliente o disparado desde el servidor).

```lua
-- Lado del cliente
TriggerEvent("foltone_ultra_hud:notify", message, type, duration)

-- Lado del servidor (a un jugador específico)
TriggerClientEvent("foltone_ultra_hud:notify", source, message, type, duration)

-- Lado del servidor (a todos los jugadores)
TriggerClientEvent("foltone_ultra_hud:notify", -1, message, type, duration)
```

### foltone_ultra_hud:advancedNotify

Notificación avanzada a través de evento.

```lua
-- Lado del cliente
TriggerEvent("foltone_ultra_hud:advancedNotify", image, title, message, subtitle, duration)

-- Lado del servidor
TriggerClientEvent("foltone_ultra_hud:advancedNotify", source, image, title, message, subtitle, duration)
```

### foltone_ultra_hud:enableHud / foltone_ultra_hud:disableHud

Mostrar u ocultar el HUD a través de eventos (útil para control del lado del servidor).

```lua
-- Lado del servidor: ocultar HUD para un jugador
TriggerClientEvent("foltone_ultra_hud:disableHud", source)

-- Lado del servidor: mostrar HUD para un jugador
TriggerClientEvent("foltone_ultra_hud:enableHud", source)
```

## Tipos de Notificación

| Tipo | Color | Icono | Caso de uso |
|---|---|---|---|
| *(ninguno)* | Blanco | Ninguno | Mensajes generales |
| `"success"` | Verde | Marca de verificación | Confirmaciones, acciones completadas |
| `"error"` | Rojo | Cruz | Errores, acciones denegadas |
| `"warning"` | Amarillo | Triángulo | Advertencias, avisos importantes |
| `"info"` | Azul | Círculo de información | Mensajes informativos |

## Comando de Prueba

Usa `/testnotif` para probar las notificaciones en el juego:

```
/testnotif all       -- Enviar todos los tipos de notificación
/testnotif simple    -- Notificación neutral
/testnotif success   -- Notificación de éxito
/testnotif error     -- Notificación de error
/testnotif warning   -- Notificación de advertencia
/testnotif info      -- Notificación informativa
/testnotif advanced  -- Notificación avanzada con imagen
```
