---
title: "Configuration"
description: "Banking script configuration guide"
script: "foltone-banking"
section: "foltone_banking"
order: 2
version: "1.0.0"
---

# Configuration — foltone_banking

All configuration is done in `config.lua` at the root of the script.

## Language

```lua
Config.Locale = "fr" -- "fr" or "en"
```

Translations are in the `locales/` folder. You can add your own language by creating a new file (e.g., `locales/de.lua`) and setting `Config.Locale = "de"`.

## Framework

```lua
Config.Framework = "esx" -- "esx", "qbcore" or "qbx"
```

| Value | Framework |
|---|---|
| `"esx"` | ESX Legacy |
| `"qbcore"` | QBCore |
| `"qbx"` | QBX |

## Interaction Mode

```lua
Config.InteractionType = "drawtext" -- "marker", "ox_target", "qb-target", "qtarget", "drawtext"
```

| Value | Description |
|---|---|
| `"marker"` | Ground marker at bank/ATM positions |
| `"ox_target"` | ox_target eye interaction |
| `"qb-target"` | qb-target eye interaction |
| `"qtarget"` | qtarget eye interaction |
| `"drawtext"` | Help text prompt (default) |

## IBAN & Account Settings

```lua
Config.IBANPrefix = "FB"
Config.DefaultPIN = "0000"
Config.StartingBalance = 0
```

| Parameter | Type | Description |
|---|---|---|
| `IBANPrefix` | string | Prefix for generated IBANs (e.g., `"FB"` produces `FB123456789`) |
| `DefaultPIN` | string | Default PIN code assigned to new accounts |
| `StartingBalance` | number | Starting balance for newly created accounts |

## ATM Configuration

```lua
Config.ATMs = {
    models = {"prop_atm_01", "prop_atm_02", "prop_atm_03", "prop_fleeca_atm"},
    features = {"deposit", "withdraw", "balance", "transfer", "history"},
    distance = 1.5,
    blip = false,
}
```

| Parameter | Type | Description |
|---|---|---|
| `models` | table | List of ATM prop model names to detect |
| `features` | table | Enabled features at ATMs |
| `distance` | number | Interaction distance (in game units) |
| `blip` | boolean/table | `false` to disable, or a table with `sprite`, `color`, `scale`, `label` |

> **Note**: Joint accounts, savings, and crypto are **not available** at ATMs (bank only).

## Bank Configuration

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

| Parameter | Type | Description |
|---|---|---|
| `ped.model` | string | PED model hash name for the bank clerk |
| `ped.scenario` | string | PED animation scenario |
| `features` | table | Enabled features at banks (superset of ATM features) |
| `distance` | number | Interaction distance |
| `blip` | table/false | Map blip settings or `false` to disable |
| `blip.sprite` | number | Blip sprite ID |
| `blip.color` | number | Blip color ID |
| `blip.scale` | number | Blip scale |
| `blip.label` | string | Blip label on the map |
| `positions` | table | Array of bank locations with `pos` (vector3) and `heading` (number) |

## Card System

```lua
Config.CardSystem = {
    useItem = false,
    cardItem = "bank_card",
    reissuePrice = 500,
    pinChangePrice = 100,
}
```

| Parameter | Type | Description |
|---|---|---|
| `useItem` | boolean | `true` = card is a physical ox_inventory item, `false` = virtual card |
| `cardItem` | string | ox_inventory item name (only used if `useItem = true`) |
| `reissuePrice` | number | Cost to reissue a lost/blocked card |
| `pinChangePrice` | number | Cost to change the PIN code |

## Transfer Settings

```lua
Config.Transfer = {
    allowByServerId = true,
    allowByIBAN = true,
    offlineTransfer = true,
}
```

| Parameter | Type | Description |
|---|---|---|
| `allowByServerId` | boolean | Allow transfers by entering the recipient's server ID |
| `allowByIBAN` | boolean | Allow transfers by entering the recipient's IBAN |
| `offlineTransfer` | boolean | Allow transfers to offline players (resolved by IBAN) |

## Transaction History

```lua
Config.History = {
    perPage = 50,
}
```

| Parameter | Type | Description |
|---|---|---|
| `perPage` | number | Number of transactions shown per page in the history view |

## Theme

```lua
Config.theme = {}
```

The default theme is the **Blue Edition** (Cyber Street Design System). The `theme` table is empty by default, which applies the built-in blue color scheme. You can override specific CSS variables by adding key-value pairs to this table.

> **Note**: The design system uses electric blue accents, dark panel backgrounds, and three font families (Bebas Neue, Rajdhani, JetBrains Mono). Do not use gold, orange, purple, or cyan colors.

## Notifications

```lua
Config.Notification = function(message)
    SetNotificationTextEntry("STRING")
    AddTextComponentString(message)
    DrawNotification(false, false)
end
```

Replace this function with your preferred notification system (e.g., okokNotify, ox_lib, etc.). This is a client-side function.

## Display Text

```lua
Config.DisplayText = function(text)
    SetTextComponentFormat("STRING")
    AddTextComponentString(text)
    DisplayHelpTextFromStringLabel(0, 0, 1, -1)
end
```

Customize the help text display shown when the player is near an interaction point (used with `"drawtext"` interaction mode).

## Society / Job Account Settings

```lua
Config.Society = {
    defaultGrades = {"boss", "manager"},
    jobs = {
        -- Per-job override:
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

| Parameter | Type | Description |
|---|---|---|
| `defaultGrades` | table | List of grade names that have access to society banking by default |
| `jobs` | table | Per-job overrides for allowed grades (key = job name, value = table with `grades`) |
| `features` | table | Enabled society features |
| `positions` | table | PED positions for society access points, each with `job`, `pos`, `heading` |
| `distance` | number | Interaction distance for society PED |
| `ped.model` | string | PED model for the society accountant |
| `ped.scenario` | string | PED animation scenario |
| `blip` | table/false | Map blip settings or `false` to disable |

### Features

| Feature | Description |
|---|---|
| `"balance"` | View society account balance |
| `"deposit"` | Deposit personal cash into society account |
| `"withdraw"` | Withdraw from society account to personal cash |
| `"transfer"` | Transfer from society account to a personal account (by server ID or IBAN) |
| `"payroll"` | Pay an employee from the society account |
| `"history"` | View society transaction history |

### Per-Job Grade Override

```lua
Config.Society.jobs = {
    ["police"] = { grades = {"boss", "lieutenant"} },
    ["ambulance"] = { grades = {"boss"} },
}
```

> If a job is not listed in `jobs`, the `defaultGrades` list is used.

## Credit Score

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

| Parameter | Type | Description |
|---|---|---|
| `default` | number | Starting credit score for new accounts |
| `min` | number | Minimum possible score |
| `max` | number | Maximum possible score |
| `rewards` | table | Score change per operation type (positive = increase, negative = decrease) |

### Reward Actions

| Action | Default | Description |
|---|---|---|
| `deposit` | +2 | Making a deposit |
| `withdraw` | -1 | Making a withdrawal |
| `transfer_out` | +1 | Sending a transfer |
| `transfer_in` | +1 | Receiving a transfer |
| `upgrade` | +5 | Upgrading account level |

## Account Levels

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

### Standard Level

| Parameter | Type | Description |
|---|---|---|
| `label` | string | Display name |
| `interestRate` | number | Interest rate per cron cycle (%) |
| `interestCap` | number | Maximum interest earned per reset period |
| `transferMax` | number | Maximum transfer amount |
| `taxReduction` | number | Tax reduction percentage (0 = none) |

### Premium Level

| Parameter | Type | Description |
|---|---|---|
| `label` | string | Display name |
| `interestRate` | number | Interest rate per cron cycle (%) |
| `interestCap` | number | Maximum interest earned per reset period |
| `transferMax` | number | Maximum transfer amount |
| `taxReduction` | number | Tax reduction percentage (25% = 25% less tax) |
| `upgradePrice` | number | Cost to upgrade from Standard to Premium |
| `minCreditScore` | number | Minimum credit score required to upgrade |

## Interest System

```lua
Config.Interest = {
    interval = 60,
    resetPeriod = 1440,
}
```

| Parameter | Type | Description |
|---|---|---|
| `interval` | number | Minutes between each interest cron cycle |
| `resetPeriod` | number | Minutes before the interest cap resets (1440 = 24 hours) |

> Interest is only calculated for **online** players. The actual rate is modulated by the player's credit score and capped by their account level.

## Progressive Taxation

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

Each operation type (`deposit`, `withdraw`, `transfer`) has its own set of tax brackets.

| Parameter | Type | Description |
|---|---|---|
| `from` | number | Bracket start amount (inclusive) |
| `to` | number | Bracket end amount (exclusive). `0` means unlimited (last bracket) |
| `rate` | number | Tax rate in percent for this bracket |

### How Brackets Work

Tax is calculated **progressively** across brackets. For example, a $30,000 deposit with the default config:

- $0 to $10,000: 0% tax = $0
- $10,000 to $30,000: 2% tax = $400
- **Total tax: $400**

> **Important**: Brackets must be contiguous and ordered. Society operations, joint accounts, savings, and crypto are **exempt** from taxation. Premium accounts receive a 25% tax reduction.

## Joint Account Settings

```lua
Config.JointAccount = {
    enabled = true,
    maxMembers = 4,
    maxAccountsPerPlayer = 2,
    transferMax = 50000,
    features = {"deposit", "withdraw", "transfer", "history"},
}
```

| Parameter | Type | Description |
|---|---|---|
| `enabled` | boolean | Enable or disable joint accounts |
| `maxMembers` | number | Maximum number of members per joint account |
| `maxAccountsPerPlayer` | number | Maximum joint accounts a player can be part of |
| `transferMax` | number | Maximum transfer amount from a joint account |
| `features` | table | Enabled features for joint accounts |

> Joint accounts are only accessible at **banks** (not ATMs). They are exempt from taxation, interest, and credit score changes.

## Phone Notifications

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

| Parameter | Type | Description |
|---|---|---|
| `enabled` | boolean | Enable or disable phone notifications |
| `resource` | string | Phone resource name: `"lb_phone"`, `"qs-smartphone"`, or `"gksphone"` |
| `events` | table | Toggle individual notification events on/off |
| `appTitle` | string | App name displayed in the phone notification |
| `appIcon` | string | Icon name displayed in the phone notification |

### Notification Events

| Event | Description |
|---|---|
| `transfer_received` | When the player receives a personal transfer |
| `society_payroll_received` | When the player receives a payroll payment |
| `interest_credited` | When interest is credited to the account |
| `joint_deposit` | When a member deposits into a shared joint account |
| `joint_withdraw` | When a member withdraws from a shared joint account |
| `joint_transfer` | When a member makes a transfer from a shared joint account |
| `joint_member_added` | When a new member is added to a joint account |
| `joint_member_left` | When a member leaves a joint account |

> Phone notifications are only sent to **online** players.

## Discord Webhook

```lua
Config.Webhook = {
    enabled = true,
    url = "",
    botName = "Fleeca Bank",
    color = 3899126,
}
```

| Parameter | Type | Description |
|---|---|---|
| `enabled` | boolean | Enable or disable Discord webhook logging |
| `url` | string | Discord webhook URL (leave empty to disable) |
| `botName` | string | Bot name displayed in Discord embeds |
| `color` | number | Embed color in decimal (3899126 = blue #3b82f6) |

> All banking operations (personal, society, joint, savings, crypto) are logged to the webhook. The webhook uses a fire-and-forget approach.

## Savings Account

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

| Parameter | Type | Description |
|---|---|---|
| `enabled` | boolean | Enable or disable savings accounts |
| `interestRate` | number | Classic savings interest rate (% per cron cycle) |
| `interestCap` | number | Maximum interest earned per reset period |
| `maxWithdrawalsPerDay` | number | Maximum number of withdrawals from savings per 24-hour period |
| `minLockAmount` | number | Minimum amount required to create a fixed-term deposit |

### Fixed-Term Lock Options

| Parameter | Type | Description |
|---|---|---|
| `days` | number | Lock duration in days |
| `rate` | number | Interest rate applied at maturity (%) |
| `label` | string | Display label in the UI |

> Savings accounts have a separate interest cron from the main checking account. Interest is online-only with a configurable cap.

## Crypto Trading

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

| Parameter | Type | Description |
|---|---|---|
| `enabled` | boolean | Enable or disable crypto trading |
| `apiSource` | string | Price API source: `"binance"`, `"coincap"`, or `"coinpaprika"` |
| `refreshInterval` | number | Minutes between price fetches from the API |
| `coins` | table | List of tradeable cryptocurrencies |
| `currency` | string | Reference currency for prices (e.g., `"usd"`) |
| `minTradeAmount` | number | Minimum trade amount in dollars |
| `historyPerPage` | number | Number of trades shown per page in history |

### Coin Configuration

| Parameter | Type | Description |
|---|---|---|
| `id` | string | Coin identifier used by the API (e.g., `"bitcoin"`) |
| `symbol` | string | Ticker symbol displayed in the UI (e.g., `"BTC"`) |
| `label` | string | Full display name (e.g., `"Bitcoin"`) |

> Prices are fetched server-side via `sv_crypto_prices.lua` and broadcast to all connected clients. The server maintains a cache to minimize API calls. Crypto operations are exempt from taxation.
