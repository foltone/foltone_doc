---
title: "Utilisation"
description: "Guide d'utilisation du script Mechanic"
script: "foltone-mechanic"
section: "Mechanic"
order: 3
version: "2.0.0"
---

# Utilisation — foltone_mechanic

## Customisation de véhicules

1. Amenez un véhicule au point de custom (marqué sur la carte)
2. Interagissez pour ouvrir le menu de personnalisation
3. Choisissez les modifications : peinture, mods, néons, roues, etc.
4. Chaque modification a un prix basé sur la config
5. Le pourcentage de bénéfice est ajustable (grade 3+)
6. Confirmez et envoyez la facture au client

### Conditions pour le custom
- Le véhicule doit être suffisamment propre
- Le véhicule ne doit pas être trop endommagé
- Certains points de custom peuvent être limités par classe/modèle de véhicule

### Facturation client
- Le mécanicien fait les customs et définit le prix
- Le client reçoit une facture (touche Y pour accepter, N pour refuser)
- L'argent est réparti entre le joueur et la société

## Missions de remorquage

1. Ouvrez le menu F6 → Activer les missions
2. Un véhicule en panne apparaît quelque part sur la carte
3. Rendez-vous au point avec votre flatbed/towtruck
4. Attachez le véhicule au plateau
5. Livrez-le au point de dépôt
6. Récompense aléatoire (joueur + société)

### Commandes flatbed
- Approchez un véhicule → il s'attache au plateau
- Ré-interagissez → il se détache

## Menu F6

| Option | Description |
|--------|-------------|
| Prise de service | Toggle duty + annonce |
| Missions | Activer/désactiver + arrêter la mission en cours |
| Annonces | Annonce publique |
| Facturer | Facturer un joueur proche |

## Coffre, Vestiaire, Garage, Menu Patron

Fonctionnement identique aux autres jobs Foltone v2.0.

## Sécurité

- Rate limiting sur toutes les actions serveur
- Validation du job côté serveur
- Logs Discord optionnels
