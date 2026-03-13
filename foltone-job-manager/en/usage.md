---
title: "Usage"
description: "Job Manager script usage guide"
script: "foltone-job-manager"
section: "foltone_job_manager"
order: 3
version: "1.0.0"
---

# Usage — foltone_job_manager

## Overview

The script provides a NUI tablet interface allowing society bosses to manage their company: money, employees, salaries and transfers. Only players with the configured boss grade can access the interface.

## Accessing the Interface

1. Have the **boss grade** (or the grade configured in `bossGrade`) for the job
2. Go to the society **marker** (position configured in `config.lua`)
3. Press **E** to open the tablet interface

> The marker only appears if the player has the boss grade for the corresponding job.

## Money Tab

The money management tab allows you to:

- **View the balance** of the society
- **Add money** — Transfer personal money to the society account
- **Withdraw money** — Transfer money from the society to the player
- **Revenue chart** — View revenue over the last 10 days via a chart

> Revenue is automatically recorded every hour in the `server/data.json` file.

## Employees Tab

The employee management tab displays a list of all society employees with:

- **Last Name** and **First Name**
- Current **Grade**

### Available Actions

| Action | Description |
|--------|-------------|
| **Promote** | Increases the employee's grade by one level |
| **Demote** | Decreases the employee's grade by one level |
| **Fire** | Fires the employee (sets job to `unemployed`) |

> Actions only work if the target employee is **online**.

## Salaries Tab

This tab displays all job grades with their current salary. The boss can **edit the salary** for each grade directly in the input field.

> On ESX, salaries are updated in the `job_grades` database table.

## Transfers Tab

The boss can make transfers from the society account to:

### Transfer to a Player

1. Select type **"Person"**
2. Enter the **server ID** of the recipient player
3. Enter the **amount**
4. Click **"Process Transfer"**

### Transfer to Another Society

1. Select type **"Company"**
2. Choose the **target society** from the dropdown
3. Enter the **amount**
4. Click **"Process Transfer"**

> Only societies configured in `Config.SocietyList` appear in the list.

## Light / Dark Mode

The interface has a day/night toggle in the top right corner. The theme choice is saved in the browser's `localStorage` and persists between sessions.

## Revenue History

The script automatically records each society's balance **every hour** in the `server/data.json` file. This data feeds the revenue chart displayed in the Money tab.

## Available Events

### Server Events

```lua
-- Add money to the society
TriggerServerEvent("foltone_job_manager:addSocietyMoney", companyName, amount)

-- Remove money from the society
TriggerServerEvent("foltone_job_manager:removeSocietyMoney", companyName, amount)

-- Promote an employee
TriggerServerEvent("foltone_job_manager:promoteEmployee", companyName, targetIdentifier)

-- Demote an employee
TriggerServerEvent("foltone_job_manager:unpromoteEmployee", companyName, targetIdentifier)

-- Fire an employee
TriggerServerEvent("foltone_job_manager:fireEmployee", companyName, targetIdentifier)

-- Update a grade's salary
TriggerServerEvent("foltone_job_manager:updateSalary", companyName, gradeId, salary)

-- Transfer to a player
TriggerServerEvent("foltone_job_manager:transferSocietyMoneyToPlayer", companyName, targetId, amount)

-- Transfer to a society
TriggerServerEvent("foltone_job_manager:transferSocietyMoneyToSociety", companyName, targetCompany, amount)

-- Set a player's job
TriggerServerEvent("foltone_job_manager:setJob", targetId, companyName, grade)
```

### Server Callbacks

```lua
-- Get society data (balance, employees, grades, revenue)
TriggerServerFoltoneJMCallback("foltone_job_manager:getData", function(data)
    -- data.money.balance : balance
    -- data.money.revenueLastDays : array of revenue for the last 10 days
    -- data.employees : employee list
    -- data.grades : grade list with salaries
end, companyName)
```
