---
title: "Changelog"
description: "Historique des modifications du script Ambulance"
script: "foltone-ambulancejob"
section: "Ambulance"
order: 4
version: "2.0.0"
---

# Changelog — foltone_advanced_ambulancejob

## v2.0.0

Refonte modulaire avec toutes les features ambulance préservées.

### Nouveautés
- Architecture modulaire (bridge/, client/modules/, server/modules/)
- Bridge ox_target et ox_inventory optionnels
- Multi-coffres avec permissions par grade
- Menus dual : RageUI ou ox_lib context
- Prise de service avec sync serveur
- Sécurité : rate limiting, validation serveur
- Logs Discord optionnels
- Escrow-friendly

### Préservé
- Système de mort NUI complet (timers, respawn, pénalités)
- Brancards (3 types, 3 positions, animations)
- Soins (léger, complet, réanimation)
- Pharmacie
- Props, escorte
- Garage hélicoptère
- Commandes admin /revive, /reviveall

## v1.0.0

Version initiale.
