---
title: "Installation"
description: "Installation du script Job Builder"
script: "foltone-job-builder"
section: "Job Builder"
order: 1
version: "2.0.0"
---

# Installation — foltone_job_builder

## Prerequis

- **ESX Legacy**, **ox_lib**, **oxmysql**, **esx_society**, **esx_addonaccount**
- Optionnels : **ox_inventory** (coffres stash), **ox_target** (interactions 3D), **esx_addoninventory**, **esx_billing**

## Configuration serveur

```ini
ensure foltone_job_builder
```

## Verification

1. Connectez-vous en tant qu'admin
2. Tapez `/jb` pour le builder RageUI ou `/jbnui` pour le NUI builder
3. Console : `[Foltone Job Builder] v2.0.0 loaded`
