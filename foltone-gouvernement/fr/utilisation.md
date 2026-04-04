---
title: "Utilisation"
description: "Guide d'utilisation du script Gouvernement"
script: "foltone-gouvernement"
section: "Gouvernement"
order: 3
version: "2.0.0"
---

# Utilisation — foltone_gouvernement

## Menu F6

Le menu F6 s'adapte selon la branche :

### Branche Admin (grades 0-4)
| Fonction | Grade min | Description |
|----------|-----------|-------------|
| Gestion fiscale | 2 | Voir recettes, modifier taux, envoyer fiches |
| Nominations | 3 | Nommer/revoquer chefs de service |
| Permis | 2 | Donner/retirer permis ESX |
| Facturer | 0 | Facturer un joueur |

### Branche Securite (grades 5-7)
| Fonction | Grade min | Description |
|----------|-----------|-------------|
| Menottes | 6 | Menotter/demenotter un joueur |
| Escorte | 6 | Escorter un joueur menotte |
| Armurerie | 5 | Prendre armes/equipement |

## Systeme fiscal

### Taxe salaires
Prelevement automatique sur chaque paie ESX. Taux modifiable par le gouverneur.

### Taxe societes
Cronjob automatique qui preleve un % sur le solde de chaque societe ciblee.

### Fiches d'impot
Le secretaire/gouverneur envoie une facture manuelle au patron d'une societe via esx_billing.

## Nominations

Le gouverneur choisit un job autorise, un joueur, et un grade. Le changement s'applique immediatement (en ligne) ou en BDD (hors ligne).

## Annonces officielles

Broadcast a tous les joueurs avec titre et message personnalises.
