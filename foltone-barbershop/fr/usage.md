---
title: "Utilisation"
description: "Comment utiliser le barbershop en jeu"
script: "foltone-barbershop"
section: "Barbershop"
order: 3
version: "1.1.0"
---

# Utilisation

## Trouver un Barbershop

Les emplacements des barbershops sont indiqués sur la carte par un **blip ciseaux** (sprite 71). Il y a 7 emplacements par défaut sur la carte.

## S'asseoir sur la chaise

Approchez-vous d'une chaise de barbier et interagissez avec elle selon la méthode d'interaction configurée (target, drawtext, marker, etc.). Votre personnage s'assiéra sur la chaise.

Une fois assis :

- Un **PNJ barbier** apparaît à côté de vous et joue une animation de ciseaux.
- La **caméra** se focalise sur la tête de votre personnage.
- Le **menu NUI** s'ouvre du côté configuré de l'écran.

## Catégories du menu

Le menu du barbershop comporte **5 catégories** :

| Catégorie | Ce qu'elle modifie |
|-----------|--------------------|
| **Coiffure** | Style de coiffure et couleur des cheveux |
| **Barbe** | Style de barbe, couleur et opacité |
| **Sourcils** | Style de sourcils, couleur et opacité |
| **Yeux** | Couleur des yeux |
| **Maquillage** | Style de maquillage, couleur et opacité |

### Contrôles par catégorie

Chaque catégorie propose les contrôles suivants selon le type :

- **Grille de styles** — parcourez visuellement tous les styles disponibles
- **Sélecteur de couleur** — choisissez la couleur principale
- **Curseur d'opacité** — ajustez la transparence (disponible pour la barbe, les sourcils et le maquillage)

Les modifications sont prévisualisées en temps réel sur votre personnage pendant la navigation.

## Contrôles clavier

| Touche | Action |
|--------|--------|
| **Flèches directionnelles** (Haut / Bas / Gauche / Droite) | Naviguer dans les styles et options |
| **Entrée** | Valider / sélectionner l'option actuelle |
| **A** ou **Q** | Tourner la tête vers la gauche |
| **D** | Tourner la tête vers la droite |
| **Echap** | Annuler et quitter le menu |

## Confirmer ou annuler

- **Bouton Payer** — confirme la coupe et facture le prix configuré (`Config.Price`, par défaut 75$). Votre nouvelle apparence est sauvegardée.
- **Annuler** (ou appuyer sur Echap) — restaure votre apparence d'origine avant de vous être assis. Aucun argent n'est prélevé.

Si vous n'avez pas assez d'argent, une notification vous en informera et la transaction ne sera pas effectuée.
