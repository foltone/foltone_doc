---
title: "Utilisation"
description: "Guide d'utilisation du script Ambulance"
script: "foltone-ambulancejob"
section: "Ambulance"
order: 3
version: "2.0.0"
---

# Utilisation — foltone_advanced_ambulancejob

## Système de mort (NUI)

Quand un joueur meurt :

1. **Phase 1** (5 min) : le joueur est au sol, écran NUI avec timer
2. **Phase 2** (10 min) : le bouton "Appeler les secours" apparaît, les ambulanciers reçoivent un blip
3. **Respawn** : si aucun ambulancier n'intervient, le joueur respawn à l'hôpital avec pénalités configurables

### Réanimation par un ambulancier
1. L'ambulancier s'approche du joueur mort
2. Menu F6 → Réanimer
3. Animation de réanimation (5 secondes)
4. Le joueur est réanimé sur place

## Menu F6

| Fonction | Description |
|----------|-------------|
| Soigner | Soin léger (régénère partiellement la vie) |
| Soin complet | Soin complet (régénère toute la vie) |
| Réanimer | Réanimer un joueur mort |
| Brancards | Poser/prendre un brancard, mettre un patient dessus |
| Escorte | Escorter un joueur |
| Props | Poser/retirer des objets (medikit, plots, barrières) |
| Pharmacie | Prendre des items médicaux |

## Brancards

1. Choisissez un type de brancard dans le menu
2. Le brancard apparaît devant vous
3. Approchez un joueur → mettez-le sur le brancard
4. Poussez le brancard (il vous suit)
5. Chargez le brancard dans l'ambulance (position configurée)
6. Changez la position : haut, bas, assis

## Pharmacie

1. Rendez-vous au marqueur de la pharmacie
2. Prenez des items médicaux (limite configurable)
3. Utilisez-les sur les patients

## Commandes admin

```
/revive [id]     -- Réanimer un joueur (admin)
/reviveall       -- Réanimer tous les joueurs (admin)
```

## Coffre, Vestiaire, Garage, Menu Patron

Fonctionnement identique aux autres jobs Foltone v2.0.

## Sécurité

- Rate limiting, validation serveur, logs Discord optionnels
