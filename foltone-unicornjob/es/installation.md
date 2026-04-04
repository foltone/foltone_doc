---
title: "Instalacion"
description: "Guia de instalacion del script foltone_unicornjob"
script: "foltone-unicornjob"
section: "Unicorn Job"
order: 1
version: "1.0.0"
---

# Instalacion

## Requisitos previos

Antes de instalar `foltone_unicornjob`, asegurese de que los siguientes recursos estan instalados y funcionando:

- **es_extended** (ESX Framework)
- **oxmysql** (base de datos)
- **esx_addonaccount** (cuentas de sociedad)
- **esx_addoninventory** (inventario de sociedad)
- **esx_society** (gestion de sociedad)

## Pasos de instalacion

### 1. Transferencia de archivos

Coloque la carpeta `foltone_unicornjob` en su directorio `resources/`:

```
resources/
  [esx]/
  [foltone]/
    foltone_unicornjob/
      client/
      server/
      shared/
      fxmanifest.lua
```

### 2. Importacion SQL

Ejecute el archivo SQL proporcionado en su base de datos:

```sql
SOURCE install.sql;
```

Esto creara las tablas para la sociedad Unicorn, cuentas e inventarios asociados.

### 3. Configuracion del server.cfg

Agregue el recurso en su `server.cfg` **despues** de las dependencias:

```cfg
ensure es_extended
ensure oxmysql
ensure esx_addonaccount
ensure esx_addoninventory
ensure esx_society
ensure foltone_unicornjob
```

### 4. Configuracion del empleo

Asegurese de que el empleo `unicorn` existe en las tablas `jobs` y `job_grades`. Se incluye un archivo SQL de ejemplo.

### 5. Configuracion de items

Agregue los items de bar (bebidas, cocteles, etc.) a su tabla `items` si no fueron creados por el SQL de instalacion.

## Verificacion

1. Inicie el servidor
2. Conectese al juego
3. Verifique el blip del Unicorn en el mapa
4. Asignese el empleo y pruebe el acceso al bar

## Notas importantes

- Script protegido por **escrow** (Tebex). Los archivos protegidos no se pueden modificar.
- Los archivos `shared/` son completamente configurables.
- Revise la consola del servidor si encuentra errores.
