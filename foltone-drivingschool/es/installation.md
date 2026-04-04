---
title: "Instalacion"
description: "Guia de instalacion del script foltone_drivingschool"
script: "foltone-drivingschool"
section: "Driving School"
order: 1
version: "1.0.0"
---

# Instalacion

## Requisitos

- **ESX Framework** (es_extended)
- **esx_license** (sistema de licencias)

## Pasos de instalacion

### 1. Descargar el script

Coloque la carpeta `foltone_drivingschool` en su directorio `resources/[foltone]/`.

### 2. Agregar tipos de licencia

Asegurese de que los siguientes tipos de licencia existan en esx_license:

- `drive` - Licencia de coche
- `drive_bike` - Licencia de moto
- `drive_truck` - Licencia de camion

### 3. Agregar al server.cfg

```cfg
ensure foltone_drivingschool
```

Asegurese de que las dependencias se inicien antes:

```cfg
ensure es_extended
ensure esx_license
```

### 4. Configurar el script

Edite el archivo `config.lua` para personalizar las preguntas, rutas y vehiculos (vea la seccion Configuracion).

### 5. Reiniciar el servidor

Reinicie su servidor o ejecute `refresh` y luego `ensure foltone_drivingschool` en la consola.

## Estructura de archivos

```
foltone_drivingschool/
├── client/
├── server/
├── html/          -- Interfaz NUI para el examen teorico
│   ├── index.html
│   ├── style.css
│   └── script.js
├── config.lua
└── fxmanifest.lua
```

## Problemas comunes

| Problema | Solucion |
|---|---|
| La interfaz NUI no aparece | Verifique los archivos en la carpeta html/ |
| Licencia no otorgada | Verifique que esx_license funcione |
| El vehiculo de examen no aparece | Verifique los modelos de vehiculos en la config |
