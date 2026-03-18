---
title: "Instalación"
description: "Instalación del script Foltone FiveM Discord Bot"
script: "foltone-fivem-discord-bot"
section: "Discord Bot"
order: 1
version: "1.0.0"
---

# Instalación — foltone_fivem_discord_bot

## Requisitos previos

- **Node.js 18+** — Entorno de ejecución JavaScript para el bot
- **Servidor FiveM** — Servidor de juego con `oxmysql`
- **ESX Legacy** o **QBCore** o **QBX** — Framework de FiveM
- **oxmysql** — Librería MySQL

### Dependencias opcionales

| Dependencia | Propósito | Requerida para |
|-----------|---------|-------------|
| `vMenu` | Detección de administradores | Si `AdminSystem = "vmenu"` |
| `txAdmin` | Detección de administradores | Si `AdminSystem = "txadmin"` |
| `EasyAdmin` | Detección de administradores | Si `AdminSystem = "easyadmin"` |

## Descarga

Descarga el script desde tu cuenta de Tebex y coloca la carpeta `foltone_fivem_discord_bot` en tu directorio `resources/`.

## Paso 1 — Crear el bot de Discord

1. Ve al [Portal de Desarrolladores de Discord](https://discord.com/developers/applications)
2. Haz clic en **New Application** y dale un nombre a tu bot
3. En la pestaña **Bot**:
   - Haz clic en **Reset Token** y copia el token (lo necesitarás en `config.lua`)
   - Activa los siguientes **Privileged Gateway Intents**:
     - `SERVER MEMBERS INTENT`
     - `MESSAGE CONTENT INTENT`
4. En la pestaña **OAuth2 > URL Generator**:
   - Marca `bot` y `applications.commands`
   - Marca los siguientes permisos: `Send Messages`, `Manage Channels`, `Read Message History`, `Embed Links`, `Attach Files`, `Manage Messages`
   - Copia la URL generada e invita al bot a tu servidor de Discord

## Paso 2 — Importar la base de datos

Ejecuta el archivo `sql/install.sql` en tu base de datos MySQL:

```bash
mysql -u root -p your_database < sql/install.sql
```

También puedes copiar el contenido del archivo y ejecutarlo en phpMyAdmin o HeidiSQL.

## Paso 3 — Configurar config.lua

Abre `config.lua` y completa la información requerida:

```lua
Config.Bot = {
    token = "YOUR_TOKEN_HERE",          -- Token copiado del Portal de Desarrolladores
    guildId = "YOUR_GUILD_ID",          -- Clic derecho en tu servidor > Copiar ID
    port = 3847,                         -- Puerto de comunicación interna (no cambiar salvo conflicto)
    authToken = "A_RANDOM_SECRET",      -- Clave secreta interna (genera una cadena aleatoria)
    autoStart = true,
    healthCheckInterval = 60,
}
```

> **Importante**: Para obtener los IDs de Discord, activa el **Modo Desarrollador** en la configuración de Discord (Configuración > Avanzado > Modo Desarrollador), luego haz clic derecho en un servidor, canal o rol para copiar su ID.

Después configura los IDs de canales y roles según sea necesario. Consulta la página de [Configuración](./configuration.md) para más detalles sobre cada sección.

## Paso 4 — Instalar las dependencias de Node.js

```bash
cd resources/foltone_fivem_discord_bot/bot
npm install
```

> Este paso instala todas las dependencias de Node.js necesarias para que el bot funcione (discord.js, axios, etc.).

## Paso 5 — Configuración del servidor

Añade a tu `server.cfg`:

```ini
ensure oxmysql
ensure es_extended      # o qb-core / qbx_core
ensure foltone_fivem_discord_bot
```

> **Importante**: `foltone_fivem_discord_bot` debe iniciarse **después** de tu framework y `oxmysql`.

## Framework

El script soporta 3 frameworks y detección automática:

| Framework | Valor de configuración | Dependencias |
|-----------|-------------|--------------|
| Detección automática | `"auto"` | Detecta automáticamente ESX / QBCore / QBX |
| ESX Legacy | `"esx"` | `es_extended`, `oxmysql` |
| QBCore | `"qbcore"` | `qb-core`, `oxmysql` |
| QBX | `"qbx"` | `qbx_core`, `oxmysql` |

```lua
Config.Framework = "auto" -- "auto", "esx", "qbcore" o "qbx"
```

## Verificación

Después de reiniciar el servidor:

1. Comprueba la consola del servidor — deberías ver `[foltone_fivem_discord_bot] Bot connected as YourBotName#1234`
2. En Discord, escribe `/playerlist` — debería aparecer la lista de jugadores conectados
3. Conéctate al servidor en el juego, escribe `/adminpanel` (o F7) — el panel NUI debería abrirse
4. Verifica que el canal del dashboard se actualice automáticamente

> Si el bot no se inicia, asegúrate de que Node.js 18+ esté instalado en tu máquina y que las dependencias de `npm install` hayan sido instaladas.
