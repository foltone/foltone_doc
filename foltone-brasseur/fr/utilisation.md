---
title: "Utilisation"
description: "Guide d'utilisation du script Brasseur"
script: "foltone-brasseur"
section: "Brasseur"
order: 3
version: "2.0.0"
---

# Utilisation — foltone_brasseur

## Prise de service

Appuyez sur **F6** → **Prendre/quitter le service**

## Pipeline de production

1. **Récolte** : Récoltez du houblon au point de récolte
2. **Transformation** : Transformez le houblon en bière blonde (1x) ou rousse (2x)
3. **Vente** : Vendez les bières au point de vente

Chaque étape utilise une barre de progression avec animation, annulable à tout moment.

## Menu F6

- Prise de service (toggle + annonce)
- Points d'intérêt (GPS)
- Facturer un joueur proche
- Annonces publiques

## Coffres

- **Avec ox_inventory** : stash drag & drop
- **Sans ox_inventory** : menu déposer/retirer
- 3 coffres filtrés par grade

## Vestiaire, Garage, Menu Patron

Fonctionnement identique au vigneron. Voir la documentation du vigneron pour les détails.

## Fichiers éditables

- `client/cl_editable.lua` : `OnVehicleSpawned()`, `SendBill()`
- `server/sv_editable.lua` : `OnHarvestComplete()`, `OnTransformComplete()`, `OnSellComplete()`
