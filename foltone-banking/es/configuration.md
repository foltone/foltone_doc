---
title: "Configuracion"
description: "Guia de configuracion del script bancario"
script: "foltone-banking"
section: "Banking"
order: 2
version: "1.0.0"
---

# Configuracion — foltone_banking

Toda la configuracion se realiza en `config.lua` en la raiz del script.

## Idioma

```lua
Config.Locale = "fr" -- "fr" or "en"
```

Las traducciones se encuentran en la carpeta `locales/`. Puedes agregar tu propio idioma creando un nuevo archivo (por ejemplo, `locales/de.lua`) y configurando `Config.Locale = "de"`.

## Framework

```lua
Config.Framework = "esx" -- "esx", "qbcore" or "qbx"
```

| Valor | Framework |
|---|---|
| `"esx"` | ESX Legacy |
| `"qbcore"` | QBCore |
| `"qbx"` | QBX |

## Modo de Interaccion

```lua
Config.InteractionType = "drawtext" -- "marker", "ox_target", "qb-target", "qtarget", "drawtext"
```

| Valor | Descripcion |
|---|---|
| `"marker"` | Marcador en el suelo en posiciones de banco/cajero automatico |
| `"ox_target"` | Interaccion visual con ox_target |
| `"qb-target"` | Interaccion visual con qb-target |
| `"qtarget"` | Interaccion visual con qtarget |
| `"drawtext"` | Texto de ayuda en pantalla (por defecto) |

## Configuracion de IBAN y Cuenta

```lua
Config.IBANPrefix = "FB"
Config.DefaultPIN = "0000"
Config.StartingBalance = 0
```

| Parametro | Tipo | Descripcion |
|---|---|---|
| `IBANPrefix` | string | Prefijo para los IBAN generados (por ejemplo, `"FB"` produce `FB123456789`) |
| `DefaultPIN` | string | Codigo PIN por defecto asignado a las cuentas nuevas |
| `StartingBalance` | number | Saldo inicial para las cuentas recien creadas |

## Configuracion de Cajeros Automaticos

```lua
Config.ATMs = {
    models = {"prop_atm_01", "prop_atm_02", "prop_atm_03", "prop_fleeca_atm"},
    features = {"deposit", "withdraw", "balance", "transfer", "history"},
    distance = 1.5,
    blip = false,
}
```

| Parametro | Tipo | Descripcion |
|---|---|---|
| `models` | table | Lista de nombres de modelos de props de cajeros automaticos a detectar |
| `features` | table | Funciones habilitadas en los cajeros automaticos |
| `distance` | number | Distancia de interaccion (en unidades del juego) |
| `blip` | boolean/table | `false` para desactivar, o una tabla con `sprite`, `color`, `scale`, `label` |

> **Nota**: Las cuentas conjuntas, ahorros y criptomonedas **no estan disponibles** en cajeros automaticos (solo en bancos).

## Configuracion del Banco

```lua
Config.Banks = {
    ped = { model = "s_m_m_bankman_01", scenario = "WORLD_HUMAN_CLIPBOARD" },
    features = {"deposit", "withdraw", "balance", "transfer", "history", "card", "pin"},
    distance = 2.0,
    blip = { sprite = 108, color = 2, scale = 0.8, label = "Banque" },
    positions = {
        { pos = vector3(149.0, -1040.0, 29.4), heading = 336.0 },
        { pos = vector3(314.2, -278.7, 54.2), heading = 336.0 },
        { pos = vector3(-351.5, -49.5, 49.0), heading = 336.0 },
        { pos = vector3(-1212.9, -330.1, 37.8), heading = 336.0 },
        { pos = vector3(-2962.5, 482.6, 15.7), heading = 336.0 },
        { pos = vector3(1175.0, 2706.8, 38.1), heading = 336.0 },
    },
}
```

| Parametro | Tipo | Descripcion |
|---|---|---|
| `ped.model` | string | Nombre del modelo hash del PED para el empleado bancario |
| `ped.scenario` | string | Escenario de animacion del PED |
| `features` | table | Funciones habilitadas en los bancos (superconjunto de las funciones del cajero) |
| `distance` | number | Distancia de interaccion |
| `blip` | table/false | Configuracion del blip en el mapa o `false` para desactivar |
| `blip.sprite` | number | ID del sprite del blip |
| `blip.color` | number | ID del color del blip |
| `blip.scale` | number | Escala del blip |
| `blip.label` | string | Etiqueta del blip en el mapa |
| `positions` | table | Array de ubicaciones bancarias con `pos` (vector3) y `heading` (number) |

## Sistema de Tarjetas

```lua
Config.CardSystem = {
    useItem = false,
    cardItem = "bank_card",
    reissuePrice = 500,
    pinChangePrice = 100,
}
```

| Parametro | Tipo | Descripcion |
|---|---|---|
| `useItem` | boolean | `true` = la tarjeta es un objeto fisico de ox_inventory, `false` = tarjeta virtual |
| `cardItem` | string | Nombre del objeto en ox_inventory (solo se usa si `useItem = true`) |
| `reissuePrice` | number | Costo para reemitir una tarjeta perdida/bloqueada |
| `pinChangePrice` | number | Costo para cambiar el codigo PIN |

## Configuracion de Transferencias

```lua
Config.Transfer = {
    allowByServerId = true,
    allowByIBAN = true,
    offlineTransfer = true,
}
```

| Parametro | Tipo | Descripcion |
|---|---|---|
| `allowByServerId` | boolean | Permitir transferencias ingresando el ID de servidor del destinatario |
| `allowByIBAN` | boolean | Permitir transferencias ingresando el IBAN del destinatario |
| `offlineTransfer` | boolean | Permitir transferencias a jugadores desconectados (resuelto por IBAN) |

## Historial de Transacciones

```lua
Config.History = {
    perPage = 50,
}
```

| Parametro | Tipo | Descripcion |
|---|---|---|
| `perPage` | number | Numero de transacciones mostradas por pagina en la vista de historial |

## Tema

```lua
Config.theme = {}
```

El tema por defecto es la **Blue Edition** (Sistema de Diseno Cyber Street). La tabla `theme` esta vacia por defecto, lo que aplica el esquema de colores azul incorporado. Puedes personalizar variables CSS especificas agregando pares clave-valor a esta tabla.

> **Nota**: El sistema de diseno utiliza acentos en azul electrico, fondos de panel oscuros y tres familias tipograficas (Bebas Neue, Rajdhani, JetBrains Mono). No uses colores dorado, naranja, morado o cian.

## Notificaciones

```lua
Config.Notification = function(message)
    SetNotificationTextEntry("STRING")
    AddTextComponentString(message)
    DrawNotification(false, false)
end
```

Reemplaza esta funcion con tu sistema de notificaciones preferido (por ejemplo, okokNotify, ox_lib, etc.). Esta es una funcion del lado del cliente.

## Texto en Pantalla

```lua
Config.DisplayText = function(text)
    SetTextComponentFormat("STRING")
    AddTextComponentString(text)
    DisplayHelpTextFromStringLabel(0, 0, 1, -1)
end
```

Personaliza la visualizacion del texto de ayuda que se muestra cuando el jugador esta cerca de un punto de interaccion (usado con el modo de interaccion `"drawtext"`).

## Configuracion de Sociedad / Cuenta de Trabajo

```lua
Config.Society = {
    defaultGrades = {"boss", "manager"},
    jobs = {
        -- Configuracion por trabajo:
        -- ["police"] = { grades = {"boss", "lieutenant"} },
    },
    features = {"balance", "deposit", "withdraw", "transfer", "payroll", "history"},
    positions = {
        -- { job = "police", pos = vector3(440.0, -981.0, 30.7), heading = 0.0 },
    },
    distance = 2.0,
    ped = { model = "s_m_m_accountant_01", scenario = "WORLD_HUMAN_CLIPBOARD" },
    blip = false,
}
```

| Parametro | Tipo | Descripcion |
|---|---|---|
| `defaultGrades` | table | Lista de nombres de grado que tienen acceso a la banca de sociedad por defecto |
| `jobs` | table | Configuracion por trabajo para grados permitidos (clave = nombre del trabajo, valor = tabla con `grades`) |
| `features` | table | Funciones de sociedad habilitadas |
| `positions` | table | Posiciones de PED para puntos de acceso de sociedad, cada uno con `job`, `pos`, `heading` |
| `distance` | number | Distancia de interaccion para el PED de sociedad |
| `ped.model` | string | Modelo del PED para el contador de sociedad |
| `ped.scenario` | string | Escenario de animacion del PED |
| `blip` | table/false | Configuracion del blip en el mapa o `false` para desactivar |

### Funciones

| Funcion | Descripcion |
|---|---|
| `"balance"` | Ver el saldo de la cuenta de sociedad |
| `"deposit"` | Depositar efectivo personal en la cuenta de sociedad |
| `"withdraw"` | Retirar de la cuenta de sociedad a efectivo personal |
| `"transfer"` | Transferir de la cuenta de sociedad a una cuenta personal (por ID de servidor o IBAN) |
| `"payroll"` | Pagar a un empleado desde la cuenta de sociedad |
| `"history"` | Ver el historial de transacciones de sociedad |

### Configuracion de Grados por Trabajo

```lua
Config.Society.jobs = {
    ["police"] = { grades = {"boss", "lieutenant"} },
    ["ambulance"] = { grades = {"boss"} },
}
```

> Si un trabajo no esta listado en `jobs`, se utiliza la lista `defaultGrades`.

## Puntuacion Crediticia

```lua
Config.CreditScore = {
    default = 500,
    min = 0,
    max = 1000,
    rewards = {
        deposit = 2,
        withdraw = -1,
        transfer_out = 1,
        transfer_in = 1,
        upgrade = 5,
    },
}
```

| Parametro | Tipo | Descripcion |
|---|---|---|
| `default` | number | Puntuacion crediticia inicial para cuentas nuevas |
| `min` | number | Puntuacion minima posible |
| `max` | number | Puntuacion maxima posible |
| `rewards` | table | Cambio de puntuacion por tipo de operacion (positivo = aumento, negativo = disminucion) |

### Acciones de Recompensa

| Accion | Por defecto | Descripcion |
|---|---|---|
| `deposit` | +2 | Realizar un deposito |
| `withdraw` | -1 | Realizar un retiro |
| `transfer_out` | +1 | Enviar una transferencia |
| `transfer_in` | +1 | Recibir una transferencia |
| `upgrade` | +5 | Mejorar el nivel de cuenta |

## Niveles de Cuenta

```lua
Config.AccountLevels = {
    standard = {
        label = "Standard",
        interestRate = 0.5,
        interestCap = 5000,
        transferMax = 50000,
        taxReduction = 0,
    },
    premium = {
        label = "Premium",
        interestRate = 1.5,
        interestCap = 20000,
        transferMax = 200000,
        taxReduction = 25,
        upgradePrice = 50000,
        minCreditScore = 700,
    },
}
```

### Nivel Standard

| Parametro | Tipo | Descripcion |
|---|---|---|
| `label` | string | Nombre para mostrar |
| `interestRate` | number | Tasa de interes por ciclo cron (%) |
| `interestCap` | number | Interes maximo ganado por periodo de reinicio |
| `transferMax` | number | Monto maximo de transferencia |
| `taxReduction` | number | Porcentaje de reduccion de impuestos (0 = ninguno) |

### Nivel Premium

| Parametro | Tipo | Descripcion |
|---|---|---|
| `label` | string | Nombre para mostrar |
| `interestRate` | number | Tasa de interes por ciclo cron (%) |
| `interestCap` | number | Interes maximo ganado por periodo de reinicio |
| `transferMax` | number | Monto maximo de transferencia |
| `taxReduction` | number | Porcentaje de reduccion de impuestos (25% = 25% menos impuestos) |
| `upgradePrice` | number | Costo para mejorar de Standard a Premium |
| `minCreditScore` | number | Puntuacion crediticia minima requerida para mejorar |

## Sistema de Intereses

```lua
Config.Interest = {
    interval = 60,
    resetPeriod = 1440,
}
```

| Parametro | Tipo | Descripcion |
|---|---|---|
| `interval` | number | Minutos entre cada ciclo cron de intereses |
| `resetPeriod` | number | Minutos antes de que se reinicie el limite de intereses (1440 = 24 horas) |

> Los intereses solo se calculan para jugadores **en linea**. La tasa real esta modulada por la puntuacion crediticia del jugador y limitada por su nivel de cuenta.

## Tributacion Progresiva

```lua
Config.Tax = {
    deposit = {
        { from = 0, to = 10000, rate = 0 },
        { from = 10000, to = 50000, rate = 2 },
        { from = 50000, to = 0, rate = 5 },
    },
    withdraw = {
        { from = 0, to = 10000, rate = 0 },
        { from = 10000, to = 50000, rate = 1 },
        { from = 50000, to = 0, rate = 3 },
    },
    transfer = {
        { from = 0, to = 10000, rate = 0 },
        { from = 10000, to = 50000, rate = 1.5 },
        { from = 50000, to = 0, rate = 4 },
    },
}
```

Cada tipo de operacion (`deposit`, `withdraw`, `transfer`) tiene su propio conjunto de tramos fiscales.

| Parametro | Tipo | Descripcion |
|---|---|---|
| `from` | number | Monto de inicio del tramo (inclusivo) |
| `to` | number | Monto de fin del tramo (exclusivo). `0` significa ilimitado (ultimo tramo) |
| `rate` | number | Tasa impositiva en porcentaje para este tramo |

### Como Funcionan los Tramos

Los impuestos se calculan **progresivamente** a traves de los tramos. Por ejemplo, un deposito de $30,000 con la configuracion por defecto:

- $0 a $10,000: 0% de impuesto = $0
- $10,000 a $30,000: 2% de impuesto = $400
- **Impuesto total: $400**

> **Importante**: Los tramos deben ser contiguos y estar ordenados. Las operaciones de sociedad, cuentas conjuntas, ahorros y criptomonedas estan **exentas** de tributacion. Las cuentas Premium reciben una reduccion de impuestos del 25%.

## Configuracion de Cuentas Conjuntas

```lua
Config.JointAccount = {
    enabled = true,
    maxMembers = 4,
    maxAccountsPerPlayer = 2,
    transferMax = 50000,
    features = {"deposit", "withdraw", "transfer", "history"},
}
```

| Parametro | Tipo | Descripcion |
|---|---|---|
| `enabled` | boolean | Habilitar o deshabilitar cuentas conjuntas |
| `maxMembers` | number | Numero maximo de miembros por cuenta conjunta |
| `maxAccountsPerPlayer` | number | Numero maximo de cuentas conjuntas en las que un jugador puede participar |
| `transferMax` | number | Monto maximo de transferencia desde una cuenta conjunta |
| `features` | table | Funciones habilitadas para cuentas conjuntas |

> Las cuentas conjuntas solo son accesibles en **bancos** (no en cajeros automaticos). Estan exentas de tributacion, intereses y cambios de puntuacion crediticia.

## Notificaciones por Telefono

```lua
Config.PhoneNotifications = {
    enabled = true,
    resource = "lb_phone",
    events = {
        transfer_received = true,
        society_payroll_received = true,
        interest_credited = true,
        joint_deposit = true,
        joint_withdraw = true,
        joint_transfer = true,
        joint_member_added = true,
        joint_member_left = true,
    },
    appTitle = "Fleeca Bank",
    appIcon = "bank",
}
```

| Parametro | Tipo | Descripcion |
|---|---|---|
| `enabled` | boolean | Habilitar o deshabilitar notificaciones por telefono |
| `resource` | string | Nombre del recurso del telefono: `"lb_phone"`, `"qs-smartphone"`, o `"gksphone"` |
| `events` | table | Activar/desactivar eventos de notificacion individuales |
| `appTitle` | string | Nombre de la aplicacion mostrado en la notificacion del telefono |
| `appIcon` | string | Nombre del icono mostrado en la notificacion del telefono |

### Eventos de Notificacion

| Evento | Descripcion |
|---|---|
| `transfer_received` | Cuando el jugador recibe una transferencia personal |
| `society_payroll_received` | Cuando el jugador recibe un pago de nomina |
| `interest_credited` | Cuando se acreditan intereses a la cuenta |
| `joint_deposit` | Cuando un miembro deposita en una cuenta conjunta compartida |
| `joint_withdraw` | Cuando un miembro retira de una cuenta conjunta compartida |
| `joint_transfer` | Cuando un miembro realiza una transferencia desde una cuenta conjunta compartida |
| `joint_member_added` | Cuando se agrega un nuevo miembro a una cuenta conjunta |
| `joint_member_left` | Cuando un miembro abandona una cuenta conjunta |

> Las notificaciones por telefono solo se envian a jugadores **en linea**.

## Webhook de Discord

```lua
Config.Webhook = {
    enabled = true,
    url = "",
    botName = "Fleeca Bank",
    color = 3899126,
}
```

| Parametro | Tipo | Descripcion |
|---|---|---|
| `enabled` | boolean | Habilitar o deshabilitar el registro mediante webhook de Discord |
| `url` | string | URL del webhook de Discord (dejar vacio para desactivar) |
| `botName` | string | Nombre del bot mostrado en los embeds de Discord |
| `color` | number | Color del embed en decimal (3899126 = azul #3b82f6) |

> Todas las operaciones bancarias (personales, de sociedad, conjuntas, ahorros, criptomonedas) se registran en el webhook. El webhook utiliza un enfoque de enviar y olvidar.

## Cuenta de Ahorro

```lua
Config.Savings = {
    enabled = true,
    interestRate = 3.0,
    interestCap = 50000,
    maxWithdrawalsPerDay = 1,
    minLockAmount = 1000,
    locks = {
        { days = 3,  rate = 2.0,  label = "3 jours"  },
        { days = 7,  rate = 5.0,  label = "7 jours"  },
        { days = 14, rate = 12.0, label = "14 jours" },
        { days = 30, rate = 30.0, label = "30 jours" },
    },
}
```

| Parametro | Tipo | Descripcion |
|---|---|---|
| `enabled` | boolean | Habilitar o deshabilitar cuentas de ahorro |
| `interestRate` | number | Tasa de interes clasica del ahorro (% por ciclo cron) |
| `interestCap` | number | Interes maximo ganado por periodo de reinicio |
| `maxWithdrawalsPerDay` | number | Numero maximo de retiros del ahorro por periodo de 24 horas |
| `minLockAmount` | number | Monto minimo requerido para crear un deposito a plazo fijo |

### Opciones de Deposito a Plazo Fijo

| Parametro | Tipo | Descripcion |
|---|---|---|
| `days` | number | Duracion del bloqueo en dias |
| `rate` | number | Tasa de interes aplicada al vencimiento (%) |
| `label` | string | Etiqueta de visualizacion en la interfaz |

> Las cuentas de ahorro tienen un cron de intereses separado de la cuenta corriente principal. Los intereses son solo para jugadores en linea con un limite configurable.

## Trading de Criptomonedas

```lua
Config.Crypto = {
    enabled = true,
    apiSource = "binance",
    refreshInterval = 5,
    coins = {
        { id = "bitcoin",  symbol = "BTC", label = "Bitcoin"  },
        { id = "ethereum", symbol = "ETH", label = "Ethereum" },
        { id = "litecoin", symbol = "LTC", label = "Litecoin" },
    },
    currency = "usd",
    minTradeAmount = 100,
    historyPerPage = 50,
}
```

| Parametro | Tipo | Descripcion |
|---|---|---|
| `enabled` | boolean | Habilitar o deshabilitar el trading de criptomonedas |
| `apiSource` | string | Fuente de la API de precios: `"binance"`, `"coincap"`, o `"coinpaprika"` |
| `refreshInterval` | number | Minutos entre cada consulta de precios a la API |
| `coins` | table | Lista de criptomonedas negociables |
| `currency` | string | Moneda de referencia para precios (por ejemplo, `"usd"`) |
| `minTradeAmount` | number | Monto minimo de operacion en dolares |
| `historyPerPage` | number | Numero de operaciones mostradas por pagina en el historial |

### Configuracion de Monedas

| Parametro | Tipo | Descripcion |
|---|---|---|
| `id` | string | Identificador de la moneda usado por la API (por ejemplo, `"bitcoin"`) |
| `symbol` | string | Simbolo ticker mostrado en la interfaz (por ejemplo, `"BTC"`) |
| `label` | string | Nombre completo para mostrar (por ejemplo, `"Bitcoin"`) |

> Los precios se obtienen del lado del servidor mediante `sv_crypto_prices.lua` y se transmiten a todos los clientes conectados. El servidor mantiene una cache para minimizar las llamadas a la API. Las operaciones con criptomonedas estan exentas de tributacion.
