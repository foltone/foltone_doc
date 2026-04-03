---
title: "Instalación"
description: "Instalación del script Vigneron"
script: "foltone-vigneron"
section: "Vigneron"
order: 1
version: "2.0.0"
---

# Instalación — foltone_vigneron

## Requisitos

- **ESX Legacy** — Framework del servidor
- **ox_lib** — Notificaciones, inputs, barras de progreso
- **oxmysql** — Librería MySQL
- **skinchanger** — Vestuario / uniformes
- **esx_society** — Gestión de sociedad

### Opcionales

- **ox_inventory** — Cofres stash (fallback a esx_addoninventory)
- **ox_target** — Interacciones 3D (fallback a markers + tecla E)
- **esx_billing** — Facturación

## Configuración del servidor

```ini
ensure oxmysql
ensure es_extended
ensure ox_lib
ensure esx_society
ensure skinchanger
ensure foltone_vigneron
```

## Base de datos

Con **esx_addoninventory**: ejecute `foltone_vigneron.sql`. Con **ox_inventory**: los stash se crean automáticamente.

## Verificación

1. Conéctese con un personaje con el trabajo `vigne`
2. Verifique el blip "Vigneron" en el mapa
3. Consola: `[Foltone Vigneron] v2.0.0 chargee`
