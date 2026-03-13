---
title: "Utilisation"
description: "Guide d'utilisation du script Elevator Builder"
script: "foltone-elevator-builder"
section: "foltone_elevator_builder"
order: 3
version: "1.0.0"
---

# Utilisation — foltone_elevator_builder

## Fonctionnement général

Elevator Builder permet de créer et gérer des ascenseurs en jeu via une interface NUI. Les ascenseurs sont composés d'étages avec un nom et une position. Les joueurs peuvent se téléporter entre les étages via un panneau d'ascenseur interactif.

## Menu d'administration

### Ouvrir le menu

Tapez `/fab` dans le chat pour ouvrir le menu d'administration NUI.

### Créer un ascenseur

1. Ouvrez le menu admin (`/fab`)
2. Cliquez sur **"Créer un ascenseur"**
3. Définissez le **nom de l'ascenseur**
4. Choisissez le **nombre d'étages** (1 à 9)
5. Pour chaque étage :
   - Cliquez sur **"Définir le nom"** et saisissez le nom (ex: "RDC", "Étage 1", "Toit")
   - Cliquez sur **"Définir la position"** — le menu se ferme, votre position actuelle est enregistrée
6. Cliquez sur **"Créer l'ascenseur"** pour valider

> Les marqueurs de prévisualisation s'affichent en vert pendant la création pour vérifier les positions.

### Modifier un ascenseur

1. Ouvrez le menu admin (`/fab`)
2. Cliquez sur **"Modifier un ascenseur"**
3. Sélectionnez l'ascenseur à modifier
4. Vous pouvez :
   - **Renommer l'ascenseur** — Cliquez sur le bouton de renommage
   - **Modifier un étage** — Sélectionnez l'étage, puis modifiez son nom ou sa position
   - **Supprimer un étage** — Sélectionnez l'étage, puis cliquez sur "Supprimer"
   - **Supprimer l'ascenseur** — Supprime l'ascenseur et tous ses étages

### Panneau de configuration

Depuis le menu admin, accédez au panneau de configuration pour modifier en temps réel :

- Couleur et type du marqueur
- Distances de rendu et d'interaction
- Activation/désactivation de ox_target
- Animation de téléportation (durée, fondu)
- Sons (activation, volume)

Les changements sont appliqués immédiatement pour tous les joueurs.

## Utilisation joueur

### Sans ox_target (touche E)

1. Approchez-vous d'un marqueur d'ascenseur (distance configurable, par défaut 1.0m)
2. Le texte **"Appuyez sur E pour accéder à l'ascenseur"** s'affiche
3. Appuyez sur **E**
4. Le panneau d'ascenseur NUI s'ouvre, affichant l'étage actuel et les étages disponibles
5. Cliquez sur l'étage souhaité pour vous y téléporter

### Avec ox_target

1. Visez un point d'ascenseur avec ox_target
2. Cliquez sur l'option d'ascenseur
3. Le panneau s'ouvre — sélectionnez votre étage

### Fermer le panneau

Appuyez sur **Échap** ou cliquez sur le bouton de fermeture.

## Interface du panneau d'ascenseur

Le panneau affiche :
- L'**étage actuel** en temps réel (indicateur digital)
- La **liste des étages** disponibles avec leurs noms
- Des **boutons** pour chaque étage

L'indicateur d'étage se met à jour automatiquement lorsque le joueur se déplace entre les positions d'étages.

## Animation de téléportation

Quand l'animation est activée, le processus est :
1. Son de fermeture des portes
2. Fondu noir
3. Téléportation + son de déplacement
4. Fondu clair + son d'arrivée (ding)
5. Son d'ouverture des portes

## Stockage des données

Les ascenseurs sont sauvegardés dans le fichier `json/data.json`. Ce fichier est lu/écrit automatiquement par le serveur. Format :

```json
[
    {
        "label": "Ascenseur Principal",
        "floors": [
            { "idEtage": 1, "name": "RDC", "position": { "x": 0.0, "y": 0.0, "z": 0.0 } },
            { "idEtage": 2, "name": "Étage 1", "position": { "x": 0.0, "y": 0.0, "z": 10.0 } }
        ]
    }
]
```

## Exports disponibles

Le script expose des exports pour l'intégration avec d'autres scripts :

### openElevator

Ouvre le panneau d'ascenseur pour un ascenseur spécifique.

```lua
-- Ouvre l'ascenseur avec l'ID 1
local success = exports['foltone-elevator-builder']:openElevator(1)
```

### teleportToFloor

Téléporte directement le joueur à un étage spécifique.

```lua
-- Téléporte à l'étage 2 de l'ascenseur 1
local success = exports['foltone-elevator-builder']:teleportToFloor(1, 2)
```

### getElevators

Récupère la liste de tous les ascenseurs et leurs étages.

```lua
local elevators = exports['foltone-elevator-builder']:getElevators()
-- Retourne : { { id = 1, label = "...", floors = { { idEtage = 1, name = "RDC" }, ... } }, ... }
```

### getCurrentFloor

Récupère le nom de l'étage le plus proche du joueur.

```lua
local floorName = exports['foltone-elevator-builder']:getCurrentFloor()
-- Retourne : "RDC" ou nil si aucun étage à proximité
```
