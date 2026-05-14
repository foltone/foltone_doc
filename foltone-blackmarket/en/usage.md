---
title: "Usage"
description: "Usage guide for foltone_blackmarket script"
script: "foltone-blackmarket"
section: "Blackmarket"
order: 3
version: "1.0.0"
---

# Usage

## Finding the van

The van spawns automatically based on the server's spawn cycle (`FirstSpawnDelaySeconds` then `LifetimeSeconds` / `RespawnCooldownSeconds`). It picks a random location from `Config.SpawnLocations`.

There are several ways to find it :

1. **Encrypted phone item** : the player uses `bm_encrypted_phone` from their inventory. A flashing blip 161 appears for 20 seconds (rough zone), then the precise van location for 60 seconds.
2. **Permanent blip** : if `Config.ShowBlip = true`. Optionally gated by `Config.RequireContactItem`.
3. **Roleplay** : the player learns the location through other players, contacts, etc.

## Interacting with the dealer

Approach the van. Depending on `Config.TargetSystem` :

- **ox_target / qb-target / qtarget** : a target option appears around the dealer (a 2m×2m box around the seller seat).
- **none / fallback** : a textUI prompts to press **E** at close range.

The shop menu opens (RageUI in-game or NUI HTML, depending on `Config.MenuType`).

## Purchase flow

The menu offers several categories :

1. **Weapons** — pistols, SMG, shotgun, etc. Each has its 3D preview, stats and a scratched serial marker.
2. **Items** — ammunition.
3. **Protection** — body armor, heavy armor, medkit.
4. **Customs** — components (suppressor, scope, extended clip...) and tints. Only weapons the player **already owns** appear here.

3D preview : when an item is highlighted, the model is displayed in front of the van. **Mouse wheel** zooms in/out.

For customs : a weapon selector with arrows lets you switch between customizable weapons you own.

## Risk and heat

- Every purchase has a **10% chance** (configurable) of triggering a police alert with the buyer's coordinates.
- Each purchase adds **heat** to the van. Above the threshold (default 8), the van automatically despawns and police receive a temporary blip.
- A police officer entering an 80m radius **causes the dealer to flee** (van + ped disappear).

## Admin commands

The `bm_van` command is available to admins (ACE or group). It requires `Bridge.IsAdmin` to return true.

| Command | Description |
|---|---|
| `bm_van spawn [idx]` | Forces a van spawn (optional location index) |
| `bm_van despawn` | Forces immediate despawn |
| `bm_van status` | Shows van state (location, heat) in console |

## Permissions

| Action | Requirement |
|---|---|
| Find via permanent blip | `Config.ShowBlip = true` |
| Find via phone | Item `bm_encrypted_phone` in inventory |
| Buy a weapon | Required money + minimum reputation if `minRep > 0` |
| Buy a custom | Already own the weapon + sufficient money |
| `bm_van` commands | ACE `foltone_blackmarket.admin` or group in `Config.AdminGroups` |

## Reputation (optional)

If you define a `GetPlayerReputation(src)` function in a server file, items with `minRep > 0` will be locked for players below threshold. Without that function defined, no reputation gate is applied.

## Updating

On every startup, the server checks against the remote version. If a newer version is available, a yellow message appears in the console with instructions.
