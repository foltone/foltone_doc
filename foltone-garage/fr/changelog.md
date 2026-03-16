---
title: "Changelog"
description: "Historique des versions de Foltone Garage"
script: "foltone-garage"
section: "Foltone Garage"
order: 99
version: "2.0.0"
---

# Changelog

## v2.0.0 — 2026-03-16

### Ajouts
- Refonte complete du script (architecture, securite, design)
- Nouveau panel NUI avec 4 onglets (vehicules, ranger, fourriere, label)
- Menu RageUI en fallback configurable (`Config.MenuType`)
- Support multi-target : ox_target, qb-target, interact, drawtext, marker
- Systeme de fourriere avec prix dynamique (basePrice + pricePerHour, plafond min/max)
- Labels personnalises pour les vehicules (NUI exclusif, 30 caracteres max)
- Vehicules de service pour les garages job (liste de modeles spawnable)
- Support QBX natif en plus d'ESX et QBCore
- Callback custom securise (`RegisterServerFoltoneGRCallback`)
- Rate limiting sur tous les events serveur
- Validation serveur sur toutes les operations

### Modifications
- Configuration des garages deplacee dans `config_garage.lua` (separation config/logique)
- Prix de fourriere calcule cote serveur (plus de manipulation possible cote client)
- Garages par type de vehicule (car, boat, plane, heli) avec activation individuelle
