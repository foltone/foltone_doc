---
title: "Uso"
description: "Guia de uso de Foltone Garage"
script: "foltone-garage"
section: "Foltone Garage"
order: 3
version: "2.0.0"
---

# Uso — foltone_garage

## Resumen

Foltone Garage es un sistema completo de garaje para FiveM. Permite a los jugadores almacenar y recuperar sus vehiculos, gestionar vehiculos incautados y asignar etiquetas personalizadas. El script soporta coches, barcos, aviones y helicopteros, con un sistema de deposito con precios dinamicos.

## Acceder a un garaje

La interfaz se abre al interactuar con el PED administrador del garaje ubicado en las coordenadas configuradas en `config_garage.lua`.

El metodo de interaccion depende de `Config.InteractionType`:

| Modo | Como interactuar |
|------|----------------|
| `ox_target` / `qb-target` / `interact` | Apunta al PED con el cursor del target |
| `drawtext` | Acercate al PED y presiona **E** |
| `marker` | Entra en el marcador y presiona **E** |

## Modo NUI (panel HTML)

El panel NUI tiene **4 pestanas**:

### Pestana Vehiculos

Muestra todos los vehiculos almacenados en el garaje actual.

Para cada vehiculo:
- **Modelo** y **etiqueta** (si se definio)
- **Matricula**
- **Estado** (disponible, fuera, incautado)
- **Boton Recuperar** — genera el vehiculo en la posicion de aparicion configurada

> Solo se muestran los vehiculos que coinciden con el tipo de garaje (coches, barcos, aviones o helicopteros).

### Pestana Almacenar

Permite almacenar el vehiculo que se esta conduciendo actualmente.

1. Conduce el vehiculo cerca de la zona de almacenamiento (`storeVeh`)
2. Abre la interfaz del garaje
3. Haz clic en **Almacenar**
4. El vehiculo desaparece y se marca como almacenado en la BD

> La distancia de almacenamiento es configurable por garaje (`distanceStore`).

#### Vehiculos de servicio

Para garajes de trabajo con `serviceVehicles` definidos, la pestana Almacenar tambien lista vehiculos de servicio que pueden generarse directamente.

### Pestana Deposito

Muestra los vehiculos del jugador que estan actualmente en el deposito.

Para cada vehiculo incautado:
- **Matricula** y **modelo**
- **Precio de recuperacion** calculado dinamicamente segun el tiempo transcurrido
- **Boton Recuperar** — deduce el monto y genera el vehiculo

#### Calculo del precio

```
Precio = basePrice + (horas_transcurridas × pricePerHour)
Precio = max(minPrice, min(maxPrice, Precio))
```

Ejemplo con la configuracion predeterminada (basePrice 500, pricePerHour 100):
- Despues de 2h: 500 + 200 = **$700**
- Despues de 10h: 500 + 1000 = **$1500** (limitado por maxPrice si se excede)

### Pestana Etiqueta

> Disponible solo en el modo `Config.MenuType = "nui"`.

Permite asignar un nombre personalizado a uno de los vehiculos del jugador.

1. Selecciona un vehiculo de la lista
2. Escribe la etiqueta deseada (maximo 30 caracteres)
3. Haz clic en **Guardar**

La etiqueta reemplaza el nombre del modelo en la pestana Vehiculos.

---

## Modo RageUI (menu clasico)

El modo RageUI proporciona **3 submenus** accesibles desde un menu principal:

| Submenu | Equivalente NUI |
|----------|---------------|
| Vehiculos | Pestana Vehiculos |
| Almacenar | Pestana Almacenar |
| Deposito | Pestana Deposito |

> Las etiquetas personalizadas de vehiculos no estan disponibles en el modo RageUI.

---

## Garajes de trabajo

Los garajes con `job`, `job2` o `annyJob` definidos estan restringidos a jugadores con el trabajo correspondiente.

| Parametro | Comportamiento |
|-----------|---------|
| `job = "ambulance"` | Acceso exclusivo para jugadores con el trabajo `ambulance` |
| `job2 = "famillies"` | Acceso a traves de la banda / trabajo secundario `famillies` |
| `annyJob = "police"` | Acceso para cualquier grado del trabajo `police` |

Los vehiculos de servicio (si estan configurados) solo son accesibles para miembros del trabajo.

---

## Sistema de deposito

Los vehiculos pueden ser incautados manualmente por un administrador o mediante otros scripts compatibles.

Un jugador puede recuperar su vehiculo desde cualquier deposito del tipo correcto (coche, barco, avion o helicoptero).

El precio aumenta automaticamente con el tiempo. Una vez pagado, el vehiculo queda disponible y aparece en la posicion de aparicion configurada del deposito.

---

## Tipos de vehiculo

| Tipo | Descripcion |
|------|-------------|
| `car` | Coches, motocicletas y vehiculos terrestres |
| `boat` | Barcos y embarcaciones |
| `plane` | Aviones y jets |
| `heli` | Helicopteros |

Cada tipo tiene su propia lista de garajes y depositos configurados en `config_garage.lua`.
