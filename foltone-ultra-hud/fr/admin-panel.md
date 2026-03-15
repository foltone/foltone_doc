---
title: "Panneau Admin"
description: "Guide d'utilisation du panneau admin Ultra HUD"
script: "foltone-ultra-hud"
section: "foltone_ultra_hud"
order: 4
version: "1.0.0"
---

# Panneau Admin — foltone_ultra_hud

Le panneau admin fournit une interface de configuration complete en jeu. Les changements s'appliquent a **tous les joueurs** du serveur et persistent apres redemarrage.

## Ouvrir le panneau

Tapez la commande admin dans le chat (par defaut : `/hudadmin`). Les permissions admin sont requises.

### Ordre de verification des permissions

1. **Groupe framework** — ESX : `admin`, `superadmin`, `god` / QBCore : permission `admin`, `god`
2. **Groupes personnalises** — Tout groupe liste dans `Config.adminGroups`
3. **Fallback ACE** — Permission `command.hudadmin`

## Sections du panneau

### Couleurs

Changez la couleur de chaque element du HUD avec les selecteurs de couleur :

- Texte, Vie, Armure, Faim, Soif, Stamina, Apnee, Carburant

Les couleurs s'appliquent aux barres, cercles, carres, hexagones et leurs effets lumineux.

### Visibilite

Activez/desactivez individuellement les elements du HUD :

- ID, Metier, Metier 2/Gang, Argent, Banque, Argent sale, Position, Vie, Armure, Faim, Soif, Stamina, Apnee, Compteur

### Affichage

| Parametre | Options | Description |
|---|---|---|
| Affichage statuts | Barre, Cercle, Carre, Hexagone, Texte | Forme des indicateurs de statut |
| Remplissage | Stroke, Fill | Stroke = contour progressif, Fill = remplissage solide bas vers haut |
| Unite de vitesse | KM/H, MPH | Unite du compteur |

### Taille

Curseurs de mise a l'echelle pour chaque groupe (0.5x a 1.5x) :

- Portefeuille, Position, Statut, Compteur

### Notifications

| Parametre | Plage | Description |
|---|---|---|
| Position | 6 positions | Ou les notifications apparaissent a l'ecran |
| Largeur | 15-40 vw | Largeur du conteneur de notifications |
| Taille | 0.5-2.0 | Multiplicateur d'echelle des notifications |

## Mode Apercu

Cliquez sur **APERCU** pour voir tous les elements du HUD avec des donnees de demo. Cliquez sur **QUITTER APERCU** pour revenir.

## Mode Arrangement

Cliquez sur **ARRANGER** pour entrer en mode glisser-deposer :

1. Le panneau admin se ferme et tous les elements deviennent deplacables
2. Glissez les elements pour les repositionner ou vous voulez
3. Cliquez sur **SAUVEGARDER POSITIONS** pour enregistrer la disposition pour tous les joueurs
4. Cliquez sur **ANNULER** pour annuler les changements
5. Cliquez sur **REINITIALISER** pour restaurer les positions par defaut

## Sauvegarde

Cliquez sur **SAUVEGARDER** pour enregistrer tous les parametres (couleurs, visibilite, affichage, taille, notifications) dans `settings.json`. Les changements sont immediatement appliques a tous les joueurs connectes.

> Les parametres sont stockes cote serveur dans `settings.json` dans le dossier de la ressource. Ils persistent apres redemarrage du serveur et s'appliquent a tous les joueurs.
