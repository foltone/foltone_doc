---
title: "Uso"
description: "Guia de uso del script bancario"
script: "foltone-banking"
section: "Banking"
order: 3
version: "1.0.0"
---

# Uso — foltone_banking

## Descripcion General

Foltone Banking es un script bancario completo para FiveM con una interfaz NUI moderna (diseno Blue Edition). Proporciona cuentas personales, cuentas de sociedad, cuentas conjuntas, ahorros, trading de criptomonedas, puntuacion crediticia, tributacion progresiva y mas.

## Acceso a la Interfaz Bancaria

Hay tres formas de acceder a la interfaz bancaria:

| Punto de Acceso | Ubicacion | Funciones Disponibles |
|---|---|---|
| **PED del Banco** | Posiciones bancarias configuradas (sucursales Fleeca) | Todas las funciones (personal, sociedad, conjunta, ahorros, criptomonedas) |
| **Cajero Automatico** | Cualquier prop de cajero automatico en el mundo del juego | Solo funciones personales (deposito, retiro, transferencia, historial) |
| **PED de Sociedad** | Posiciones de trabajo configuradas | Solo funciones de sociedad |

El metodo de interaccion depende de `Config.InteractionType`:

- **marker** — Camina hacia el marcador y presiona E
- **drawtext** — Acercate y presiona E cuando aparezca el texto de ayuda
- **ox_target / qb-target / qtarget** — Usa el sistema de objetivo/vision en el PED o cajero automatico

## Panel Principal

El panel principal es la pagina que se muestra cuando se abre la interfaz. Muestra:

- **Saldo** — Saldo actual de la cuenta corriente
- **IBAN** — Tu identificador unico de cuenta (por ejemplo, `FB123456789`)
- **Grafico de Evolucion del Saldo** — Grafico visual de tu saldo a lo largo del tiempo
- **Puntuacion Crediticia** — Barra de puntuacion de 0 a 1000 con el valor actual
- **Nivel de Cuenta** — Insignia Standard o Premium con opcion de mejora
- **Deposito** — Depositar efectivo en tu cuenta (con vista previa de impuestos en tiempo real)
- **Retiro** — Retirar dinero de tu cuenta (con vista previa de impuestos en tiempo real)

> La vista previa de impuestos se actualiza en tiempo real mientras escribes el monto, mostrando exactamente cuanto impuesto se aplicara segun los tramos progresivos y tu nivel de cuenta.

## Transferencias

La pagina de transferencias te permite enviar dinero a otros jugadores.

### Transferencia por ID de Servidor

1. Selecciona el modo **Server ID**
2. Ingresa el ID de servidor del destinatario
3. Ingresa el monto
4. Opcionalmente agrega una etiqueta/descripcion
5. Confirma la transferencia

### Transferencia por IBAN

1. Selecciona el modo **IBAN**
2. Ingresa el IBAN del destinatario (cuenta personal o conjunta)
3. El sistema resuelve el IBAN y muestra el nombre del destinatario
4. Ingresa el monto
5. Opcionalmente agrega una etiqueta/descripcion
6. Confirma la transferencia

> Las transferencias soportan tanto IBAN personales como IBAN de cuentas conjuntas. Las transferencias fuera de linea son posibles si `Config.Transfer.offlineTransfer` esta habilitado. Se muestra una vista previa de impuestos en tiempo real. El monto maximo de transferencia esta determinado por tu nivel de cuenta.

## Historial de Transacciones

La pagina de historial muestra todas las transacciones con paginacion.

### Filtros Disponibles

| Filtro | Muestra |
|---|---|
| Todos | Todas las transacciones |
| Deposito | Depositos |
| Retiro | Retiros |
| Transferencia Entrante | Transferencias recibidas |
| Transferencia Saliente | Transferencias enviadas |
| Interes | Creditos de intereses |
| Impuesto | Deducciones de impuestos |
| Mejora | Pagos de mejora de cuenta |

Cada entrada muestra el tipo, monto, saldo despues de la transaccion, fecha y una insignia indicando el tipo de operacion. La paginacion se controla con `Config.History.perPage`.

## Tarjeta Bancaria

La seccion de gestion de tarjetas esta disponible solo en bancos. Muestra:

- **Numero de Tarjeta** — Tu numero de tarjeta virtual de 16 digitos
- **Codigo PIN** — PIN actual (oculto por defecto)
- **Estado de la Tarjeta** — Activa o Bloqueada

### Acciones Disponibles

| Accion | Costo | Descripcion |
|---|---|---|
| **Bloquear / Desbloquear** | Gratis | Alternar el estado activo de la tarjeta |
| **Cambiar PIN** | Configurable (`pinChangePrice`) | Establecer un nuevo codigo PIN de 4 digitos |
| **Reemitir Tarjeta** | Configurable (`reissuePrice`) | Obtener un nuevo numero de tarjeta |

> Si `Config.CardSystem.useItem` esta habilitado, la tarjeta es un objeto fisico de ox_inventory.

## Cuentas de Sociedad

Las cuentas de sociedad (trabajo) son accesibles para jugadores con grados autorizados (configurados en `Config.Society.defaultGrades` o configuraciones por trabajo).

### Acceso

- Desde el **banco** o **cajero automatico**: aparece una pestana de sociedad en la barra lateral si el jugador tiene el grado requerido
- Desde un **PED de sociedad**: abre directamente la interfaz de sociedad (si las posiciones estan configuradas)

### Panel de Sociedad

Muestra el saldo de la cuenta de sociedad, el nombre del trabajo y el grado del jugador.

### Operaciones de Sociedad

| Operacion | Descripcion |
|---|---|
| **Deposito** | Transferir efectivo personal a la cuenta de sociedad |
| **Retiro** | Retirar de la cuenta de sociedad a efectivo personal |
| **Transferencia Externa** | Transferir de la cuenta de sociedad a una cuenta personal (por ID de servidor o IBAN) |
| **Nomina** | Pagar a un empleado en linea desde la cuenta de sociedad (ingresa su ID de servidor y monto) |

> Las operaciones de sociedad estan **exentas de tributacion**. El saldo es gestionado por el framework (esx_addonaccount o qb-banking).

### Historial de Sociedad

Historial de transacciones dedicado para la cuenta de sociedad. Cada entrada muestra el nombre del empleado, grado, tipo de operacion, monto y destino (para transferencias/nomina).

## Cuentas Conjuntas

Las cuentas conjuntas permiten que multiples jugadores compartan una cuenta bancaria. Estan disponibles solo en **bancos** (no en cajeros automaticos).

### Crear una Cuenta Conjunta

1. Navega a la seccion de Cuentas Conjuntas en la barra lateral
2. Haz clic en **Crear Cuenta Conjunta**
3. Se crea una nueva cuenta conjunta con un IBAN unico
4. Eres agregado automaticamente como el primer miembro

### Agregar Miembros

1. Abre la pagina de gestion de la cuenta conjunta
2. Ingresa el ID de servidor del jugador a agregar
3. Confirma — el jugador es agregado a la cuenta conjunta

### Operaciones de Cuenta Conjunta

| Operacion | Descripcion |
|---|---|
| **Deposito** | Depositar efectivo personal en la cuenta conjunta |
| **Retiro** | Retirar de la cuenta conjunta a efectivo personal |
| **Transferencia** | Transferir de la cuenta conjunta a una cuenta personal (por IBAN) |

### Abandonar una Cuenta Conjunta

1. Abre la pagina de gestion de la cuenta conjunta
2. Haz clic en **Abandonar** y confirma
3. Eres eliminado de la cuenta

> Las cuentas conjuntas estan **exentas de tributacion, intereses y cambios de puntuacion crediticia**. Cada jugador puede participar en un maximo de `maxAccountsPerPlayer` cuentas conjuntas, y cada cuenta puede tener hasta `maxMembers` miembros. El servidor valida la membresia en cada operacion (anti-trampas).

## Ahorro Clasico

La cuenta de ahorro te permite apartar dinero y ganar intereses con el tiempo.

### Depositar en Ahorro

1. Navega a la seccion de Ahorro
2. Ingresa el monto a depositar
3. El dinero se transfiere de tu cuenta corriente a tu ahorro

### Retirar del Ahorro

1. Ingresa el monto a retirar
2. El dinero se transfiere de vuelta a tu cuenta corriente

> Los retiros estan limitados a `maxWithdrawalsPerDay` por periodo de 24 horas (por defecto: 1). El ahorro gana intereses automaticamente mediante un cron del servidor (solo jugadores en linea), a la tasa definida en `Config.Savings.interestRate`, con un limite de `Config.Savings.interestCap`.

## Depositos a Plazo Fijo

Los depositos a plazo fijo bloquean una porcion de tus ahorros por un periodo determinado a cambio de una tasa de interes garantizada.

### Crear un Deposito a Plazo Fijo

1. Navega a la seccion de Ahorro
2. Elige una duracion de bloqueo (por ejemplo, 3 dias, 7 dias, 14 dias, 30 dias)
3. Ingresa el monto a bloquear (minimo: `Config.Savings.minLockAmount`)
4. Confirma — el dinero queda bloqueado y no puede retirarse hasta el vencimiento

### Progreso y Reclamacion

- Una **barra de progreso** muestra cuanto falta para el vencimiento de cada deposito
- La marca de tiempo de desbloqueo (`unlocks_at`) es absoluta y sobrevive a reinicios del servidor
- Una vez que termina el periodo de bloqueo, haz clic en **Reclamar** para recibir tu capital mas los intereses ganados

### Opciones de Bloqueo (Por Defecto)

| Duracion | Tasa de Interes | Monto Minimo |
|---|---|---|
| 3 dias | 2.0% | $1,000 |
| 7 dias | 5.0% | $1,000 |
| 14 dias | 12.0% | $1,000 |
| 30 dias | 30.0% | $1,000 |

## Trading de Criptomonedas

El sistema de trading de criptomonedas permite a los jugadores comprar y vender criptomonedas con precios reales del mercado.

### Pagina del Mercado

- Muestra **precios en vivo** para todas las monedas configuradas (actualizados cada `refreshInterval` minutos)
- **Compra** criptomonedas ingresando un monto en dolares (minimo: `Config.Crypto.minTradeAmount`)
- La cantidad de criptomoneda recibida se calcula segun el precio actual del mercado
- El dinero se deduce de tu cuenta corriente

### Pagina del Portafolio

- Muestra tus **tenencias** de cada criptomoneda
- Muestra **Ganancias y Perdidas** (P&L) en dolares ($) y porcentaje (%) por moneda y total
- **Vender** una cantidad especifica de una moneda
- **Vender Todo** para liquidar tu posicion completa en una moneda
- Las ganancias se depositan de vuelta en tu cuenta corriente

### Historial de Operaciones

- Historial paginado de todas tus operaciones con criptomonedas
- Filtrable por **Compra** o **Venta**
- Cada entrada muestra: moneda, tipo, cantidad, precio por unidad, total y fecha

> Los precios de criptomonedas se obtienen del lado del servidor mediante `sv_crypto_prices.lua` usando la API configurada (Binance, CoinCap o CoinPaprika). El servidor almacena los precios en cache y transmite actualizaciones a todos los clientes conectados. Las operaciones con criptomonedas estan **exentas de tributacion**. La proteccion contra doble gasto asegura verificaciones de saldo a nivel de base de datos.

## Sistema de Puntuacion Crediticia

Cada jugador tiene una puntuacion crediticia que va de 0 a 1000 (valor inicial por defecto: 500).

### Como Funciona

La puntuacion crediticia se modifica mediante operaciones bancarias:

| Accion | Cambio de Puntuacion |
|---|---|
| Deposito | +2 |
| Retiro | -1 |
| Transferencia enviada | +1 |
| Transferencia recibida | +1 |
| Mejora de cuenta | +5 |

### Efectos de la Puntuacion Crediticia

- **Modulacion de la tasa de interes** — Una puntuacion mas alta significa mejores tasas de interes
- **Elegibilidad para mejora de cuenta** — Premium requiere una puntuacion crediticia minima de 700
- La puntuacion se muestra como una barra de progreso en el panel principal

## Niveles de Cuenta

Hay dos niveles de cuenta: **Standard** y **Premium**.

### Comparacion

| Caracteristica | Standard | Premium |
|---|---|---|
| Tasa de Interes | 0.5% por ciclo | 1.5% por ciclo |
| Limite de Interes | $5,000 por periodo | $20,000 por periodo |
| Transferencia Maxima | $50,000 | $200,000 |
| Reduccion de Impuestos | 0% | 25% |

### Mejorar a Premium

1. Tener una puntuacion crediticia de al menos **700**
2. Tener al menos **$50,000** disponibles
3. Haz clic en el boton **Mejorar** en el panel principal
4. La tarifa de mejora se deduce de tu cuenta

## Tributacion Progresiva

Los impuestos se aplican progresivamente en depositos, retiros y transferencias usando tramos configurables.

### Tramos Fiscales por Defecto

**Depositos:**

| Tramo | Tasa |
|---|---|
| $0 - $10,000 | 0% |
| $10,000 - $50,000 | 2% |
| $50,000+ | 5% |

**Retiros:**

| Tramo | Tasa |
|---|---|
| $0 - $10,000 | 0% |
| $10,000 - $50,000 | 1% |
| $50,000+ | 3% |

**Transferencias:**

| Tramo | Tasa |
|---|---|
| $0 - $10,000 | 0% |
| $10,000 - $50,000 | 1.5% |
| $50,000+ | 4% |

### Exenciones Fiscales

Las siguientes operaciones estan **exentas de tributacion**:

- Operaciones de cuentas de sociedad
- Operaciones de cuentas conjuntas
- Operaciones de cuentas de ahorro
- Operaciones de trading de criptomonedas

### Reduccion de Impuestos Premium

Los titulares de cuentas Premium reciben una **reduccion del 25%** en todos los impuestos. Por ejemplo, si el impuesto calculado es de $400, un jugador Premium solo paga $300.

## Sistema de Intereses

Los intereses se acreditan automaticamente mediante un cron del servidor que se ejecuta cada `Config.Interest.interval` minutos (por defecto: 60).

### Como Funcionan los Intereses

1. El cron se ejecuta en el intervalo configurado
2. Solo los jugadores **en linea** reciben intereses
3. La tasa de interes depende del **nivel de cuenta** (Standard: 0.5%, Premium: 1.5%)
4. La tasa esta **modulada por la puntuacion crediticia** — puntuaciones mas altas generan mejores tasas
5. Los intereses ganados estan **limitados** por periodo de reinicio (Standard: $5,000, Premium: $20,000)
6. El limite se reinicia cada `Config.Interest.resetPeriod` minutos (por defecto: 1440 = 24 horas)

> Las cuentas de ahorro tienen un cron de intereses separado con su propia tasa y limite.

## Notificaciones por Telefono

Si un recurso de telefono compatible esta instalado y configurado, los jugadores reciben notificaciones en el telefono para eventos clave:

| Evento | Notificacion |
|---|---|
| Transferencia recibida | Monto e informacion del remitente |
| Nomina recibida | Monto y nombre de la sociedad |
| Interes acreditado | Monto acreditado |
| Deposito conjunto | Monto y nombre del miembro |
| Retiro conjunto | Monto y nombre del miembro |
| Transferencia conjunta | Monto y detalles |
| Miembro conjunto agregado | Informacion del nuevo miembro |
| Miembro conjunto salio | Informacion del miembro que se fue |

Recursos de telefono soportados: `lb-phone`, `qs-smartphone`, `gksphone`.

> Las notificaciones solo se envian a jugadores **en linea**. Cada tipo de evento puede activarse o desactivarse individualmente en la configuracion.

## Webhook de Discord

Cuando esta habilitado y configurado con una URL de webhook, todas las operaciones bancarias se registran en un canal de Discord:

- **Operaciones personales** — Depositos, retiros, transferencias, intereses, impuestos, mejoras
- **Operaciones de sociedad** — Depositos, retiros, transferencias, nomina
- **Operaciones conjuntas** — Depositos, retiros, transferencias, cambios de miembros
- **Operaciones de ahorro** — Depositos, retiros, bloqueos, reclamaciones
- **Operaciones de criptomonedas** — Compras, ventas

Cada entrada de registro se envia como un embed de Discord con los detalles de la operacion, montos e informacion del jugador. Los webhooks utilizan un enfoque de enviar y olvidar y no bloquean el juego.
