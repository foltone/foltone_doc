---
title: "Changelog"
description: "Historique des versions du script barbershop"
script: "foltone-barbershop"
section: "Barbershop"
order: 4
version: "1.2.0"
---

# Changelog

## v1.2.0

Ajout d'une couleur secondaire pour les cheveux et la barbe.

### Personnalisation
- Nouvelle **couleur secondaire** (`Couleur 2`) pour les cheveux et la barbe : la couleur principale et la couleur secondaire se règlent désormais indépendamment, permettant des dégradés et des mèches
- Nouvelle clé de locale `color2` (« Couleur 2 » / « Color 2 »)

## v1.1.0

Corrections du menu NUI, durcissement serveur et notification de mise à jour.

### Menu NUI
- Compatibilité avec les ressources renommées : utilisation de `GetParentResourceName()` au lieu d'un nom codé en dur, permettant de renommer le dossier de la ressource sans casser les callbacks NUI
- Correction du menu inutilisable à la seconde ouverture : l'état interne (focus clavier, page courante, contenu DOM) est désormais réinitialisé à chaque ouverture
- Correction de la « case fantôme » qui restait surlignée à la fermeture du menu
- Surlignage de sélection synchronisé avec le curseur de la souris : plus de décalage entre la case survolée et la case surlignée
- Plus de double surlignage : un seul élément peut être marqué actif à la fois
- Plus de scroll intempestif au survol souris : le `scrollIntoView` automatique est désactivé pour la navigation souris (conservé pour la navigation clavier)

### Sécurité serveur
- Validation des `chairId` côté serveur : seuls les identifiants de chaises définis dans `Config.Positions` sont acceptés, empêchant un client malveillant de réserver des chaises fantômes
- Le paiement exige désormais que le joueur soit effectivement assis sur une chaise : un appel `pay` sans chaise active est rejeté
- Ajout d'un rate-limit sur l'événement `releaseChair` (cohérence avec `takeChair` et `pay`)

### Configuration
- Nouvelle option `Config.AutoUpdateCheck` (défaut : `true`) pour activer ou désactiver la vérification automatique de mise à jour au démarrage du serveur
- Suppression de `Config.Debug` (n'était jamais utilisée)

### Notification de mise à jour
- Notification automatique de mise à jour : le serveur compare la version installée avec la dernière version publiée et affiche un message dans la console si une mise à jour est disponible

## v1.0.0

Version initiale.

- Menu barbershop basé sur NUI avec options de style glass/solid
- Support multi-framework : ESX Legacy, QBCore, QBX
- Intégration des ressources d'apparence : illenium-appearance, fivem-appearance, qb-clothing
- 5 catégories de personnalisation : Coiffure, Barbe, Sourcils, Yeux, Maquillage
- Grille de styles avec sélecteur de couleur et curseur d'opacité
- Navigation complète au clavier (flèches directionnelles, Entrée, Echap)
- Contrôles de rotation de la tête (touches A/Q/D) pour prévisualiser les modifications
- Prévisualisation en temps réel de toutes les modifications d'apparence
- 7 emplacements de barbershop préconfigurés avec blips sur la carte
- PNJ barbier avec animation de ciseaux
- Méthodes d'interaction configurables (ox_target, qb-target, qtarget, interact, drawtext, marker)
- Prix, couleurs de l'interface, position et style du menu configurables
- Support multilingue (anglais et français)
