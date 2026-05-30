---
title: "Configuration"
description: "Reference de configuration du script de salon de tatouage"
script: "foltone-tattooshop"
section: "Tattoo Shop"
order: 2
version: "1.0.0"
---

# Configuration

Toute la configuration se fait dans le fichier `config.lua` a la racine de la ressource.

## Parametres generaux

| Option | Type | Defaut | Description |
|--------|------|--------|-------------|
| `Config.Framework` | string | `"esx"` | Selection du framework : `"esx"`, `"qbcore"` ou `"qbx"` |
| `Config.Locale` | string | `"en"` | Langue : `"fr"` ou `"en"` |
| `Config.Price` | number | `3000` | Prix par tatouage (achat ou retrait) |

## Parametres d'interaction

| Option | Type | Defaut | Description |
|--------|------|--------|-------------|
| `Config.InteractionType` | string | `"drawtext"` | Methode d'interaction : `"drawtext"`, `"ox_target"`, `"qb-target"` ou `"marker"` |
| `Config.InteractionDistance` | number | `3.0` | Distance a laquelle le joueur peut interagir avec le salon |

## Parametres du menu

| Option | Type | Defaut | Description |
|--------|------|--------|-------------|
| `Config.MenuPosition` | string | `"right"` | Position du menu a l'ecran : `"left"` ou `"right"` |
| `Config.MenuStyle` | string | `"glass"` | Style visuel du menu : `"glass"` ou `"solid"` |

## Couleurs de l'interface

Personnalisez les couleurs d'accentuation du menu via `Config.UIColors` :

| Cle | Defaut | Description |
|-----|--------|-------------|
| `accent` | `"#e67e22"` | Couleur d'accentuation principale |
| `accentLight` | `"#f39c12"` | Variante claire de l'accent |
| `accentDim` | `"#d35400"` | Variante sombre de l'accent |

## Positions des salons de tatouage

`Config.TattooShopPositions` definit les 6 emplacements des salons sous forme de coordonnees `vector3`. Chaque position genere un blip et une zone d'interaction.

## Parametres des blips

`Config.Blip` controle l'apparence du blip sur la carte :

| Cle | Description |
|-----|-------------|
| `sprite` | ID du sprite du blip |
| `color` | ID de la couleur du blip |
| `scale` | Taille du blip sur la carte |
| `display` | Mode d'affichage du blip |
| `name` | Libelle affiche sur la carte |

## Categories de zones corporelles

`Config.CategoriesLabel` definit les 7 zones corporelles utilisees comme onglets de navigation :

1. Tete
2. Torse
3. Cheveux
4. Bras gauche
5. Bras droit
6. Jambe gauche
7. Jambe droite

## Configuration de la tenue minimale

`Config.NakedSkinMale` et `Config.NakedSkinFemale` definissent les vetements minimaux appliques au joueur lorsqu'il entre dans le salon de tatouage, permettant aux tatouages d'etre entierement visibles sur le modele du personnage.

## Base de donnees des tatouages

`Config.TattoosCategories` contient la base de donnees complete des tatouages organisee par zone corporelle. Le script inclut **plus de 700 tatouages** avec leurs noms d'overlay, references de collection et assignations de zone.
