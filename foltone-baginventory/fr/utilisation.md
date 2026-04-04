---
title: "Utilisation"
description: "Guide d'utilisation du script foltone_baginventory"
script: "foltone-baginventory"
section: "Bag Inventory"
order: 3
version: "1.0.0"
---

# Utilisation

## Fonctionnement general

Le systeme de sacs permet aux joueurs de transporter des objets supplementaires dans des sacs qu'ils peuvent poser au sol, remplir et ramasser.

## Utiliser un sac

### Deployer un sac

1. Ouvrez votre inventaire et utilisez un item de sac (ex: "Petit sac").
2. Le sac est deploye et apparait dans votre dos ou vos mains.
3. Vous pouvez maintenant y stocker des objets.

### Ouvrir le menu du sac

1. Appuyez sur la touche d'interaction lorsque le sac est equipe.
2. Le menu RageUI affiche le contenu du sac.
3. Vous pouvez ajouter ou retirer des objets et des armes.

### Poser un sac au sol

1. Ouvrez le menu du sac.
2. Selectionnez l'option "Poser au sol".
3. Le sac apparait au sol a votre position sous forme d'objet 3D.
4. D'autres joueurs peuvent interagir avec le sac pose.

### Ramasser un sac

1. Approchez-vous d'un sac pose au sol.
2. Appuyez sur la touche d'interaction.
3. Le sac et son contenu sont ajoutes a votre inventaire.

### Plier un sac

Si l'option est activee dans la configuration :

1. Ouvrez le menu du sac.
2. Selectionnez "Plier le sac".
3. Le sac est range dans votre inventaire comme un item classique.

## Comportement a la mort

Si `Config.DropOnDeath` est active :

- Tous vos sacs (ou seulement celui equipe) tombent au sol a votre mort.
- N'importe quel joueur peut ramasser ces sacs.
- Le contenu est conserve.

## Limites

- Chaque sac a un poids et un nombre d'emplacements maximum.
- Le nombre de sacs par joueur est limite (configurable).
- Un sac ne peut pas contenir un autre sac.
