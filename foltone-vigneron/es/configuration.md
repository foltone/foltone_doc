---
title: "Configuración"
description: "Configuración del script Vigneron"
script: "foltone-vigneron"
section: "Vigneron"
order: 2
version: "2.0.0"
---

# Configuración — foltone_vigneron

Toda la configuración está en `config.lua`.

## General

```lua
Config.JobName = 'vigne'
Config.SocietyName = 'society_vigne'
Config.MenuSystem = 'rageui'   -- 'rageui' o 'ox_lib'
Config.DiscordWebhook = ''
```

## Features

```lua
Config.Features = {
    boss = true, storage = true, locker = true, garage = true,
    processing = true, f6menu = true, bills = true, ads = true, duty = true,
}
```

## Multi-cofres

Múltiples cofres con permisos por grado y soporte opcional de ox_inventory stash.

## Pipeline de producción

| Tipo | Descripción |
|------|-------------|
| `harvest` | Recolectar un item |
| `transform` | Convertir items en otro |
| `sell` | Vender un item (dinero jugador + sociedad) |

## Discord Webhooks

Todas las acciones sensibles se registran cuando `Config.DiscordWebhook` está configurado.
