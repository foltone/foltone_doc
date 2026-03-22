---
title: "Utilisation"
description: "Guide d'utilisation de Foltone CCTV"
script: "foltone-cctv"
section: "Foltone CCTV"
order: 3
version: "1.1.0"
---

# Utilisation — foltone_cctv

## Presentation

Foltone CCTV est un systeme de cameras de surveillance complet pour FiveM. Les joueurs peuvent acheter, placer et gerer des cameras de securite avec visualisation en temps reel, detection de mouvement, partage par job et capture d'ecran. Le script propose 4 types de cameras, chacun avec des props, optiques et prix uniques.

## Acheter des cameras

### Boutique

Interagissez avec le PNJ vendeur aux positions configurees pour ouvrir la boutique.

La boutique affiche tous les types de cameras disponibles en grille de cartes :
- **Image** et nom du modele
- **Description** et specs techniques (FOV, zoom, etc.)
- **Prix** et bouton d'achat

Chaque type de camera donne un item d'inventaire different.

### Methodes d'acces

| Mode | Comment interagir |
|------|------------------|
| `ox_target` | Visez le PNJ avec le curseur target |
| `drawtext` | Approchez le PNJ et appuyez sur **E** |
| `marker` | Entrez dans le marqueur et appuyez sur **E** |

## Placer des cameras

1. Utilisez l'item camera depuis votre inventaire
2. Le **HUD de placement** apparait (bas gauche) avec les instructions :
   - **Clic gauche** — Poser la camera
   - **Clic droit** — Annuler
   - **Scroll** — Tourner la camera
3. Visez un mur ou une surface — la camera fantome se plaque contre la surface
4. L'indicateur affiche **PRET** (vert) ou **TROP LOIN** (rouge)
5. Cliquez pour confirmer — un champ de nom apparait au centre de l'ecran
6. Entrez un nom et validez — la camera est installee

> Les cameras s'orientent automatiquement contre la surface du mur. La rotation au scroll permet d'ajuster l'angle de vue.

## Visualiser les cameras

### Tablette

Utilisez l'item `cctv_tablet` pour ouvrir le panneau de surveillance. Le joueur joue une animation avec une tablette en main.

### Terminaux informatiques

Interagissez avec les positions d'ordinateurs fixes pour ouvrir le panneau. Le joueur joue une animation de frappe.

### Postes de surveillance

Les postes de surveillance peuvent etre achetes en boutique et places dans le monde en utilisant l'item. Ils peuvent aussi etre configures a des positions fixes dans le config. Interagissez avec pour ouvrir le panneau de surveillance. Meme fonctionnalite que la tablette.

## Panneau de surveillance

Le panneau comporte **4 onglets** :

### Grille

Affiche toutes les cameras accessibles en grille avec :
- **Preview animee** avec bruit CCTV par camera
- **Nom de la camera** et badges de statut (ACTIVE, MOUVEMENT, JOB, SHARED)
- **Indicateur REC** et horodatage en temps reel
- **Bouton VOIR** pour entrer dans la camera

### Gestion

Liste toutes vos cameras avec les controles :
- **Detection de mouvement** activable/desactivable
- **Assigner au job** — partage la camera avec tous les joueurs de votre job actuel
- **Renommer** — changer le nom d'affichage
- **Supprimer** — supprime definitivement la camera

### Partage

Partagez vos cameras avec des joueurs specifiques :
- Entrez un **ID serveur de joueur** pour accorder l'acces
- **Revoquez** l'acces d'un joueur partage
- Les joueurs partages peuvent voir vos cameras mais pas les gerer

### Captures

Visualisez et gerez les captures d'ecran des cameras :
- Apercu miniature (si `screenshot-basic` est configure)
- Nom de la camera et horodatage
- Bouton **Supprimer** pour effacer les captures
- **Cliquez sur une capture** pour la voir en plein ecran dans un lightbox avec nom de camera et date

## Vue camera

Quand vous regardez une camera, l'ecran affiche un overlay CCTV avec des effets visuels :

### Controles

| Touche | Action |
|--------|--------|
| **Souris** | Rotation de la camera (pan/tilt) |
| **Scroll** | Zoom avant/arriere |
| **N** | Activer/desactiver la vision nocturne |
| **E** | Prendre une capture d'ecran |
| **Fleches gauche/droite** | Camera precedente/suivante |
| **Backspace** | Retour au panneau grille |
| **Escape** | Quitter la vue camera |

### Effets visuels

La vue camera inclut des effets configurables :
- **Filtre timecycle** — filtre camera de securite GTA (desaturation, contraste)
- **Vignette** — bords assombris
- **Grain** — bruit anime
- **Scanline** — ligne de balayage horizontale
- **Marqueurs d'angle** — coins de visee
- **Aberration chromatique** — leger decalage de couleur

> Tous les effets sont configurables dans `Config.CameraEffect`. Mettez une valeur a `0.0` pour le desactiver.

### Vision nocturne

Appuyez sur **N** pour activer la vision nocturne (vue amplifiee teintee verte). Appuyez a nouveau pour revenir a la vue CCTV normale.

### Effets sonores

Le systeme joue des sons natifs GTA pour :
- Ouverture/fermeture de la vue camera
- Zoom avant/arriere
- Rotation de la camera
- Changement de camera
- Prise de capture
- Activation de la vision nocturne

## Groupes de job

Les proprietaires de cameras peuvent assigner leurs cameras a un groupe de job :

1. Ouvrez l'onglet **Gestion**
2. Cliquez sur **ASSIGNER AU JOB** sur une camera
3. La camera est maintenant accessible a **tous les joueurs du meme job**
4. Un badge jaune **JOB** apparait sur les cameras partagees dans la grille
5. Cliquez a nouveau sur le badge pour rendre la camera **privee**

> Seul le proprietaire peut assigner/retirer le groupe de job. Les membres du job peuvent voir mais pas gerer.

## Destruction des cameras

Les cameras peuvent etre detruites en tirant dessus ou en les frappant avec les armes configurees.

| Parametre | Effet |
|-----------|-------|
| `Config.DestructionHits` | Nombre de coups necessaires (defaut : 3) |
| `Config.DestructionWeapons` | Liste des armes qui infligent des degats |

Quand une camera est detruite :
- Le prop est supprime pour tous les joueurs
- La camera est supprimee de la base de donnees
- Le proprietaire recoit une notification

## Detection de mouvement

Quand activee sur une camera :
- Detecte les joueurs dans le rayon configure
- Envoie une notification au proprietaire avec le nom de la camera et l'heure
- Notifie aussi les joueurs ayant un acces partage
- Respecte le cooldown entre les alertes

## Ajouter des types de cameras

Pour ajouter un nouveau type de camera :

1. Ajoutez une entree dans `Config.CameraTypes` dans `config.lua`
2. Creez l'item correspondant dans votre systeme d'inventaire
3. Optionnellement, ajoutez une image PNG dans `client/nui/img/<image>.png` (correspondant au champ `image` du config)
4. Utilisez `/cctv_debug` en jeu pour calibrer l'offset camera

La boutique et le systeme de placement prennent automatiquement en compte les nouveaux types depuis le config.
