---
title: "Configuracion"
description: "Guia de configuracion del script foltone_gruppe6"
script: "foltone-gruppe6"
section: "Gruppe6"
order: 2
version: "1.0.0"
---

# Configuracion de foltone_gruppe6

## Archivo de configuracion

Toda la configuracion se realiza en `config.lua` en la raiz del script.

## Parametros del empleo

### Grados del trabajo

```lua
Config.JobGrades = {
    { name = "recluta", label = "Recluta", salary = 200 },
    { name = "agente", label = "Agente", salary = 350 },
    { name = "jefe", label = "Jefe de equipo", salary = 500 },
    { name = "patron", label = "Patron", salary = 700 },
}
```

### Recompensas de mision

```lua
Config.MissionReward = {min = 500, max = 1500}
```

Defina el rango de recompensa por cada mision completada.

### Uniformes

```lua
Config.Outfits = {
    male = { ... },
    female = { ... },
}
```

Configure los componentes del uniforme (camiseta, torso, pantalon, zapatos, etc.) para cada genero.

### Vehiculo

```lua
Config.VehicleModel = "stockade"
```

Modelo del vehiculo blindado utilizado en las misiones.

## Parametros del robo

### Policia requerida

```lua
Config.Robbery = {
    requiredPolice = 2,
    cooldown = 1800, -- en segundos (30 minutos)
    explosiveItem = "explosive", -- item necesario
    rewardMin = 5000,
    rewardMax = 15000,
}
```

| Parametro | Descripcion |
|-----------|-------------|
| `requiredPolice` | Numero minimo de policias en servicio |
| `cooldown` | Tiempo de espera entre dos robos (segundos) |
| `explosiveItem` | Nombre del item explosivo requerido en el inventario |
| `rewardMin` / `rewardMax` | Rango de recompensa del robo |

## Traduccion

Los textos se encuentran en `locales/`. Agregue o modifique archivos para soportar otros idiomas.
