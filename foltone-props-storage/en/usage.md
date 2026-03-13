---
title: "Usage"
description: "Props Storage script usage guide"
script: "foltone-props-storage"
section: "foltone_props_storage"
order: 3
version: "1.0.0"
---

# Usage — foltone_props_storage

## Overview

The script allows players to place physical safes in the game world. Each safe is protected by a PIN code and only the owner can pick it up.

## Placing a Storage

1. **Get the item** — A player needs a safe item (`big_safe` or `safe`) in their inventory
2. **Use the item** — Using the item opens the placement interface
3. **Position the safe**:
   - **Arrow keys** — Move the safe (forward/backward/left/right)
   - **A / E keys** — Rotate the safe
   - **Enter** — Confirm placement
4. **Set PIN code** — A dialog asks for a PIN (minimum 4 digits, simple codes forbidden)

The safe is then placed in the world and saved to the database.

## Accessing a Storage

### Without ox_inventory (RageUI)

1. Walk up to the safe (configurable distance, default 2.5m)
2. Press **E** to interact
3. Enter the **PIN code**
4. The RageUI menu opens with options:
   - **Deposit/Withdraw items**
   - **Deposit/Withdraw money** (cash + dirty money)
   - **Deposit/Withdraw weapons** (with ammo)
   - **Change PIN** *(owner only)*
   - **Pick up safe** *(owner only, safe must be empty)*

### With ox_inventory

1. Walk up to the safe
2. Use **ox_target** to interact
3. Enter the **PIN code**
4. The **ox_inventory** interface opens as a regular stash
5. Drag and drop items as usual

## Weight System

Each safe has a maximum weight capacity:

| Type | Model | Capacity |
|------|-------|----------|
| Large Safe | `p_v_43_safe_s` | 50,000 |
| Safe | `prop_ld_int_safe_01` | 30,000 |

Items have weights defined in ESX/ox_inventory. Weapons have configurable weights in `config.lua`.

## PIN Security

- PIN must be **at least 4 digits**
- Simple codes are **forbidden**: `0000`, `1111`, `2222`, ..., `9999`, `1234`
- Only the **owner** can change the PIN
- Only the **owner** can pick up the safe

## Changing the PIN

1. Open the safe with your current PIN
2. Select **"Change PIN"** from the menu
3. Enter your new PIN code

> **Note**: This option is only visible to the safe owner.

## Picking Up a Storage

1. Open the safe with your PIN
2. **Empty the safe completely** (items, money, weapons)
3. Select **"Pick up safe"**
4. The safe item returns to your inventory
5. The safe is removed from the world and database

## Instances / Buckets

The script supports FiveM **routing buckets**. Safes placed in a specific instance are only visible within that instance.

To sync a player's instance from another script:

```lua
TriggerClientEvent("foltone_props_storage:updatePlayerInstance", playerId, instanceId)
```

## Discord Logs

All actions are logged via Discord webhook:

- Placing a new safe
- Opening a safe
- Depositing / withdrawing items
- Depositing / withdrawing money
- Depositing / withdrawing weapons
- Changing PIN
- Picking up a safe

## Available Events

### Server Events

```lua
-- Place a safe (triggered automatically via item use)
TriggerServerEvent("foltone_props_storage:addNewPropStorage", ...)

-- Deposit/Withdraw
TriggerServerEvent("foltone_props_storage:putPropMoney", id, type, amount)
TriggerServerEvent("foltone_props_storage:takePropMoney", id, type, amount)
TriggerServerEvent("foltone_props_storage:putPropItem", id, itemName, count)
TriggerServerEvent("foltone_props_storage:takePropItem", id, itemName, count)
TriggerServerEvent("foltone_props_storage:putPropWeapon", id, weaponName, ammo)
TriggerServerEvent("foltone_props_storage:takePropWeapon", id, weaponName)
```

### Server Callbacks

```lua
-- Verify PIN and open safe
ESX.TriggerServerCallback("foltone_props_storage:tryOpenProp", function(success)
    -- success: true/false
end, propId, pin)

-- Get safe inventory data
ESX.TriggerServerCallback("foltone_props_storage:getPropData", function(data)
    -- data: inventory, weight, etc.
end, propId)

-- Check if player is owner
ESX.TriggerServerCallback("foltone_props_storage:isOwner", function(isOwner)
    -- isOwner: true/false
end, propId)
```

### Client Events

```lua
-- Sync player instance
TriggerClientEvent("foltone_props_storage:updatePlayerInstance", playerId, instanceId)
```
