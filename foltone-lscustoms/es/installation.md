---
title: "Instalacion"
description: "Guia de instalacion del script foltone_lscustoms"
script: "foltone-lscustoms"
section: "LS Customs"
order: 1
version: "1.0.0"
---

# Instalacion de foltone_lscustoms

## Requisitos

- **ESX Framework** (es_extended)
- **oxmysql** para la base de datos
- **RageUI** (incluido o instalar por separado)

## Pasos de instalacion

### 1. Descargar el script

Coloque la carpeta `foltone_lscustoms` en su directorio `resources/`.

### 2. Importar la base de datos

Ejecute el archivo SQL proporcionado para crear las tablas necesarias (facturas, registros de modificaciones, etc.).

### 3. Configurar server.cfg

Agregue la siguiente linea a su `server.cfg`:

```cfg
ensure foltone_lscustoms
```

### 4. Orden de inicio

```cfg
ensure es_extended
ensure oxmysql
ensure foltone_lscustoms
```

### 5. Desactivar scripts de mecanico por defecto

Si utiliza otro script de mecanico (version con empleo), asegurese de que no haya conflictos. Este script es **standalone** y no requiere ningun empleo.

## Verificacion

1. Reinicie su servidor
2. Vaya a un punto LS Customs en el mapa
3. Entre en la zona con un vehiculo
4. Verifique que el menu RageUI se abra y que la vista previa en vivo funcione
5. Pruebe una mision de remolque NPC
