---
title: "Utilisation"
description: "Guide d'utilisation du script Vigneron"
script: "foltone-vigneron"
section: "Vigneron"
order: 3
version: "2.0.0"
---

# Utilisation — foltone_vigneron

## Prise de service

1. Appuyez sur **F6** pour ouvrir le menu job
2. Sélectionnez **Prendre/quitter le service**
3. Une annonce est envoyée à tous les joueurs

## Pipeline de production

### Récolte
1. Rendez-vous au point de récolte (marqué sur la carte)
2. Interagissez (touche E ou ox_target)
3. Barre de progression avec animation — annulable
4. L'item est ajouté à votre inventaire

### Transformation
- Les matières premières sont consommées automatiquement
- Le produit transformé est créé

### Vente
- L'item est vendu, l'argent est réparti entre joueur et société

## Menu F6

| Option | Description |
|--------|-------------|
| Prise de service | Toggle on/off + annonce |
| Points d'intérêt | GPS vers les lieux de travail |
| Facturer | Facturer un joueur proche |
| Annonces | Annonce publique |

## Coffres

- **Avec ox_inventory** : ouverture stash classique (drag & drop)
- **Sans ox_inventory** : menu RageUI/ox_lib pour déposer/retirer
- Filtrés par grade

## Vestiaire

- **Tenue civile** : remet votre skin de base
- **Tenue de travail** : applique la tenue de votre grade

## Garage

- Sortir un véhicule depuis le menu
- Ranger en amenant le véhicule à la zone de suppression
- Un seul véhicule à la fois

## Menu Patron

| Fonction | Description |
|----------|-------------|
| Caisse société | Solde, déposer/retirer argent |
| Employés | Promouvoir / licencier |
| Salaires | Modifier le salaire par grade |
| Tenues | Assigner la tenue actuelle à un grade |

## Fichiers éditables (hors escrow)

- `client/cl_editable.lua` : `OnVehicleSpawned()`, `SendBill()`
- `server/sv_editable.lua` : `OnHarvestComplete()`, `OnTransformComplete()`, `OnSellComplete()`

## Sécurité

- Rate limiting sur toutes les actions serveur
- Validation job/grade côté serveur
- Montants de vente lus depuis Config serveur (anti-cheat)
- Logs Discord optionnels
