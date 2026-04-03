---
title: "Utilisation"
description: "Guide d'utilisation du script Police"
script: "foltone-policejob"
section: "Police"
order: 3
version: "2.0.0"
---

# Utilisation — foltone_policejob

## Menu F6

Le menu F6 donne accès à toutes les fonctions de police :

| Fonction | Description |
|----------|-------------|
| Menottes | Menotter/démenotter le joueur le plus proche |
| Escorte | Escorter un joueur menotté |
| Fouille | Fouiller l'inventaire d'un joueur |
| Amendes | Infliger une amende par catégorie |
| Prison | Envoyer en GAV ou en prison (timer NUI) |
| K9 | Faire apparaître/disparaître le chien, attaquer, suivre, rechercher |
| Props | Poser/retirer des objets (plots, barrières, gazebo) |
| Codes radio | Envoyer des codes radio à tous les policiers |
| Renforts | Envoyer une demande de renfort avec blip |
| Armurerie | Prendre des armes/items selon le grade |
| Factures | Facturer un joueur |

## Système de prison

### GAV (Garde à Vue)
1. Menottez le suspect
2. Amenez-le au commissariat
3. Menu F6 → Prison → GAV
4. Choisissez la cellule et la durée
5. Le suspect est téléporté en cellule avec tenue de prisonnier

### Prison
1. Menu F6 → Prison → Prison
2. Définissez la durée
3. Le joueur est téléporté à la prison avec timer NUI
4. À la fin du timer, il est libéré automatiquement

## K9 (Chien de police)

- **Spawn/despawn** : faire apparaître ou disparaître le K9
- **Siège** : le K9 monte dans le véhicule (configurable)
- **Suivre** : le K9 suit le policier
- **Attaquer** : le K9 attaque le joueur le plus proche
- **Rechercher** : le K9 recherche (animation)

## Coffre, Vestiaire, Garage, Menu Patron

Fonctionnement identique aux autres jobs Foltone v2.0.

## Sécurité

- Rate limiting sur toutes les actions serveur
- Validation du job côté serveur
- Logs Discord optionnels
