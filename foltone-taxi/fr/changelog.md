---
title: "Changelog"
description: "Historique des modifications du script Taxi"
script: "foltone-taxi"
section: "Taxi"
order: 4
version: "2.0.0"
---

# Changelog — foltone_taxi

## v2.0.0

Refonte complète avec architecture modulaire.

### Nouveautés
- Architecture modulaire (bridge/, client/modules/, server/modules/)
- Système de missions NPC refondu (pickup/dropoff/paiement distance/pénalité dégâts)
- Bridge ox_target et ox_inventory optionnels
- Multi-coffres avec permissions par grade
- Menus dual : RageUI ou ox_lib context
- Prise de service avec sync serveur
- Sécurité : rate limiting, validation serveur, plafond $5000/course
- Logs Discord optionnels
- Exports préservés : `startStopService()`, `cancelMission()`
- Escrow-friendly

## v1.0.0

Version initiale.
