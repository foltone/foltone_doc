---
title: "Usage"
description: "How to use the barbershop in game"
script: "foltone-barbershop"
section: "Barbershop"
order: 3
version: "1.2.0"
---

# Usage

## Finding a Barbershop

Barbershop locations are marked on the map with a **scissors blip** (sprite 71). There are 7 locations across the map by default.

## Sitting in the Chair

Approach a barber chair and interact with it using the configured interaction method (target, drawtext, marker, etc.). Your character will sit down in the chair.

When seated:

- An **NPC barber** spawns next to you and plays a scissors animation.
- The **camera** focuses on your character's head.
- The **NUI menu** opens on the configured side of the screen.

## Menu Categories

The barbershop menu has **5 categories**:

| Category | What it changes |
|----------|----------------|
| **Hair** | Hairstyle, primary color, and secondary color |
| **Beard** | Beard style, primary color, secondary color, and opacity |
| **Eyebrows** | Eyebrow style, color, and opacity |
| **Eyes** | Eye color |
| **Makeup** | Makeup style, color, and opacity |

### Category Controls

Each category provides the following controls depending on the type:

- **Style grid** — browse all available styles visually
- **Color picker** — choose the primary color
- **Secondary color picker (`Color 2`)** — choose a secondary tint (available for hair and beard)
- **Opacity slider** — adjust transparency (available for beard, eyebrows, and makeup)

Changes are previewed in real time on your character as you browse.

## Keyboard Controls

| Key | Action |
|-----|--------|
| **Arrow keys** (Up / Down / Left / Right) | Navigate through styles and options |
| **Enter** | Validate / select the current option |
| **A** or **Q** | Rotate head to the left |
| **D** | Rotate head to the right |
| **Escape** | Cancel and exit the menu |

## Confirming or Cancelling

- **Pay button** — confirms the haircut and charges the configured price (`Config.Price`, default $75). Your new appearance is saved.
- **Cancel** (or pressing Escape) — restores your original appearance before you sat down. No money is charged.

If you do not have enough money, a notification will inform you and the transaction will not go through.
