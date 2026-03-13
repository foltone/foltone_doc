---
title: "Installation"
description: "Elevator Builder script installation guide"
script: "foltone-elevator-builder"
section: "foltone_elevator_builder"
order: 1
version: "1.1.0"
---

# Installation — foltone_elevator_builder

## Requirements

- **FiveM** with **Lua 5.4**
- **ox_target** *(optional)* — For target-based interaction instead of E key

## Download

Download the script from your Tebex account and place the folder in your `resources/` directory.

## Server Configuration

Add to your `server.cfg`:

```ini
ensure foltone-elevator-builder
```

> **Note**: This script is **standalone** — it doesn't require any framework (ESX, QBCore, etc.). Data is saved in the `json/data.json` file.

## No Database Required

Unlike other scripts, Elevator Builder does **not use a SQL database**. All elevator data is stored in the `json/data.json` file in JSON format.

## Admin Command

The script registers the `/fab` command to open the elevator admin menu. You can change this command in `client/cl_editable.lua`:

```lua
RegisterCommand("fab", function(source, args)
    TriggerEvent("foltone_ascenseur:open_menu")
end)
```

> **Important**: Make sure to restrict access to this command via your ACE permissions system to prevent all players from creating elevators.

## ox_target (optional)

If you want to use ox_target for interaction:

1. Make sure `ox_target` is running on your server
2. Enable the option in `Config.lua`:

```lua
Config.use_target = true
```

The script automatically detects ox_target. If `use_target` is enabled but ox_target is not installed, the script automatically falls back to E key interaction.

## Verification

After restarting your server:

1. Type `/fab` in chat
2. The admin NUI interface should open
3. Create an elevator with 2 floors to test
4. Markers should appear at the defined positions
