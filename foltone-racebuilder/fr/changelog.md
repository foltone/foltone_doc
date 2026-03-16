---
title: "Changelog"
description: "Historique des versions de Foltone Race Builder"
script: "foltone-racebuilder"
section: "Race Builder"
order: 99
version: "1.1.0"
---

# Changelog

## v1.1.0 — 2026-03-16

### Améliorations de l'éditeur
- Modification des propriétés de course (nom, véhicule, type, tours, max joueurs) depuis le gestionnaire de checkpoints
- L'édition d'une course ouvre maintenant directement le gestionnaire de checkpoints au lieu du mode placement
- Aperçu du marker départ/arrivée visible en temps réel pendant le placement du spawn
- Aperçu de la grille de départ amélioré avec des markers circulaires et des positions numérotées
- Positions de la grille éloignées de la ligne de départ (option `StartOffset` dans la config)
- Fermer le gestionnaire de checkpoints (X ou fermer) retourne maintenant au mode placement

### Corrections de bugs
- Correction des markers de checkpoint qui n'apparaissaient plus après un restart du script (compatibilité integer/float Lua 5.4 avec le native DrawMarker)
- Correction de l'erreur nil `restorePlayerBucket` causée par l'ordre de déclaration des fonctions
- Correction du callback `getRaces` qui ne retournait pas les données de checkpoints, causant une liste vide lors de l'édition
- Correction des incohérences d'état NUI lors de la navigation entre le formulaire et le gestionnaire de checkpoints
- Correction de l'artefact de preview checkpoint lors de la fermeture du gestionnaire
- Correction de `editorNpcPoint` non sauvegardé/restauré pendant le test de course
- Prévention des threads de boucle de placement dupliqués avec un flag de garde

## v1.0.0 — 2026-03-10
- Release initiale
- Système de création de courses complet
- Éditeur de checkpoints in-game
- Classements et chronomètres
- Support QB-Core et ESX
