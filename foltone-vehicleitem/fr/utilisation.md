---
title: "Utilisation"
description: "Guide d'utilisation du script foltone_vehicleitem"
script: "foltone-vehicleitem"
section: "Vehicle Item"
order: 3
version: "1.0.0"
---

# Utilisation

## Presentation

Le script Vehicle Item permet d'acheter des vehicules sous forme d'items dans l'inventaire. Les joueurs peuvent ensuite spawner ces vehicules depuis leur inventaire et les ranger a tout moment.

## Achat d'un vehicule

1. Rendez-vous a la boutique de vehicules (marquee par un blip sur la carte si active).
2. Interagissez avec le PNJ vendeur pour ouvrir le menu d'achat (RageUI).
3. Parcourez la liste des vehicules disponibles avec leur prix.
4. Selectionnez le vehicule souhaite.
5. Si vous avez assez d'argent, le vehicule est ajoute a votre inventaire sous forme d'item.

## Utilisation d'un vehicule

### Sortir un vehicule (spawn)

1. Ouvrez votre inventaire.
2. Utilisez l'item du vehicule (ex: "BMX").
3. Le vehicule apparait a proximite de votre personnage.
4. L'item est retire de votre inventaire.

### Ranger un vehicule (store)

1. Approchez-vous de votre vehicule spawne.
2. Utilisez l'interaction pour ranger le vehicule.
3. Le vehicule disparait du monde et revient dans votre inventaire sous forme d'item.

## Cas d'utilisation typiques

### Velos et petits vehicules

Le systeme est ideal pour les velos (BMX, Cruiser, Scorcher) que les joueurs veulent transporter facilement.

### Vehicules temporaires

Permet de donner des vehicules en recompense sous forme d'items echangeables entre joueurs.

### Commerce entre joueurs

Les items vehicules peuvent etre echanges ou vendus entre joueurs comme n'importe quel autre item d'inventaire.

## Conseils

- Assurez-vous d'avoir suffisamment de place dans votre inventaire avant d'acheter.
- Un seul vehicule peut etre spawne a la fois par item.
- Si vous vous deconnectez avec un vehicule spawne, il sera supprime. Pensez a le ranger avant.
- Les items vehicules sont compatibles avec les systemes de drop et d'echange standard.
