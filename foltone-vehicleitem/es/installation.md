---
title: "Instalacion"
description: "Guia de instalacion del script foltone_vehicleitem"
script: "foltone-vehicleitem"
section: "Vehicle Item"
order: 1
version: "1.0.0"
---

# Instalacion

## Requisitos previos

Antes de instalar `foltone_vehicleitem`, asegurese de que los siguientes recursos estan instalados:

- **es_extended** (ESX Framework)
- **oxmysql** (base de datos)

## Pasos de instalacion

### 1. Transferencia de archivos

Coloque la carpeta `foltone_vehicleitem` en su directorio `resources/`:

```
resources/
  [esx]/
  [foltone]/
    foltone_vehicleitem/
      client/
      server/
      shared/
      fxmanifest.lua
```

### 2. Importacion SQL

Ejecute el archivo SQL proporcionado para agregar los items de vehiculos a su base de datos:

```sql
SOURCE install.sql;
```

Esto agregara los items necesarios (ej: `bmx_item`, etc.) a su tabla `items`.

### 3. Configuracion del server.cfg

Agregue el recurso en su `server.cfg` **despues** de las dependencias:

```cfg
ensure es_extended
ensure oxmysql
ensure foltone_vehicleitem
```

### 4. Verificacion de items

Asegurese de que cada vehiculo configurado en el script tiene un item correspondiente en la tabla `items` de la base de datos.

## Verificacion

1. Inicie el servidor
2. Conectese al juego
3. Verifique que la tienda es accesible (si esta configurada)
4. Pruebe la compra y el spawn de un vehiculo desde el inventario

## Notas importantes

- Este script **no** requiere esx_society ni esx_addonaccount.
- Los archivos de configuracion (`shared/`) se pueden modificar libremente.
- El script es compatible con los inventarios estandar de ESX.
