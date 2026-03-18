---
title: "Instalacion"
description: "Guia de instalacion del script bancario"
script: "foltone-banking"
section: "Banking"
order: 1
version: "1.0.0"
---

# Instalacion — foltone_banking

## Requisitos

- **ESX Legacy** o **QBCore** o **QBX** — Framework
- **oxmysql** — Libreria MySQL

### Dependencias Opcionales

| Dependencia | Proposito |
|---|---|
| `esx_addonaccount` | Cuentas de sociedad (solo ESX) |
| `qb-banking` | Cuentas de sociedad (solo QBCore / QBX) |
| `ox_target` | Modo de interaccion por objetivo |
| `qb-target` | Modo de interaccion por objetivo |
| `qtarget` | Modo de interaccion por objetivo |
| `ox_inventory` | Tarjeta bancaria fisica como objeto |
| `lb-phone` | Notificaciones por telefono |
| `qs-smartphone` | Notificaciones por telefono |
| `gksphone` | Notificaciones por telefono |

## Descarga

Descarga el script desde tu cuenta de [Tebex](https://foltone.tebex.io/) y coloca la carpeta `foltone_banking` en tu directorio `resources/`.

## Configuracion del Servidor

Agrega a tu `server.cfg`:

```ini
ensure oxmysql
ensure es_extended       # o qb-core / qbx_core
ensure esx_addonaccount  # Solo ESX, para cuentas de sociedad
ensure foltone_banking
```

> **Importante**: `foltone_banking` debe iniciarse **despues** de tu framework y `oxmysql`. Si usas dependencias opcionales (ox_target, lb-phone, etc.), aseguralas **antes** de `foltone_banking`.

## Framework

El script soporta 3 frameworks:

| Framework | Valor de configuracion | Dependencias requeridas | Dependencia de sociedad |
|---|---|---|---|
| ESX Legacy | `"esx"` | `es_extended`, `oxmysql` | `esx_addonaccount` |
| QBCore | `"qbcore"` | `qb-core`, `oxmysql` | `qb-banking` |
| QBX | `"qbx"` | `qbx_core`, `oxmysql` | `qb-banking` |

Configura el framework en `config.lua`:

```lua
Config.Framework = "esx" -- "esx", "qbcore" or "qbx"
```

## Configuracion de Base de Datos

### Instalacion Nueva

Ejecuta el archivo `sql/install.sql` en tu base de datos. Esto crea todas las tablas necesarias:

- `foltone_banking_accounts` — Cuentas personales
- `foltone_banking_transactions` — Historial de transacciones personales
- `foltone_banking_cards` — Tarjetas bancarias
- `foltone_banking_society_transactions` — Historial de transacciones de sociedad
- `foltone_banking_joint_accounts` — Cuentas conjuntas
- `foltone_banking_joint_members` — Miembros de cuentas conjuntas
- `foltone_banking_joint_transactions` — Historial de transacciones conjuntas
- `foltone_banking_savings` — Cuentas de ahorro
- `foltone_banking_savings_locks` — Depositos a plazo fijo
- `foltone_banking_crypto_holdings` — Carteras de criptomonedas
- `foltone_banking_crypto_trades` — Historial de operaciones con criptomonedas

```sql
-- Importar el esquema completo
SOURCE sql/install.sql;
```

### Actualizacion desde una Version Anterior

Si estas actualizando desde una version anterior, ejecuta los archivos de migracion correspondientes **en orden**:

| Archivo de migracion | Agrega |
|---|---|
| `sql/migrate_phase3.sql` | Columnas de puntuacion crediticia, niveles de cuenta, intereses y tributacion |
| `sql/migrate_phase4.sql` | Tablas de cuentas conjuntas |
| `sql/migrate_phase5.sql` | Tablas de ahorro y criptomonedas, ENUM de transacciones extendido |

> **Advertencia**: Solo ejecuta los archivos de migracion que correspondan a versiones que **aun no** hayas instalado. Ejecutar `install.sql` en un servidor nuevo ya incluye todo.

## Verificacion

Despues de reiniciar tu servidor:

1. Revisa la consola del servidor en busca de errores relacionados con `foltone_banking`
2. Conectate con un personaje
3. Ve a una **ubicacion bancaria** (un PED deberia aparecer en las posiciones configuradas) o acercate a un **cajero automatico**
4. Interactua con el PED del banco o el cajero automatico para abrir la interfaz bancaria
5. La NUI deberia aparecer con el panel principal mostrando tu saldo, IBAN y las operaciones disponibles
