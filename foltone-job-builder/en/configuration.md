---
title: "Configuration"
description: "Job Builder script configuration"
script: "foltone-job-builder"
section: "Job Builder"
order: 2
version: "2.0.0"
---

# Configuration — foltone_job_builder

```lua
Config.AdminGroups = { 'admin', 'superadmin' }
Config.UseOxInventory = GetResourceState('ox_inventory') ~= 'missing'
```

Creates complete jobs in-game: grades, multi-storage, garage, processing pipeline, announcements, boss, locker, duty.
