---
title: "Uso"
description: "Guía de uso del script Job Manager"
script: "foltone-job-manager"
section: "foltone_job_manager"
order: 3
version: "1.0.0"
---

# Uso — foltone_job_manager

## Funcionamiento general

El script proporciona una interfaz de tablet NUI que permite a los jefes de sociedad gestionar su empresa: dinero, empleados, salarios y transferencias. Solo los jugadores con el grado de jefe configurado pueden acceder a la interfaz.

## Acceder a la interfaz

1. Tener el **grado de jefe** (o el grado configurado en `bossGrade`) del trabajo
2. Ir al **marcador** de la sociedad (posición configurada en `config.lua`)
3. Presionar **E** para abrir la interfaz de tablet

> El marcador solo aparece si el jugador tiene el grado de jefe del trabajo correspondiente.

## Pestaña Dinero

La pestaña de gestión del dinero permite:

- **Ver el saldo** actual de la sociedad
- **Añadir dinero** — Transferir dinero personal a la caja de la sociedad
- **Retirar dinero** — Transferir dinero de la sociedad al jugador
- **Gráfico de ingresos** — Visualizar los ingresos de los últimos 10 días mediante un gráfico

> Los ingresos se registran automáticamente cada hora en el archivo `server/data.json`.

## Pestaña Empleados

La pestaña de gestión de empleados muestra la lista de todos los empleados de la sociedad con:

- **Apellido** y **Nombre**
- **Grado** actual

### Acciones disponibles

| Acción | Descripción |
|--------|-------------|
| **Promover** | Aumenta el grado del empleado un nivel |
| **Degradar** | Disminuye el grado del empleado un nivel |
| **Despedir** | Despide al empleado (lo pone en el trabajo `unemployed`) |

> Las acciones solo funcionan si el empleado objetivo está **en línea**.

## Pestaña Salarios

Esta pestaña muestra todos los grados del trabajo con su salario actual. El jefe puede **modificar el salario** de cada grado directamente en el campo de entrada.

> En ESX, los salarios se actualizan en la tabla `job_grades` de la base de datos.

## Pestaña Transferencias

El jefe puede realizar transferencias desde la caja de la sociedad hacia:

### Transferencia a un jugador

1. Seleccionar el tipo **"Persona"**
2. Introducir el **ID del servidor** del jugador destinatario
3. Introducir el **monto**
4. Hacer clic en **"Enviar transferencia"**

### Transferencia a otra sociedad

1. Seleccionar el tipo **"Sociedad"**
2. Elegir la **sociedad destinataria** en la lista desplegable
3. Introducir el **monto**
4. Hacer clic en **"Enviar transferencia"**

> Solo las sociedades configuradas en `Config.SocietyList` aparecen en la lista.

## Modo claro / oscuro

La interfaz dispone de un toggle día/noche en la esquina superior derecha. La elección del tema se guarda en el `localStorage` del navegador y persiste entre sesiones.

## Historial de ingresos

El script registra automáticamente el saldo de cada sociedad **cada hora** en el archivo `server/data.json`. Estos datos alimentan el gráfico de ingresos mostrado en la pestaña Dinero.

## Events disponibles

### Events del servidor

```lua
-- Añadir dinero a la sociedad
TriggerServerEvent("foltone_job_manager:addSocietyMoney", companyName, amount)

-- Retirar dinero de la sociedad
TriggerServerEvent("foltone_job_manager:removeSocietyMoney", companyName, amount)

-- Promover un empleado
TriggerServerEvent("foltone_job_manager:promoteEmployee", companyName, targetIdentifier)

-- Degradar un empleado
TriggerServerEvent("foltone_job_manager:unpromoteEmployee", companyName, targetIdentifier)

-- Despedir un empleado
TriggerServerEvent("foltone_job_manager:fireEmployee", companyName, targetIdentifier)

-- Actualizar el salario de un grado
TriggerServerEvent("foltone_job_manager:updateSalary", companyName, gradeId, salary)

-- Transferencia a un jugador
TriggerServerEvent("foltone_job_manager:transferSocietyMoneyToPlayer", companyName, targetId, amount)

-- Transferencia a una sociedad
TriggerServerEvent("foltone_job_manager:transferSocietyMoneyToSociety", companyName, targetCompany, amount)

-- Definir el trabajo de un jugador
TriggerServerEvent("foltone_job_manager:setJob", targetId, companyName, grade)
```

### Callbacks del servidor

```lua
-- Obtener datos de la sociedad (saldo, empleados, grados, ingresos)
TriggerServerFoltoneJMCallback("foltone_job_manager:getData", function(data)
    -- data.money.balance : saldo
    -- data.money.revenueLastDays : array de ingresos de los últimos 10 días
    -- data.employees : lista de empleados
    -- data.grades : lista de grados con salarios
end, companyName)
```
