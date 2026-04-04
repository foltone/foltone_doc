---
title: "Utilisation"
description: "Guide d'utilisation du script foltone_territories"
script: "foltone-territories"
section: "Territories"
order: 3
version: "1.0.0"
---

# Utilisation de foltone_territories

## Presentation

Ce script permet aux gangs de capturer des territoires en vendant de la drogue aux PNJ. Les territoires captures offrent de meilleurs prix de vente. Les PNJ peuvent accepter, refuser, ou appeler la police.

---

## Systeme de capture

### Comment capturer un territoire

1. Ayez un job de gang configure
2. Rendez-vous dans une zone de territoire (visible sur la carte)
3. Approchez un PNJ dans la zone
4. Ouvrez le menu RageUI pour lui vendre de la drogue
5. Chaque vente reussie rapporte des **points de capture**
6. Accumulez suffisamment de points pour capturer la zone

### Progression

- Chaque drogue rapporte un nombre de points different
- Les drogues plus risquees rapportent plus de points
- La progression est sauvegardee en base de donnees
- Quand le seuil est atteint, le territoire est capture par votre gang

---

## Reactions des PNJ

Quand vous approchez un PNJ pour vendre, trois reactions sont possibles :

### Accepter
Le PNJ achete la drogue. Vous recevez l'argent et les points de capture.

### Refuser
Le PNJ refuse la transaction. Rien ne se passe, vous gardez votre drogue.

### Appeler la police
Le PNJ refuse et **appelle la police**. Les forces de l'ordre recoivent une alerte avec votre position. Fuyez rapidement.

Les probabilites de chaque reaction sont configurables par type de drogue.

---

## Avantages des territoires captures

- **Meilleurs prix** : Les drogues se vendent plus cher dans un territoire controle par votre gang
- **Controle de zone** : Votre gang domine la zone visuellement sur la carte

---

## Vente de drogue

1. Assurez-vous d'avoir de la drogue dans votre inventaire
2. Approchez un PNJ (hors liste noire)
3. Interagissez via le menu RageUI
4. Selectionnez la drogue a vendre
5. Attendez la reaction du PNJ

### PNJ exclus

Certains PNJ (policiers, etc.) ne peuvent pas etre cibles. Ils sont definis dans la liste noire de la configuration.

---

## Commandes

Aucune commande necessaire. Toute l'interaction se fait via le menu RageUI et les zones definies sur la carte.
