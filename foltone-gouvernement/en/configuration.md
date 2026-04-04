---
title: "Configuration"
description: "Government script configuration"
script: "foltone-gouvernement"
section: "Gouvernement"
order: 2
version: "2.0.0"
---

# Configuration — foltone_gouvernement

## Branches
- **Admin** (grades 0-4): Intern, Official, Secretary, Vice-Governor, Governor
- **Security** (grades 5-7): Guard, Security Agent, Security Chief

## Tax system (3 independent modes)
- **Paycheck tax**: auto-deduct % from ESX payday
- **Society cronjob**: periodic % deduction from society balances
- **Tax invoices**: manual billing via esx_billing

## Cross-job nominations
Governor can change grades in other jobs (police, EMS, etc.) + broadcast official announcements.

## ESX permits
Give/remove licenses (drive, weapon, DMV) via esx_license.

## Security armory
Grade-based weapons/items for security branch.
