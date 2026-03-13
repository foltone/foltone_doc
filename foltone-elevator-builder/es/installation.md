---
title: "Instalación"
description: "Guía de instalación del script Elevator Builder"
script: "foltone-elevator-builder"
section: "foltone_elevator_builder"
order: 1
version: "1.1.0"
---

# Instalación — foltone_elevator_builder

## Requisitos

- **FiveM** con **Lua 5.4**
- **ox_target** *(opcional)* — Para interacción por objetivo en lugar de la tecla E

## Descarga

Descarga el script desde tu cuenta Tebex y coloca la carpeta en tu directorio `resources/`.

## Configuración del servidor

Añade en tu `server.cfg`:

```ini
ensure foltone-elevator-builder
```

> **Nota**: Este script es **standalone** — no requiere ningún framework (ESX, QBCore, etc.). Los datos se guardan en el archivo `json/data.json`.

## Sin base de datos necesaria

A diferencia de otros scripts, Elevator Builder **no usa una base de datos SQL**. Todos los datos de los ascensores se almacenan en el archivo `json/data.json` en formato JSON.

## Comando de administración

El script registra el comando `/fab` para abrir el menú de administración de ascensores. Puedes modificar este comando en `client/cl_editable.lua`:

```lua
RegisterCommand("fab", function(source, args)
    TriggerEvent("foltone_ascenseur:open_menu")
end)
```

> **Importante**: Recuerda restringir el acceso a este comando mediante tu sistema de permisos ACE para evitar que todos los jugadores puedan crear ascensores.

## ox_target (opcional)

Si deseas usar ox_target para la interacción:

1. Asegúrate de que `ox_target` esté ejecutándose en tu servidor
2. Activa la opción en `Config.lua`:

```lua
Config.use_target = true
```

El script detecta automáticamente la presencia de ox_target. Si `use_target` está activado pero ox_target no está instalado, el script usa automáticamente la tecla E como alternativa.

## Verificación

Después de reiniciar el servidor:

1. Escribe `/fab` en el chat
2. La interfaz de administración NUI debería abrirse
3. Crea un ascensor con 2 pisos para probar
4. Los marcadores deberían aparecer en las posiciones definidas
