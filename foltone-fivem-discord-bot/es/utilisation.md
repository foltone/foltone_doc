---
title: "Uso"
description: "Uso del script Foltone FiveM Discord Bot"
script: "foltone-fivem-discord-bot"
section: "Discord Bot"
order: 3
version: "1.0.0"
---

# Uso — foltone_fivem_discord_bot

## Comandos Slash de Discord

Todos los comandos se ejecutan desde Discord con el prefijo `/`.

### Jugadores

| Comando | Descripción | Permiso |
|---------|-------------|------------|
| `/playerlist` | Lista de jugadores conectados con ID de servidor e identificadores | moderator |
| `/playerinfo [id]` | Información detallada de un jugador (identificadores, trabajo, dinero) | moderator |
| `/kick [id] [reason]` | Expulsar a un jugador del servidor | moderator |
| `/ban [id] [duration] [reason]` | Banear a un jugador (ej., duración `7d`, `permanent`) | admin |
| `/unban [identifier]` | Levantar el baneo de un jugador | admin |
| `/spectate [id]` | Entrar en modo espectador sobre un jugador | moderator |

### Moderación

| Comando | Descripción | Permiso |
|---------|-------------|------------|
| `/warn [id] [reason]` | Advertir a un jugador (registrado en la base de datos) | moderator |
| `/mute [id] [duration] [reason]` | Silenciar a un jugador en el chat del juego | moderator |
| `/unmute [id]` | Quitar el silencio a un jugador | moderator |
| `/freeze [id]` | Congelar a un jugador en su lugar | moderator |
| `/unfreeze [id]` | Descongelar a un jugador | moderator |
| `/slap [id] [force]` | Empujar a un jugador hacia atrás | moderator |
| `/heal [id]` | Curar completamente a un jugador | moderator |
| `/revive [id]` | Revivir a un jugador caído | admin |
| `/sanctions [id]` | Ver el historial de sanciones de un jugador | moderator |

### Economía

| Comando | Descripción | Permiso |
|---------|-------------|------------|
| `/givemoney [id] [amount] [account]` | Dar dinero a un jugador | admin |
| `/removemoney [id] [amount] [account]` | Quitar dinero a un jugador | admin |
| `/setmoney [id] [amount] [account]` | Establecer el dinero de un jugador | admin |
| `/giveitem [id] [item] [quantity]` | Dar un objeto a un jugador | admin |
| `/removeitem [id] [item] [quantity]` | Quitar un objeto a un jugador | admin |

### Vehículos y teletransporte

| Comando | Descripción | Permiso |
|---------|-------------|------------|
| `/tp [id] [target_id]` | Teletransportar a un jugador hacia otro jugador | admin |
| `/spawnvehicle [id] [model]` | Generar un vehículo para un jugador | admin |
| `/deletevehicle [id]` | Eliminar el vehículo de un jugador | admin |

### Trabajo

| Comando | Descripción | Permiso |
|---------|-------------|------------|
| `/setjob [id] [job] [grade]` | Cambiar el trabajo de un jugador | admin |

### Servidor

| Comando | Descripción | Permiso |
|---------|-------------|------------|
| `/announce [message]` | Enviar un anuncio a todos los jugadores en el juego | admin |
| `/weather [type]` | Cambiar el clima del servidor | admin |
| `/time [hour]` | Cambiar la hora del servidor | admin |
| `/whitelist [add/remove] [identifier]` | Gestionar la whitelist del servidor | admin |
| `/serverstatus` | Mostrar estadísticas del servidor | all |

### Seguimiento y programación

| Comando | Descripción | Permiso |
|---------|-------------|------------|
| `/watchlist [add/remove/list] [identifier]` | Gestionar la lista de vigilancia | admin |
| `/schedule [add/remove/list]` | Gestionar las tareas programadas | founder |

---

## Dashboard de Discord

El dashboard es un embed de Discord que se actualiza automáticamente (cada X segundos según `Config.Dashboard.refreshInterval`).

Muestra:
- Jugadores conectados / máximo
- Tiempo de actividad del servidor
- Conexiones y desconexiones recientes
- Acciones de administradores recientes
- Botones de acción rápida (expulsión rápida, ver lista de jugadores)

El dashboard se actualiza automáticamente y no requiere interacción.

---

## Sistema de tickets

### Desde Discord

Los jugadores pueden abrir un ticket usando los botones disponibles en tu canal de bienvenida o mediante un comando configurado.

Al crear:
1. Se crea un canal privado en la categoría configurada
2. El jugador y los administradores tienen acceso
3. El canal se nombra `ticket-{name}-{id}`

Al cerrar:
1. Un administrador hace clic en el botón **Cerrar Ticket**
2. La transcripción se guarda (si `transcriptEnabled = true`)
3. El canal se elimina y se envía un registro a `logsChannelId`

### Desde el juego

Los jugadores pueden abrir un ticket directamente desde FiveM:
- Comando: `/{Config.Tickets.command}` (por defecto: `/ticket`)
- Tecla de acceso rápido: `Config.Tickets.keybind` (por defecto: F6)

Los mensajes de los tickets se sincronizan en tiempo real entre Discord y el juego.

---

## Chat sincronizado

El chat es bidireccional entre Discord y el juego:
- Los mensajes enviados en el canal de Discord configurado aparecen en el juego con el prefijo `[DISCORD]`
- Los mensajes de los jugadores en el juego aparecen en Discord con su nombre

Los mensajes de Discord muestran el nombre y avatar del usuario.

---

## Alertas inteligentes

El sistema de alertas envía automáticamente notificaciones al canal configurado según las reglas definidas:

| Alerta | Activación |
|-------|---------|
| Advertencias excesivas | Jugador con X advertencias en Y minutos |
| Transacción sospechosa | Transacción que supera el umbral |
| Baja población del servidor | Número de jugadores por debajo del umbral |
| Alta población del servidor | Número de jugadores por encima del umbral |
| Jugador vigilado | Un jugador de la lista de vigilancia se conecta |
| Asesino en serie | Jugador con X asesinatos en Y minutos |
| Desconexión masiva | X jugadores desconectados en Y minutos |

Las alertas mencionan el rol configurado en `mentionRoleId` para alertas urgentes.

---

## Panel NUI de administración (en el juego)

El panel NUI es accesible solo para administradores en el juego.

### Acceso

- Comando: `/adminpanel` (o el comando configurado en `Config.Panel.command`)
- Tecla de acceso rápido: F7 (o la tecla configurada en `Config.Panel.keybind`)
- Cerrar: misma tecla o Escape

### Páginas disponibles

| Página | Descripción |
|------|-------------|
| **Dashboard** | Vista general: jugadores en línea, estadísticas del servidor, tiempo de actividad |
| **Jugadores** | Lista de jugadores con acciones rápidas (expulsar, banear, tp, curar, revivir) |
| **Economía** | Gestionar dinero e inventario de jugadores |
| **Registros** | Historial de registros del servidor con filtros por tipo |
| **Tickets** | Ver y gestionar tickets abiertos |
| **Programador** | Gestionar tareas programadas (reinicios, anuncios) |

### Acciones rápidas (panel de jugadores)

En la pestaña de jugadores, selecciona un jugador para acceder a:
- Expulsar / Banear
- Teletransportar a / Teletransportar aquí
- Dar dinero / objetos
- Curar / Revivir / Congelar
- Ver sanciones

---

## Programador de tareas

Las tareas programadas (reinicios, anuncios) se gestionan a través del programador:

### Desde Discord

```
/schedule add daily_restart restart "0 4 * * *" 30,15,5,1
/schedule list
/schedule remove daily_restart
```

### Desde el panel NUI

La pestaña **Programador** en el panel NUI permite ver y gestionar tareas sin salir del juego.

### Formato cron

| Expresión | Descripción |
|------------|-------------|
| `0 4 * * *` | Todos los días a las 4:00 AM |
| `0 */6 * * *` | Cada 6 horas |
| `0 12 * * 1` | Todos los lunes a las 12:00 PM |
