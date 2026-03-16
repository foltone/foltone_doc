---
title: "Configuration"
description: "Référence de configuration du Race Builder"
script: "foltone-racebuilder"
section: "Race Builder"
order: 2
version: "1.1.0"
---

# Configuration — foltone_racebuilder

Toute la configuration se trouve dans `config.lua`. Ce fichier n'est pas chiffré et peut être modifié librement.

## Paramètres généraux

| Option | Défaut | Description |
|--------|--------|-------------|
| `Config.Locale` | `"en"` | Langue (`"en"` ou `"fr"`) |
| `Config.Framework` | `"ESX"` | Framework : `"ESX"`, `"QBCore"` ou `"standalone"` |
| `Config.Debug` | `true` | Activer les logs de debug dans la console serveur |
| `Config.AdminPermission` | `"admin"` | Permission ACE pour le check admin (mode standalone) |
| `Config.InteractionDistance` | `3.0` | Distance d'interaction avec le PNJ (fallback touche E) |
| `Config.CountdownSeconds` | `2` | Durée du compte à rebours avant le départ |
| `Config.DefaultMaxPlayers` | `10` | Nombre max de joueurs par défaut |
| `Config.NpcModel` | `"csb_janitor"` | Modèle du PNJ de course |

## Blip sur la carte

| Option | Défaut | Description |
|--------|--------|-------------|
| `Config.Blip.Sprite` | `315` | Icône du blip |
| `Config.Blip.Color` | `1` | Couleur du blip |
| `Config.Blip.Scale` | `0.8` | Taille du blip |
| `Config.Blip.Display` | `2` | Mode d'affichage |

## Apparence des checkpoints

| Option | Défaut | Description |
|--------|--------|-------------|
| `Config.Checkpoint.Diameter` | `10.0` | Diamètre par défaut (modifiable par checkpoint dans l'éditeur) |
| `Config.Checkpoint.NearHeight` | `4.0` | Hauteur du cylindre au sol |
| `Config.Checkpoint.Color` | `{r=45, g=110, b=185, a=200}` | Couleur des checkpoints normaux (RGBA) |
| `Config.Checkpoint.FinishColor` | `{r=53, g=154, b=71, a=255}` | Couleur du checkpoint d'arrivée (RGBA) |
| `Config.Checkpoint.CylinderZOffset` | `0.05` | Décalage Z du cylindre au sol |
| `Config.Checkpoint.IconZOffset` | `3.0` | Hauteur de l'icône au-dessus du checkpoint |
| `Config.Checkpoint.IconSizeRatio` | `0.2` | Taille de l'icône = diamètre × ratio |
| `Config.Checkpoint.IconType` | `2` | Type DrawMarker pour la flèche (2 = flèche) |
| `Config.Checkpoint.FinishIconType` | `4` | Type DrawMarker pour l'arrivée (4 = damier) |

## Blip GPS du checkpoint actif

| Option | Défaut | Description |
|--------|--------|-------------|
| `Config.CheckpointBlip.Sprite` | `854` | Sprite du blip GPS pendant la course |
| `Config.CheckpointBlip.Color` | `3` | Couleur du blip GPS |
| `Config.CheckpointBlip.Scale` | `0.9` | Taille du blip GPS |

## Grille de départ (multijoueur)

| Option | Défaut | Description |
|--------|--------|-------------|
| `Config.StartGrid.Columns` | `2` | Colonnes (2 = style F1 côte à côte) |
| `Config.StartGrid.ColumnSpacing` | `3.5` | Espacement latéral entre colonnes (mètres) |
| `Config.StartGrid.RowSpacing` | `8.0` | Espacement entre rangées (mètres) |
| `Config.StartGrid.StaggerOffset` | `4.0` | Décalage de la colonne droite (mètres) |
| `Config.StartGrid.StartOffset` | `12.0` | Distance entre la ligne de départ et la première rangée de voitures (mètres) |
| `Config.StartGrid.PreviewSlots` | `10` | Nombre de slots affichés dans l'éditeur |

## Paramètres de course

| Option | Défaut | Description |
|--------|--------|-------------|
| `Config.Race.ExitVehicleTimeout` | `10` | Secondes avant DQ si hors véhicule |
| `Config.Race.QuitKey` | `166` | Touche pour quitter (166 = F5) |

## Système de notification

Modifiez `Config.Notification` dans `config.lua` pour utiliser votre propre système :

```lua
Config.Notification = function(message)
    -- Par défaut : foltone_ultra_hud
    exports.foltone_ultra_hud:Notify(message)

    -- Exemple : notification GTA native
    -- SetNotificationTextEntry("STRING")
    -- AddTextComponentString(message)
    -- DrawNotification(false, false)

    -- Exemple : ox_lib
    -- lib.notify({ description = message })
end
```

## Personnalisation framework

Modifiez `client/cl_editable.lua` et `server/sv_editable.lua` pour adapter à votre framework. Ces fichiers ne sont pas chiffrés.

### sv_editable.lua

Contient les fonctions de vérification admin, d'identification joueur et de récupération de nom :

- `IsPlayerAdminServer(source)` — Retourne true si le joueur est admin
- `GetPlayerIdentifierServer(source)` — Retourne l'identifiant unique du joueur
- `GetPlayerNameServer(source)` — Retourne le nom du joueur
