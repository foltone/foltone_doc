---
title: "Idiomas"
description: "Sistema de traducción de Ultra HUD"
script: "foltone-ultra-hud"
section: "Ultra HUD"
order: 5
version: "1.0.0"
---

# Idiomas — foltone_ultra_hud

El script incluye un sistema de traducción completo tanto para los mensajes del lado Lua como para el panel de administración NUI.

## Configurar el Idioma

En `config.lua`:

```lua
Config.locale = "en" -- "en", "fr", etc.
```

## Idiomas Disponibles

| Código | Idioma | Archivo |
|---|---|---|
| `en` | Inglés | `locales/en.lua` |
| `fr` | Francés | `locales/fr.lua` |

## Agregar un Nuevo Idioma

1. Copia `locales/en.lua` a `locales/xx.lua` (donde `xx` es tu código de idioma)
2. Traduce todos los valores (mantén las claves sin cambios)
3. Cambia la primera línea de `Locales["en"]` a `Locales["xx"]`
4. Establece `Config.locale = "xx"`

**Ejemplo — crear una traducción al alemán:**

```lua
-- locales/de.lua
Locales["de"] = {
    no_permission = "Du hast keine Berechtigung.",
    settings_saved = "Einstellungen gespeichert!",
    -- ... traduce todas las claves
}
```

## Usar Traducciones en Lua

La función `L()` está disponible globalmente (script compartido):

```lua
L("key")              -- Traducción simple
L("key", arg1, arg2)  -- Traducción con argumentos de string.format
```

Si una clave no existe en el idioma actual, se recurre al inglés. Si tampoco existe en inglés, se devuelve la propia clave.

## Claves de Traducción

El sistema de traducción cubre:

- **Mensajes del servidor**: errores de permisos, confirmaciones de guardado
- **Panel de administración**: todos los títulos de sección, etiquetas, opciones, botones
- **Ajustes de notificaciones**: nombres de posiciones
- **Notificaciones de prueba**: todos los mensajes de prueba

Todo el texto del panel de administración NUI usa atributos HTML `data-locale` que se reemplazan automáticamente cuando se aplica el idioma.
