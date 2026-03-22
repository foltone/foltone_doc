---
title: "Changelog"
description: "Historique des versions de Foltone CCTV"
script: "foltone-cctv"
section: "Foltone CCTV"
order: 99
version: "1.1.0"
---

# Changelog — foltone_cctv

## 1.1.0 — 2026-03-22

### Ajouts
- Accessoires boutique : tablette et moniteur de surveillance disponibles a l'achat
- Le moniteur de surveillance est maintenant un item placable (comme les cameras) qui ouvre l'interface quand on interagit avec
- Lightbox captures : cliquez sur une capture pour la voir en plein ecran avec nom de camera et date
- Parametres d'offset `propPitch` et `propRoll` pour la correction de rotation des props
- Champs `wallOffset` et `image` dans la configuration des types de cameras
- Section `Config.ShopAccessories` pour les accessoires en boutique

### Modifications
- Types de cameras mis a jour : 4 types (Standard, Bullet, Mini Bullet, Shop Cam) remplacant les 5 precedents
- Les images de la boutique utilisent des fichiers PNG depuis le champ `image` du config au lieu de SVG
- Systeme de notification refactorise : `ClientNotification` dans config.lua (cote client, personnalisable) + le serveur declenche un event client
- SQL getCameras optimise : remplacement des requetes N+1 par une seule sous-requete IN
- install.sql mis a jour avec la table stations, toutes les colonnes et les index
- Delai d'achat reduit entre les achats en boutique
- Toutes les chaines UI traduites en anglais

### Corrections
- Correction de requestCapture qui ne validait pas la propriete/acces a la camera
- Correction de destroyCamera permettant l'abus a distance (ajout verification de distance)
- Correction de vulnerabilite XSS : remplacement des onclick inline par data-attributes + event delegation
- Correction de la fuite memoire motionCooldowns quand les cameras sont supprimees
- Correction des entrees d'acces non nettoyees quand une camera est supprimee
- Correction des migrations ALTER TABLE utilisant async au lieu de await
- Correction du mismatch CAM_TYPE_ICONS (supprime dome/ptz, ajoute shop_cam)
- Correction de l'alignement icone+texte des boutons dans toute l'interface
- Correction de l'achat du moniteur en boutique qui donnait le mauvais item
- Correction de l'erreur de contenu mixte HTTPS de screenshot-basic
- Commande cctv_debug deplacee derriere une verification de permission admin

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
