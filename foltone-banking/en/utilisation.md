---
title: "Usage"
description: "Banking script usage guide"
script: "foltone-banking"
section: "Banking"
order: 3
version: "1.0.0"
---

# Usage — foltone_banking

## Overview

Foltone Banking is a complete banking script for FiveM with a modern NUI interface (Blue Edition design). It provides personal accounts, society accounts, joint accounts, savings, crypto trading, credit scoring, progressive taxation, and more.

## Accessing the Banking Interface

There are three ways to access the banking interface:

| Access Point | Location | Available Features |
|---|---|---|
| **Bank PED** | Configured bank positions (Fleeca branches) | All features (personal, society, joint, savings, crypto) |
| **ATM** | Any ATM prop in the game world | Personal features only (deposit, withdraw, transfer, history) |
| **Society PED** | Configured workplace positions | Society features only |

The interaction method depends on `Config.InteractionType`:

- **marker** — Walk into the marker and press E
- **drawtext** — Approach and press E when help text appears
- **ox_target / qb-target / qtarget** — Use the eye/target system on the PED or ATM

## Dashboard

The dashboard is the main page displayed when the interface opens. It shows:

- **Balance** — Current checking account balance
- **IBAN** — Your unique account identifier (e.g., `FB123456789`)
- **Balance Evolution Chart** — Visual graph of your balance over time
- **Credit Score** — Score bar from 0 to 1000 with current value
- **Account Level** — Standard or Premium badge with upgrade option
- **Deposit** — Deposit cash into your account (with real-time tax preview)
- **Withdraw** — Withdraw money from your account (with real-time tax preview)

> The tax preview updates in real-time as you type the amount, showing exactly how much tax will be applied based on the progressive brackets and your account level.

## Transfers

The transfer page allows you to send money to other players.

### Transfer by Server ID

1. Select the **Server ID** mode
2. Enter the recipient's server ID
3. Enter the amount
4. Optionally add a label/description
5. Confirm the transfer

### Transfer by IBAN

1. Select the **IBAN** mode
2. Enter the recipient's IBAN (personal or joint account)
3. The system resolves the IBAN and displays the recipient's name
4. Enter the amount
5. Optionally add a label/description
6. Confirm the transfer

> Transfers support both personal IBANs and joint account IBANs. Offline transfers are possible if `Config.Transfer.offlineTransfer` is enabled. A real-time tax preview is displayed. The maximum transfer amount is determined by your account level.

## Transaction History

The history page displays all transactions with pagination.

### Available Filters

| Filter | Shows |
|---|---|
| All | All transactions |
| Deposit | Deposits |
| Withdraw | Withdrawals |
| Transfer In | Received transfers |
| Transfer Out | Sent transfers |
| Interest | Interest credits |
| Tax | Tax deductions |
| Upgrade | Account upgrade payments |

Each entry displays the type, amount, balance after transaction, date, and a badge indicating the operation type. Pagination is controlled by `Config.History.perPage`.

## Bank Card

The card management section is available at banks only. It displays:

- **Card Number** — Your 16-digit virtual card number
- **PIN Code** — Current PIN (hidden by default)
- **Card Status** — Active or Blocked

### Available Actions

| Action | Cost | Description |
|---|---|---|
| **Block / Unblock** | Free | Toggle card active status |
| **Change PIN** | Configurable (`pinChangePrice`) | Set a new 4-digit PIN code |
| **Reissue Card** | Configurable (`reissuePrice`) | Get a new card number |

> If `Config.CardSystem.useItem` is enabled, the card is a physical ox_inventory item.

## Society Accounts

Society (job) accounts are accessible to players with authorized grades (configured in `Config.Society.defaultGrades` or per-job overrides).

### Access

- From the **bank** or **ATM**: a society tab appears in the sidebar if the player has the required grade
- From a **society PED**: opens directly to the society interface (if positions are configured)

### Society Dashboard

Displays the society account balance, the job name, and the player's grade.

### Society Operations

| Operation | Description |
|---|---|
| **Deposit** | Transfer personal cash into the society account |
| **Withdraw** | Withdraw from the society account to personal cash |
| **External Transfer** | Transfer from the society account to a personal account (by server ID or IBAN) |
| **Payroll** | Pay an online employee from the society account (enter their server ID and amount) |

> Society operations are **exempt from taxation**. The balance is managed by the framework (esx_addonaccount or qb-banking).

### Society History

Dedicated transaction history for the society account. Each entry shows the employee name, grade, operation type, amount, and target (for transfers/payroll).

## Joint Accounts

Joint accounts allow multiple players to share a bank account. They are available at **banks only** (not ATMs).

### Creating a Joint Account

1. Navigate to the Joint Accounts section in the sidebar
2. Click **Create Joint Account**
3. A new joint account is created with a unique IBAN
4. You are automatically added as the first member

### Adding Members

1. Open the joint account management page
2. Enter the server ID of the player to add
3. Confirm — the player is added to the joint account

### Joint Account Operations

| Operation | Description |
|---|---|
| **Deposit** | Deposit personal cash into the joint account |
| **Withdraw** | Withdraw from the joint account to personal cash |
| **Transfer** | Transfer from the joint account to a personal account (by IBAN) |

### Leaving a Joint Account

1. Open the joint account management page
2. Click **Leave** and confirm
3. You are removed from the account

> Joint accounts are **exempt from taxation, interest, and credit score** changes. Each player can be part of up to `maxAccountsPerPlayer` joint accounts, and each account can have up to `maxMembers` members. The server validates membership on every operation (anti-cheat).

## Classic Savings

The savings account lets you set aside money and earn interest over time.

### Deposit to Savings

1. Navigate to the Savings section
2. Enter the amount to deposit
3. The money is transferred from your checking account to your savings

### Withdraw from Savings

1. Enter the amount to withdraw
2. The money is transferred back to your checking account

> Withdrawals are limited to `maxWithdrawalsPerDay` per 24-hour period (default: 1). Savings earn interest automatically via a server cron (online players only), at the rate defined in `Config.Savings.interestRate`, capped at `Config.Savings.interestCap`.

## Fixed-Term Deposits

Fixed-term deposits lock a portion of your savings for a set period in exchange for a guaranteed interest rate.

### Creating a Fixed-Term Deposit

1. Navigate to the Savings section
2. Choose a lock duration (e.g., 3 days, 7 days, 14 days, 30 days)
3. Enter the amount to lock (minimum: `Config.Savings.minLockAmount`)
4. Confirm — the money is locked and cannot be withdrawn until maturity

### Progress and Claim

- A **progress bar** shows how far along each deposit is toward maturity
- The unlock timestamp (`unlocks_at`) is absolute and survives server restarts
- Once the lock period ends, click **Claim** to receive your capital plus earned interest

### Lock Options (Default)

| Duration | Interest Rate | Minimum Amount |
|---|---|---|
| 3 days | 2.0% | $1,000 |
| 7 days | 5.0% | $1,000 |
| 14 days | 12.0% | $1,000 |
| 30 days | 30.0% | $1,000 |

## Crypto Trading

The crypto trading system lets players buy and sell cryptocurrencies with real market prices.

### Market Page

- Displays **live prices** for all configured coins (updated every `refreshInterval` minutes)
- **Buy** crypto by entering a dollar amount (minimum: `Config.Crypto.minTradeAmount`)
- The quantity of crypto received is calculated based on the current market price
- Money is deducted from your checking account

### Portfolio Page

- Displays your **holdings** for each cryptocurrency
- Shows **Profit & Loss** (P&L) in both dollars ($) and percentage (%) per coin and total
- **Sell** a specific quantity of a coin
- **Sell All** to liquidate your entire position in a coin
- Proceeds are deposited back to your checking account

### Trade History

- Paginated history of all your crypto trades
- Filterable by **Buy** or **Sell**
- Each entry shows: coin, type, quantity, price per unit, total, and date

> Crypto prices are fetched server-side via `sv_crypto_prices.lua` using the configured API (Binance, CoinCap, or CoinPaprika). The server caches prices and broadcasts updates to all connected clients. Crypto operations are **exempt from taxation**. Anti-double-spend protection ensures balance checks at the database level.

## Credit Score System

Every player has a credit score ranging from 0 to 1000 (default starting value: 500).

### How It Works

The credit score is modified by banking operations:

| Action | Score Change |
|---|---|
| Deposit | +2 |
| Withdrawal | -1 |
| Transfer sent | +1 |
| Transfer received | +1 |
| Account upgrade | +5 |

### Effects of Credit Score

- **Interest rate modulation** — Higher score means better interest rates
- **Account upgrade eligibility** — Premium requires a minimum credit score of 700
- The score is displayed as a progress bar on the dashboard

## Account Levels

There are two account levels: **Standard** and **Premium**.

### Comparison

| Feature | Standard | Premium |
|---|---|---|
| Interest Rate | 0.5% per cycle | 1.5% per cycle |
| Interest Cap | $5,000 per period | $20,000 per period |
| Max Transfer | $50,000 | $200,000 |
| Tax Reduction | 0% | 25% |

### Upgrading to Premium

1. Have a credit score of at least **700**
2. Have at least **$50,000** available
3. Click the **Upgrade** button on the dashboard
4. The upgrade fee is deducted from your account

## Progressive Taxation

Taxes are applied progressively on deposits, withdrawals, and transfers using configurable brackets.

### Default Tax Brackets

**Deposits:**

| Bracket | Rate |
|---|---|
| $0 - $10,000 | 0% |
| $10,000 - $50,000 | 2% |
| $50,000+ | 5% |

**Withdrawals:**

| Bracket | Rate |
|---|---|
| $0 - $10,000 | 0% |
| $10,000 - $50,000 | 1% |
| $50,000+ | 3% |

**Transfers:**

| Bracket | Rate |
|---|---|
| $0 - $10,000 | 0% |
| $10,000 - $50,000 | 1.5% |
| $50,000+ | 4% |

### Tax Exemptions

The following operations are **exempt from taxation**:

- Society account operations
- Joint account operations
- Savings account operations
- Crypto trading operations

### Premium Tax Reduction

Premium account holders receive a **25% reduction** on all taxes. For example, if the calculated tax is $400, a Premium player only pays $300.

## Interest System

Interest is credited automatically by a server-side cron running every `Config.Interest.interval` minutes (default: 60).

### How Interest Works

1. The cron runs at the configured interval
2. Only **online** players receive interest
3. The interest rate depends on the **account level** (Standard: 0.5%, Premium: 1.5%)
4. The rate is **modulated by credit score** — higher scores yield better rates
5. Interest earned is **capped** per reset period (Standard: $5,000, Premium: $20,000)
6. The cap resets every `Config.Interest.resetPeriod` minutes (default: 1440 = 24 hours)

> Savings accounts have a separate interest cron with their own rate and cap.

## Phone Notifications

If a compatible phone resource is installed and configured, players receive in-phone notifications for key events:

| Event | Notification |
|---|---|
| Transfer received | Amount and sender info |
| Payroll received | Amount and society name |
| Interest credited | Amount credited |
| Joint deposit | Amount and member name |
| Joint withdrawal | Amount and member name |
| Joint transfer | Amount and details |
| Joint member added | New member info |
| Joint member left | Departing member info |

Supported phone resources: `lb-phone`, `qs-smartphone`, `gksphone`.

> Notifications are only sent to **online** players. Each event type can be individually toggled in the config.

## Discord Webhook

When enabled and configured with a webhook URL, all banking operations are logged to a Discord channel:

- **Personal operations** — Deposits, withdrawals, transfers, interest, tax, upgrades
- **Society operations** — Deposits, withdrawals, transfers, payroll
- **Joint operations** — Deposits, withdrawals, transfers, member changes
- **Savings operations** — Deposits, withdrawals, locks, claims
- **Crypto operations** — Buys, sells

Each log entry is sent as a Discord embed with the operation details, amounts, and player information. Webhooks use a fire-and-forget approach and do not block gameplay.
