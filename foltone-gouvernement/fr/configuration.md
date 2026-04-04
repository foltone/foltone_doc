---
title: "Configuration"
description: "Configuration du script Gouvernement"
script: "foltone-gouvernement"
section: "Gouvernement"
order: 2
version: "2.0.0"
---

# Configuration — foltone_gouvernement

## Branches

Deux branches dans un seul job ESX :
- **Admin** (grades 0-4) : Stagiaire, Fonctionnaire, Secretaire d'Etat, Vice-Gouverneur, Gouverneur
- **Securite** (grades 5-7) : Garde, Agent de Securite, Chef de la Securite

```lua
Config.AdminGrades = { 0, 1, 2, 3, 4 }
Config.SecurityGrades = { 5, 6, 7 }
```

## Systeme fiscal (3 modes independants)

```lua
Config.Taxes = {
    paycheck = { enable = true, percent = 10 },          -- Taxe sur salaires
    society = { enable = true, percent = 5,               -- Cronjob societes
                intervalMinutes = 60,
                targetSocieties = { 'society_police', ... } },
    invoice = { enable = true, gradeRequired = 2 },       -- Fiches d'impot
}
```

## Nominations cross-job

```lua
Config.Nominations = {
    changeGrade = true,         -- Modifier le grade dans un autre job
    announcement = true,        -- Annonces officielles broadcast
    gradeRequired = 3,
    allowedJobs = { 'police', 'ambulance', 'mechanic' },
}
```

## Permis ESX

```lua
Config.Permits = {
    gradeRequired = 2,
    types = { { name = 'drive', label = 'Permis de conduire' }, ... },
}
```

## Armurerie securite

```lua
Config.Armory = {
    gradeRequired = 5,
    itemsList = {
        { type = 'weapon', grade = 5, name = 'WEAPON_PISTOL', label = 'Pistolet' },
        { type = 'weapon', grade = 7, name = 'WEAPON_CARBINERIFLE', label = 'Carabine' },
    },
}
```
