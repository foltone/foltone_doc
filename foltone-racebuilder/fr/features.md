---
title: "Fonctionnalités"
description: "Aperçu des fonctionnalités du Race Builder"
script: "foltone-racebuilder"
section: "Race Builder"
order: 3
version: "1.0.0"
---

# Fonctionnalités — foltone_racebuilder

## Éditeur de courses (`/raceeditor`)

- **Caméra noclip** — Volez autour de la carte pour placer les checkpoints
- **Placement du PNJ** — Placez un PNJ interactif avec prévisualisation
- **Point de départ / Grille** — Grille de départ style F1 pour les courses multijoueur
- **Placement des checkpoints** — Clic gauche pour placer, clic droit pour attraper et déplacer
- **Taille ajustable** — Molette pour redimensionner chaque checkpoint individuellement
- **Rotation** — Touches Q/E pour orienter le checkpoint
- **Gestionnaire de checkpoints** — Touche Entrée pour réordonner, téléporter, supprimer
- **Test de course** — Testez directement depuis l'éditeur
- **Modification** — Chargez et modifiez n'importe quelle course sauvegardée
- **Détection AZERTY/QWERTY automatique**

## Modes de course

### Chrono solo
- Le joueur court seul contre la montre
- Meilleurs temps sauvegardés dans le classement
- Records personnels suivis par joueur

### Multijoueur (simultané)
- Système de lobby avec contrôles pour l'hôte
- Grille de départ style F1 avec positions décalées
- Suivi de position en temps réel
- Classement diffusé à tous les joueurs
- Écran de résultats final

### Les deux
- La course supporte les deux modes

## Fonctionnalités en course

- **Circuits en boucle** — La ligne de départ est aussi l'arrivée, avec plusieurs tours
- **Temps par tour** — Affiché dans le HUD
- **Route GPS** — Blip avec chemin GPS vers le prochain checkpoint
- **Gel au compte à rebours** — Véhicule immobilisé pendant le décompte
- **Détection sortie véhicule** — DQ après un délai configurable
- **Détection de mort** — La course se termine si le joueur meurt
- **Confirmation pour quitter** — F5 avec dialogue de confirmation
- **Courses instanciées** — Routing buckets FiveM pour des instances isolées

## Système de véhicules

- **Véhicule imposé** — La course peut exiger un modèle spécifique
- **Plusieurs véhicules** — Liste séparée par virgules, choix aléatoire ou choix du joueur
- **Choix libre** — Laissez vide pour n'importe quel véhicule
- **Sélecteur visuel** — Interface de sélection avec images depuis `config_vehicles.lua`

## Commandes admin

| Commande | Description |
|----------|-------------|
| `/raceeditor` | Ouvrir l'éditeur de courses (admin requis) |
| `/cancelrace [raceId]` | Annuler une course/lobby en cours |
| `/kickrace [playerId]` | Expulser un joueur de sa course |

## Systèmes d'interaction

Le script supporte plusieurs méthodes d'interaction (détection automatique) :

1. **ox_target** — Interaction 3D avec le PNJ
2. **qb-target** — Interaction 3D avec le PNJ
3. **Fallback touche E** — Interaction par proximité si aucun système de target n'est installé
