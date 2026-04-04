---
title: "Instalacion"
description: "Guia de instalacion del script foltone_ammunation"
script: "foltone-ammunation"
section: "Ammunation"
order: 1
version: "1.0.0"
---

# Instalacion

## Requisitos

- **ESX Framework** (es_extended)
- **oxmysql** (base de datos)
- **esx_license** (sistema de licencias)
- **RageUI** (interfaz de menu)

## Pasos de instalacion

### 1. Descargar el script

Coloque la carpeta `foltone_ammunation` en su directorio `resources/[foltone]/`.

### 2. Importar la base de datos

Ejecute el archivo SQL proporcionado en su base de datos:

```sql
-- Importe el archivo sql/install.sql en su base de datos
```

### 3. Agregar al server.cfg

```cfg
ensure foltone_ammunation
```

Asegurese de que las dependencias se inicien **antes** de este script:

```cfg
ensure es_extended
ensure oxmysql
ensure esx_license
ensure RageUI
```

### 4. Configurar el script

Edite el archivo `config.lua` segun sus necesidades (vea la seccion Configuracion).

### 5. Reiniciar el servidor

Reinicie su servidor o ejecute `refresh` y luego `ensure foltone_ammunation` en la consola.

## Estructura de archivos

```
foltone_ammunation/
├── client/
├── server/
├── config.lua
├── fxmanifest.lua
└── sql/
```

## Problemas comunes

| Problema | Solucion |
|---|---|
| El menu no se abre | Verifique que RageUI este iniciado |
| Licencia no detectada | Verifique que esx_license funcione |
| El robo no inicia | Verifique la cantidad minima de policias |
