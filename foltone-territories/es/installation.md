---
title: "Instalacion"
description: "Guia de instalacion del script foltone_territories"
script: "foltone-territories"
section: "Territories"
order: 1
version: "1.0.0"
---

# Instalacion de foltone_territories

## Requisitos

- **ESX Framework** (es_extended)
- **oxmysql** para la base de datos
- **RageUI** (incluido o instalar por separado)

## Pasos de instalacion

### 1. Descargar el script

Coloque la carpeta `foltone_territories` en su directorio `resources/`.

### 2. Importar la base de datos

Ejecute el archivo SQL proporcionado para crear las tablas necesarias (territorios, progreso de captura, historial).

### 3. Configurar server.cfg

Agregue la siguiente linea a su `server.cfg`:

```cfg
ensure foltone_territories
```

### 4. Orden de inicio

```cfg
ensure es_extended
ensure oxmysql
ensure foltone_territories
```

### 5. Configurar las pandillas

Asegurese de que los trabajos de pandilla existan en su tabla `jobs` y coincidan con los configurados en el script.

## Verificacion

1. Reinicie su servidor
2. Asignese un trabajo de pandilla configurado
3. Vaya a una zona de territorio
4. Verifique que la zona se muestre correctamente en el mapa
5. Pruebe la venta de drogas a un PNJ en la zona
6. Verifique que los puntos de captura se incrementen
