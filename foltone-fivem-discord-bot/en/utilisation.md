---
title: "Usage"
description: "Usage of the Foltone FiveM Discord Bot script"
script: "foltone-fivem-discord-bot"
section: "Discord Bot"
order: 3
version: "1.0.0"
---

# Usage — foltone_fivem_discord_bot

## Discord Slash Commands

All commands are executed from Discord with the `/` prefix.

### Players

| Command | Description | Permission |
|---------|-------------|------------|
| `/playerlist` | List connected players with server ID and identifiers | moderator |
| `/playerinfo [id]` | Detailed information about a player (identifiers, job, money) | moderator |
| `/kick [id] [reason]` | Kick a player from the server | moderator |
| `/ban [id] [duration] [reason]` | Ban a player (e.g., duration `7d`, `permanent`) | admin |
| `/unban [identifier]` | Lift a player ban | admin |
| `/spectate [id]` | Enter spectator mode on a player | moderator |

### Moderation

| Command | Description | Permission |
|---------|-------------|------------|
| `/warn [id] [reason]` | Warn a player (logged to database) | moderator |
| `/mute [id] [duration] [reason]` | Mute a player in the in-game chat | moderator |
| `/unmute [id]` | Unmute a player | moderator |
| `/freeze [id]` | Freeze a player in place | moderator |
| `/unfreeze [id]` | Unfreeze a player | moderator |
| `/slap [id] [force]` | Knock a player back | moderator |
| `/heal [id]` | Fully heal a player | moderator |
| `/revive [id]` | Revive a downed player | admin |
| `/sanctions [id]` | View a player's sanction history | moderator |

### Economy

| Command | Description | Permission |
|---------|-------------|------------|
| `/givemoney [id] [amount] [account]` | Give money to a player | admin |
| `/removemoney [id] [amount] [account]` | Remove money from a player | admin |
| `/setmoney [id] [amount] [account]` | Set a player's money | admin |
| `/giveitem [id] [item] [quantity]` | Give an item to a player | admin |
| `/removeitem [id] [item] [quantity]` | Remove an item from a player | admin |

### Vehicles & Teleportation

| Command | Description | Permission |
|---------|-------------|------------|
| `/tp [id] [target_id]` | Teleport a player to another player | admin |
| `/spawnvehicle [id] [model]` | Spawn a vehicle for a player | admin |
| `/deletevehicle [id]` | Delete a player's vehicle | admin |

### Job

| Command | Description | Permission |
|---------|-------------|------------|
| `/setjob [id] [job] [grade]` | Change a player's job | admin |

### Server

| Command | Description | Permission |
|---------|-------------|------------|
| `/announce [message]` | Send an announcement to all players in-game | admin |
| `/weather [type]` | Change the server weather | admin |
| `/time [hour]` | Change the server time | admin |
| `/whitelist [add/remove] [identifier]` | Manage the server whitelist | admin |
| `/serverstatus` | Show server statistics | all |

### Tracking & Scheduling

| Command | Description | Permission |
|---------|-------------|------------|
| `/watchlist [add/remove/list] [identifier]` | Manage the watchlist | admin |
| `/schedule [add/remove/list]` | Manage scheduled tasks | founder |

---

## Discord Dashboard

The dashboard is a Discord embed that auto-updates (every X seconds as per `Config.Dashboard.refreshInterval`).

It shows:
- Connected players / maximum
- Server uptime
- Recent connections and disconnections
- Recent admin actions
- Quick action buttons (quick kick, view player list)

The dashboard updates automatically and requires no interaction.

---

## Ticket System

### From Discord

Players can open a ticket using buttons available in your welcome channel or via a configured command.

On creation:
1. A private channel is created in the configured category
2. The player and admins have access
3. The channel is named `ticket-{name}-{id}`

On closure:
1. An admin clicks the **Close Ticket** button
2. The transcript is saved (if `transcriptEnabled = true`)
3. The channel is deleted and a log is sent to `logsChannelId`

### From the game

Players can open a ticket directly from FiveM:
- Command: `/{Config.Tickets.command}` (default: `/ticket`)
- Shortcut key: `Config.Tickets.keybind` (default: F6)

Ticket messages are synchronized in real time between Discord and the game.

---

## Synchronized Chat

Chat is bidirectional between Discord and the game:
- Messages sent in the configured Discord channel appear in-game with the `[DISCORD]` prefix
- Player messages in-game appear on Discord with their name

Discord messages display the user's name and avatar.

---

## Smart Alerts

The alerts system automatically sends notifications to the configured channel based on defined rules:

| Alert | Trigger |
|-------|---------|
| Excessive warnings | Player with X warns in Y minutes |
| Suspicious transaction | Transaction exceeding the threshold |
| Low server population | Player count below threshold |
| High server population | Player count above threshold |
| Watched player | A watchlisted player connects |
| Serial killer | Player with X kills in Y minutes |
| Mass crash | X players disconnected in Y minutes |

Alerts mention the configured role in `mentionRoleId` for urgent alerts.

---

## Admin NUI Panel (in-game)

The NUI panel is accessible only to in-game admins.

### Access

- Command: `/adminpanel` (or configured command in `Config.Panel.command`)
- Shortcut key: F7 (or configured key in `Config.Panel.keybind`)
- Close: same key or Escape

### Available pages

| Page | Description |
|------|-------------|
| **Dashboard** | Overview: online players, server stats, uptime |
| **Players** | Player list with quick actions (kick, ban, tp, heal, revive) |
| **Economy** | Manage player money and inventory |
| **Logs** | Server log history with filters by type |
| **Tickets** | View and manage open tickets |
| **Scheduler** | Manage scheduled tasks (restarts, announcements) |

### Quick actions (players panel)

In the players tab, select a player to access:
- Kick / Ban
- Teleport to / Teleport here
- Give money / items
- Heal / Revive / Freeze
- View sanctions

---

## Task Scheduler

Scheduled tasks (restarts, announcements) are managed through the scheduler:

### From Discord

```
/schedule add daily_restart restart "0 4 * * *" 30,15,5,1
/schedule list
/schedule remove daily_restart
```

### From the NUI panel

The **Scheduler** tab in the NUI panel allows viewing and managing tasks without leaving the game.

### Cron format

| Expression | Description |
|------------|-------------|
| `0 4 * * *` | Every day at 4:00 AM |
| `0 */6 * * *` | Every 6 hours |
| `0 12 * * 1` | Every Monday at 12:00 PM |
