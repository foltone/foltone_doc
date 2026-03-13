---
title: "Instalación"
description: "Guía de instalación del script Props Storage"
script: "foltone-props-storage"
section: "foltone_props_storage"
order: 1
version: "1.0.0"
---

# Instalación — foltone_props_storage

## Requisitos

- **ESX Legacy** (v1.12.3 o superior)
- **oxmysql** — Librería MySQL
- **ox_lib** *(opcional)* — Para diálogos de entrada
- **ox_inventory** *(opcional)* — Sistema de inventario alternativo
- **ox_target** *(opcional)* — Necesario si usas ox_inventory

## Descarga

Descarga el script desde tu cuenta Tebex y coloca la carpeta en tu directorio `resources/`.

## Base de datos

Importa la tabla SQL en tu base de datos:

```sql
CREATE TABLE IF NOT EXISTS `props_inventory` (
  `id` INT PRIMARY KEY AUTO_INCREMENT,
  `owner` VARCHAR(255) NOT NULL,
  `inventory` JSON NOT NULL,
  `position` JSON NOT NULL,
  `prop` VARCHAR(100) NOT NULL,
  `pin` VARCHAR(10) NOT NULL,
  `bucket` INT DEFAULT NULL
);
```

## Configuración del servidor

Añade en tu `server.cfg`:

```ini
ensure ox_lib
ensure oxmysql
ensure es_extended
ensure foltone_props_storage
```

> **Importante**: `foltone_props_storage` debe iniciarse **después** de `es_extended` y `oxmysql`.

## Añadir items

Añade los items de caja fuerte en tu base de datos ESX:

```sql
INSERT INTO `items` (`name`, `label`, `weight`, `rare`, `can_remove`) VALUES
  ('big_safe', 'Caja Fuerte Grande', 5, 0, 1),
  ('safe', 'Caja Fuerte', 3, 0, 1);
```

Si usas **ox_inventory**, añade los items en `ox_inventory/data/items.lua`:

```lua
['big_safe'] = {
    label = 'Caja Fuerte Grande',
    weight = 5000,
    stack = false,
},
['safe'] = {
    label = 'Caja Fuerte',
    weight = 3000,
    stack = false,
},
```

## ox_lib (opcional)

Si quieres usar ox_lib para los diálogos de entrada, descomenta la línea en `fxmanifest.lua`:

```lua
shared_scripts {
    '@ox_lib/init.lua', -- descomenta esta línea
    "config.lua",
    "trad.lua",
    "locales/*.lua"
}
```

## Verificación

Después de reiniciar el servidor:

1. Date un item de caja fuerte: `/giveitem [id] big_safe 1`
2. Usa el item — la interfaz de colocación debería aparecer
3. Coloca la caja fuerte y establece un código PIN
4. Comprueba los logs en la consola del servidor

## Webhook de Discord

Para activar los logs de Discord, edita `server/sv_editable.lua` y reemplaza la URL del webhook:

```lua
PerformHttpRequest("https://discord.com/api/webhooks/TU_WEBHOOK_AQUI", ...)
```
