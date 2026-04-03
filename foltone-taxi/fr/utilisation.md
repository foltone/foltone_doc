---
title: "Utilisation"
description: "Guide d'utilisation du script Taxi"
script: "foltone-taxi"
section: "Taxi"
order: 3
version: "2.0.0"
---

# Utilisation — foltone_taxi

## Système de missions

### Déroulement d'une course

1. **Activation** : Menu F6 → Activer le service
2. **Attente** : Montez dans un taxi, une mission arrive après 10-20 secondes
3. **Pickup** : Un PNJ apparaît à un point de rendez-vous (blip sur la carte)
4. **Récupération** : Approchez-vous du PNJ, il monte dans le véhicule automatiquement
5. **Transport** : Un nouveau blip de destination apparaît
6. **Arrivée** : Arrêtez-vous près de la destination (vitesse < 3 km/h)
7. **Paiement** : Le PNJ descend, vous recevez votre paiement

### Calcul du paiement

- **Base** : Distance parcourue × prix par mètre (configurable)
- **Société** : Un pourcentage est reversé à la société (par défaut 30%)
- **Pénalité** : Si le véhicule subit des dégâts pendant la course, une pénalité est déduite

### Menu F6

| Option | Description |
|--------|-------------|
| Prise de service | Toggle duty + annonce |
| Activer le service | Démarrer/arrêter la recherche de courses |
| Annuler la course | Annuler la mission en cours |
| Facturer | Facturer un joueur proche |
| Annonces | Annonce publique |

### Exports

Vous pouvez contrôler le service depuis d'autres scripts :

```lua
-- Toggle le service
local isActive = exports["foltone_taxi"]:startStopService()

-- Annuler la mission
exports["foltone_taxi"]:cancelMission()
```

## Coffre, Vestiaire, Garage, Menu Patron

Fonctionnement identique aux autres jobs Foltone. Voir la documentation du vigneron pour les détails.

## Sécurité

- Rate limiting sur les actions serveur
- Plafond anti-cheat de **$5000 par course** côté serveur
- Validation du job côté serveur
- Logs Discord optionnels
