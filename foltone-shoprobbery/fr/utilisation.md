---
title: "Utilisation"
description: "Guide d'utilisation du script foltone_shoprobbery"
script: "foltone-shoprobbery"
section: "Shop Robbery"
order: 3
version: "1.0.0"
---

# Utilisation de foltone_shoprobbery

## Presentation

Ce script combine un systeme de boutique et un systeme de braquage. Les joueurs peuvent acheter des articles dans les superettes ou les braquer pour de l'argent. Meme systeme que l'armurerie mais adapte aux superettes.

---

## Boutique (Achat d'articles)

### Acheter des articles

1. Rendez-vous dans une superette
2. Approchez le PNJ vendeur
3. Ouvrez le menu RageUI
4. Parcourez les articles disponibles
5. Selectionnez et confirmez votre achat

Les articles et leurs prix sont configurables dans le fichier de configuration.

---

## Braquage

### Conditions prealables

- Un nombre minimum de policiers doit etre en service
- Le cooldown de la boutique doit etre ecoule
- Le PNJ vendeur doit etre en vie

### Deroulement du braquage

1. Approchez le PNJ vendeur dans une superette
2. Selectionnez l'option de braquage dans le menu
3. Une barre de progression apparait - **ne bougez pas**
4. Attendez la fin de la progression pour recuperer l'argent

### Annulation automatique

Le braquage est **immediatement annule** si :
- Vous vous deplacez pendant la progression
- Le PNJ vendeur meurt (ne le tuez pas)

### Alertes police

Lorsqu'un braquage est declenche :
- Tous les policiers en service recoivent une alerte
- L'alerte inclut une **photo du suspect**
- L'alerte inclut la **geolocalisation** de la boutique
- La position exacte est indiquee sur la carte des policiers

### Cooldown

Apres un braquage reussi, la boutique entre en cooldown. Aucun autre braquage ne peut avoir lieu dans cette boutique jusqu'a expiration du delai.

---

## Commandes

Aucune commande necessaire. Toute l'interaction se fait via le menu RageUI et les points d'interaction.
