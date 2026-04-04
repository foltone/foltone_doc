---
title: "Instalacion"
description: "Guia de instalacion del script foltone_shoprobbery"
script: "foltone-shoprobbery"
section: "Shop Robbery"
order: 1
version: "1.0.0"
---

# Instalacion de foltone_shoprobbery

## Requisitos

- **ESX Framework** (es_extended)
- **oxmysql** para la base de datos
- **RageUI** (incluido o instalar por separado)

## Pasos de instalacion

### 1. Descargar el script

Coloque la carpeta `foltone_shoprobbery` en su directorio `resources/`.

### 2. Importar la base de datos

Ejecute el archivo SQL proporcionado para crear las tablas necesarias (cooldowns, registros de robos).

### 3. Configurar server.cfg

Agregue la siguiente linea a su `server.cfg`:

```cfg
ensure foltone_shoprobbery
```

### 4. Orden de inicio

```cfg
ensure es_extended
ensure oxmysql
ensure foltone_shoprobbery
```

### 5. Configurar notificaciones policiales

Adapte las funciones de notificacion en el config para que coincidan con su sistema de despacho (telefono, MDT, etc.).

## Verificacion

1. Reinicie su servidor
2. Vaya a una tienda de conveniencia
3. Verifique que el menu de tienda funcione (compra de articulos)
4. Pruebe el robo con el numero requerido de policias en servicio
5. Verifique que las alertas policiales se envien correctamente
