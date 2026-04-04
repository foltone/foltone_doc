---
title: "Instalacion"
description: "Guia de instalacion del script foltone_charactercreator"
script: "foltone-charactercreator"
section: "Character Creator"
order: 1
version: "1.0.0"
---

# Instalacion

## Requisitos

- **ESX Framework** (es_extended)
- **skinchanger** (gestion de apariencia)
- **RageUI** (interfaz de menu)

## Pasos de instalacion

### 1. Descargar el script

Coloque la carpeta `foltone_charactercreator` en su directorio `resources/[foltone]/`.

### 2. Agregar al server.cfg

```cfg
ensure foltone_charactercreator
```

Asegurese de que las dependencias se inicien antes:

```cfg
ensure es_extended
ensure skinchanger
ensure RageUI
```

### 3. Configurar el script

Edite el archivo `config.lua` segun sus necesidades (vea la seccion Configuracion).

### 4. Reiniciar el servidor

Reinicie su servidor o ejecute `refresh` y luego `ensure foltone_charactercreator` en la consola.

## Estructura de archivos

```
foltone_charactercreator/
├── client/
├── server/
├── config.lua
└── fxmanifest.lua
```

## Compatibilidad

Este script reemplaza el creador de personajes predeterminado de ESX. Asegurese de desactivar cualquier otro script de creacion de personajes para evitar conflictos.

## Problemas comunes

| Problema | Solucion |
|---|---|
| El menu no aparece | Verifique que RageUI este iniciado |
| Apariencia no guardada | Verifique que skinchanger funcione |
| Conflicto con otro script | Desactive otros creadores de personajes |
