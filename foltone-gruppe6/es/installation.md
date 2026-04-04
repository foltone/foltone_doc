---
title: "Instalacion"
description: "Guia de instalacion del script foltone_gruppe6"
script: "foltone-gruppe6"
section: "Gruppe6"
order: 1
version: "1.0.0"
---

# Instalacion de foltone_gruppe6

## Requisitos

- **ESX Framework** (es_extended)
- **oxmysql** para la base de datos
- **RageUI** (incluido o instalar por separado)

## Pasos de instalacion

### 1. Descargar el script

Coloque la carpeta `foltone_gruppe6` en su directorio `resources/`.

### 2. Importar la base de datos

Ejecute el archivo SQL proporcionado en su base de datos:

```sql
-- Importe el archivo SQL incluido con el script
-- Contiene las tablas necesarias para el empleo y el robo
```

### 3. Agregar el trabajo a la base de datos

Asegurese de que el trabajo `gruppe6` exista en su tabla `jobs` con los grados configurados.

### 4. Configurar server.cfg

Agregue la siguiente linea a su `server.cfg`:

```cfg
ensure foltone_gruppe6
```

### 5. Orden de inicio

El script debe iniciarse **despues** de los siguientes recursos:

```cfg
ensure es_extended
ensure oxmysql
ensure foltone_gruppe6
```

## Verificacion

1. Reinicie su servidor
2. Conectese y asignese el trabajo `gruppe6`
3. Vaya al punto de servicio para verificar que el menu RageUI se abra correctamente
4. Revise los logs del servidor en busca de errores
