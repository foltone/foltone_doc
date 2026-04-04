---
title: "Utilisation"
description: "Guide d'utilisation du script foltone_ammunation"
script: "foltone-ammunation"
section: "Ammunation"
order: 3
version: "1.0.0"
---

# Utilisation

## Achat d'armes

1. Rendez-vous dans un magasin Ammu-Nation (icone sur la carte).
2. Approchez-vous du PNJ vendeur.
3. Appuyez sur la touche d'interaction pour ouvrir le menu RageUI.
4. Naviguez dans les rayons (armes de poing, fusils, munitions, etc.).
5. Selectionnez un article et confirmez l'achat.

### Licence d'arme

Certaines armes necessitent une licence. Si vous n'en possedez pas :

- Le menu vous proposera d'acheter une licence au prix configure.
- Une fois la licence obtenue, les armes restreintes deviennent disponibles.
- La licence est permanente (sauf retrait par un administrateur).

## Braquage

### Conditions requises

- Un nombre minimum de policiers doit etre en service (configurable).
- Le cooldown entre deux braquages doit etre ecoule.
- Vous devez etre a proximite du PNJ.

### Deroulement

1. Approchez-vous du PNJ et selectionnez l'option de braquage.
2. Une barre de progression s'affiche pendant le braquage.
3. Restez a proximite du PNJ -- si vous vous eloignez, le braquage est annule.
4. Ne tuez pas le PNJ -- sa mort annule le braquage.
5. Une fois termine, vous recevez un montant aleatoire (dans la fourchette configuree).

### Alertes

Lors d'un braquage :
- Les policiers en service recoivent une alerte avec votre photo et la position du magasin.
- Un blip temporaire apparait sur la carte des policiers.

## Commandes

Aucune commande joueur n'est necessaire. Toute l'interaction se fait via le menu RageUI au contact du PNJ.

## Permissions

| Action | Condition |
|---|---|
| Acheter des armes libres | Aucune |
| Acheter des armes restreintes | Licence d'arme requise |
| Braquer le magasin | Nombre de policiers minimum atteint |
