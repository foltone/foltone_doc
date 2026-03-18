---
title: "Changelog"
description: "Historique des versions de Foltone CCTV"
script: "foltone-cctv"
section: "Foltone CCTV"
order: 99
version: "1.0.0"
---

# Changelog — foltone_cctv

## 1.0.0 — 2026-03-18

- Sortie initiale
- 5 types de cameras : Standard, Dome, Bullet, Mini Bullet, PTZ Pro
- Boutique avec interface en grille de cartes, prix par type et images SVG
- Systeme de placement mural avec detection de surface normale
- Vue camera avec rotation souris, zoom scroll, raccourcis clavier
- Effets visuels CCTV : filtre timecycle, vignette, grain, scanlines, marqueurs d'angle
- Intensite des effets configurable via Config.CameraEffect
- Vision nocturne (touche N)
- Capture d'ecran via screenshot-basic
- Detection de mouvement avec rayon et cooldown configurables
- Destruction des cameras par tir/frappe (coups et armes configurables)
- Systeme de groupes de job : assigner des cameras a un job pour un acces partage
- Partage individuel par ID serveur du joueur
- Item tablette avec animation et prop
- Item poste de surveillance avec prop_cctv_unit_01
- Terminaux informatiques fixes
- Effets sonores pour toutes les actions camera
- Outil de debug camera (/cctv_debug) pour le calibrage des offsets
- Support multi-framework : ESX, QBCore, QBX
- Support multi-langue : Anglais, Francais
- Migration automatique de la base de donnees au demarrage
- Machine d'etat renforcee : tous les etats UI correctement proteges
