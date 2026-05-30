---
title: "Configuration"
description: "Tattoo shop script configuration reference"
script: "foltone-tattooshop"
section: "Tattoo Shop"
order: 2
version: "1.0.0"
---

# Configuration

All configuration is done in the `config.lua` file at the root of the resource.

## General Settings

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `Config.Framework` | string | `"esx"` | Framework selection: `"esx"`, `"qbcore"`, or `"qbx"` |
| `Config.Locale` | string | `"en"` | Language: `"fr"` or `"en"` |
| `Config.Price` | number | `3000` | Price per tattoo (buy or remove) |

## Interaction Settings

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `Config.InteractionType` | string | `"drawtext"` | Interaction method: `"drawtext"`, `"ox_target"`, `"qb-target"`, or `"marker"` |
| `Config.InteractionDistance` | number | `3.0` | Distance at which the player can interact with the shop |

## Menu Settings

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `Config.MenuPosition` | string | `"right"` | Menu position on screen: `"left"` or `"right"` |
| `Config.MenuStyle` | string | `"glass"` | Menu visual style: `"glass"` or `"solid"` |

## UI Colors

Customize the accent colors of the tattoo shop menu via `Config.UIColors`:

| Key | Default | Description |
|-----|---------|-------------|
| `accent` | `"#e67e22"` | Primary accent color |
| `accentLight` | `"#f39c12"` | Light accent variant |
| `accentDim` | `"#d35400"` | Dark/dim accent variant |

## Tattoo Shop Positions

`Config.TattooShopPositions` defines the 6 tattoo shop locations as `vector3` coordinates. Each position spawns a blip and an interaction zone.

## Blip Settings

`Config.Blip` controls the map blip appearance:

| Key | Description |
|-----|-------------|
| `sprite` | Blip sprite ID |
| `color` | Blip color ID |
| `scale` | Blip size on the map |
| `display` | Blip display mode |
| `name` | Label shown on the map |

## Body Zone Categories

`Config.CategoriesLabel` defines the 7 body zones used as navigation tabs:

1. Head
2. Torso
3. Hair
4. Left Arm
5. Right Arm
6. Left Leg
7. Right Leg

## Naked Skin Configuration

`Config.NakedSkinMale` and `Config.NakedSkinFemale` define the minimal clothing applied to the player when entering the tattoo shop, allowing tattoos to be fully visible on the character model.

## Tattoo Database

`Config.TattoosCategories` contains the full tattoo database organized by body zone. The script includes **700+ tattoos** with their overlay names, collection references, and zone assignments.
