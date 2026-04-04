---
title: "Instalacion"
description: "Guia de instalacion del script foltone_baginventory"
script: "foltone-baginventory"
section: "Bag Inventory"
order: 1
version: "1.0.0"
---

# Instalacion

## Requisitos

- **ESX Framework** (es_extended)
- **oxmysql** (base de datos)
- **RageUI** (interfaz de menu)

## Pasos de instalacion

### 1. Descargar el script

Coloque la carpeta `foltone_baginventory` en su directorio `resources/[foltone]/`.

### 2. Importar la base de datos

Ejecute el archivo SQL proporcionado:

```sql
-- Importe el archivo sql/install.sql en su base de datos
```

Este archivo crea la tabla necesaria para almacenar el contenido de las bolsas colocadas en el suelo.

### 3. Agregar al server.cfg

```cfg
ensure foltone_baginventory
```

Asegurese de que las dependencias se inicien antes:

```cfg
ensure es_extended
ensure oxmysql
ensure RageUI
```

### 4. Agregar items de bolsa

Agregue los items de bolsa en la tabla `items` de su base de datos:

```sql
INSERT INTO `items` (`name`, `label`, `weight`) VALUES
('bag_small', 'Bolsa pequena', 2),
('bag_medium', 'Bolsa mediana', 3),
('bag_large', 'Bolsa grande', 5);
```

### 5. Configurar y reiniciar

Edite `config.lua` y luego reinicie el servidor.

## Estructura de archivos

```
foltone_baginventory/
├── client/
├── server/
├── config.lua
├── fxmanifest.lua
└── sql/
```
