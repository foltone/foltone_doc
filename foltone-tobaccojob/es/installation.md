---
title: "Instalacion"
description: "Guia de instalacion del script foltone_tobaccojob"
script: "foltone-tobaccojob"
section: "Tobacco Job"
order: 1
version: "1.0.0"
---

# Instalacion

## Requisitos previos

Antes de instalar `foltone_tobaccojob`, asegurese de que los siguientes recursos estan instalados y funcionando en su servidor:

- **es_extended** (ESX Framework)
- **oxmysql** (base de datos)
- **esx_addonaccount** (cuentas de sociedad)
- **esx_addoninventory** (inventario de sociedad)
- **esx_society** (gestion de sociedad)

## Pasos de instalacion

### 1. Transferencia de archivos

Coloque la carpeta `foltone_tobaccojob` en su directorio `resources/`:

```
resources/
  [esx]/
  [foltone]/
    foltone_tobaccojob/
      client/
      server/
      shared/
      fxmanifest.lua
```

### 2. Importacion SQL

Ejecute el archivo SQL proporcionado en su base de datos:

```sql
-- Importe el archivo install.sql incluido con el recurso
SOURCE install.sql;
```

Esto creara las tablas necesarias para la sociedad, cuentas e inventarios.

### 3. Configuracion del server.cfg

Agregue el recurso en su `server.cfg` **despues** de las dependencias:

```cfg
ensure es_extended
ensure oxmysql
ensure esx_addonaccount
ensure esx_addoninventory
ensure esx_society
ensure foltone_tobaccojob
```

### 4. Configuracion del empleo

Asegurese de que el empleo `tobaccojob` existe en las tablas `jobs` y `job_grades` de su base de datos. Se incluye un archivo SQL de ejemplo.

### 5. Configuracion de items

Agregue los items necesarios (hojas de tabaco, cigarrillos, etc.) a su tabla `items` si no fueron creados por el SQL de instalacion.

## Verificacion

1. Inicie su servidor
2. Conectese al juego
3. Verifique que el blip aparece en el mapa
4. Asignese el empleo mediante comando de administrador o base de datos

## Notas importantes

- Este script esta protegido por **escrow** (Tebex). No modifique los archivos protegidos.
- Los archivos de configuracion (`shared/`) se pueden modificar libremente.
- En caso de problemas, revise la consola del servidor para mensajes de error.
