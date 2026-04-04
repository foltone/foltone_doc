---
title: "Utilisation"
description: "Guide d'utilisation du script foltone_gruppe6"
script: "foltone-gruppe6"
section: "Gruppe6"
order: 3
version: "1.0.0"
---

# Utilisation de foltone_gruppe6

## Systeme dual : Metier + Braquage

Ce script propose deux mecaniques independantes accessibles selon le role du joueur.

---

## Partie Metier (Employes Gruppe6)

### Prendre son service

1. Rendez-vous au point de prise de service avec le job `gruppe6`
2. Ouvrez le menu RageUI
3. Selectionnez **Prendre le service** pour enfiler la tenue

### Missions

1. Une fois en service, acceptez une mission depuis le menu
2. Montez dans le vehicule blinde au point indique
3. Suivez les points GPS pour effectuer la livraison / collecte
4. Retournez au depot pour valider la mission et recevoir votre recompense

### Fin de service

Retournez au point de service et selectionnez **Quitter le service** pour retirer la tenue.

---

## Partie Braquage (Criminels)

### Conditions requises

- Un nombre minimum de policiers doit etre en service (configurable)
- Le joueur doit posseder l'item explosif dans son inventaire
- Le cooldown du dernier braquage doit etre ecoule

### Deroulement

1. Rendez-vous pres du fourgon blinde
2. Interagissez pour lancer le braquage
3. Utilisez l'explosif sur la porte arriere du fourgon
4. Recuperez l'argent a l'interieur
5. Fuyez avant l'arrivee de la police

### Notifications

- La police recoit une alerte automatique lors du declenchement du braquage
- Un timer de cooldown empeche de refaire le braquage immediatement

---

## Commandes

Aucune commande serveur n'est necessaire. Toute l'interaction se fait via le menu RageUI et les points d'interaction en jeu.
