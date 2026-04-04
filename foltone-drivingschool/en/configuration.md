---
title: "Configuration"
description: "Configuration guide for foltone_drivingschool script"
script: "foltone-drivingschool"
section: "Driving School"
order: 2
version: "1.0.0"
---

# Configuration

All configuration is done in the `config.lua` file.

## General settings

```lua
Config.Locale = 'en'
Config.PedModel = 's_m_y_cop_01'       -- Instructor NPC model
Config.SchoolLocation = vector3(228.46, -1394.87, 30.59) -- Driving school position
```

## Map blip

```lua
Config.Blip = {
    sprite = 545,
    color = 3,
    scale = 0.8,
    label = "Driving School"
}
```

## Exam types

### Theory exam (NUI)

```lua
Config.TheoryExam = {
    passingScore = 80,          -- Minimum passing score (%)
    questionsPerExam = 20,      -- Questions per exam
    timePerQuestion = 30,       -- Time per question (seconds)
    price = 500,                -- Exam price
}
```

### Exam questions

```lua
Config.Questions = {
    {
        question = "What is the speed limit in urban areas?",
        answers = { "20 mph", "30 mph", "40 mph", "50 mph" },
        correct = 2,  -- Index of the correct answer
    },
    {
        question = "What does an amber traffic light mean?",
        answers = { "Speed up", "Stop if safe to do so", "Right of way", "Slow down" },
        correct = 2,
    },
    -- Add as many questions as needed...
}
```

## Practical exams

### Car exam

```lua
Config.CarExam = {
    license = "drive",
    vehicle = "sultan",           -- Vehicle model
    price = 1500,                 -- Exam price
    maxErrors = 3,                -- Max errors before failure
    speedLimit = 80,              -- Speed limit (km/h)
    checkpoints = {
        vector3(230.0, -1390.0, 30.0),
        vector3(250.0, -1350.0, 30.0),
        -- Add checkpoints...
    },
}
```

### Motorcycle exam

```lua
Config.BikeExam = {
    license = "drive_bike",
    vehicle = "bati",
    price = 1000,
    maxErrors = 3,
    speedLimit = 90,
    checkpoints = { --[[ ... ]] },
}
```

### Truck exam

```lua
Config.TruckExam = {
    license = "drive_truck",
    vehicle = "mule",
    price = 3000,
    maxErrors = 2,
    speedLimit = 60,
    checkpoints = { --[[ ... ]] },
}
```

### Error criteria

Errors are counted for:

| Infraction | Errors |
|---|---|
| Speeding | +1 |
| Vehicle collision | +1 |
| Pedestrian collision | +2 (immediate failure) |
| Missed checkpoint | +1 |
| Vehicle damage (threshold) | +1 |

## Notifications

```lua
Config.Notification = function(msg)
    ESX.ShowNotification(msg)
end
```
