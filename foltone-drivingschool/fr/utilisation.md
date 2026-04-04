---
title: "Utilisation"
description: "Guide d'utilisation du script foltone_drivingschool"
script: "foltone-drivingschool"
section: "Driving School"
order: 3
version: "1.0.0"
---

# Utilisation

## Acceder a l'auto-ecole

1. Rendez-vous au point d'auto-ecole indique sur la carte.
2. Approchez-vous du PNJ moniteur.
3. Appuyez sur la touche d'interaction pour ouvrir le menu.

## Examen du code de la route

### Deroulement

1. Selectionnez "Examen du code" dans le menu.
2. Payez les frais d'inscription.
3. Une interface NUI s'affiche avec les questions.
4. Pour chaque question :
   - Lisez la question et les reponses proposees.
   - Cliquez sur la reponse de votre choix.
   - Un timer est affiche (temps limite par question).
5. A la fin de l'examen, votre score est affiche.

### Resultat

- **Reussite** (score >= seuil configure) : Vous pouvez passer aux examens pratiques.
- **Echec** : Vous devez repayer et repasser l'examen.

## Examens pratiques

Trois types d'examens pratiques sont disponibles :

### Examen voiture

1. Selectionnez "Examen voiture" dans le menu.
2. Payez les frais.
3. Un vehicule d'examen apparait.
4. Montez dans le vehicule et suivez le parcours (checkpoints).
5. Respectez les regles :
   - Ne depassez pas la limite de vitesse.
   - Evitez les collisions.
   - Passez par tous les checkpoints dans l'ordre.
6. A la fin du parcours, le resultat est annonce.

### Examen moto

Meme principe que l'examen voiture, avec un vehicule deux-roues et un parcours dedie.

### Examen poids lourd

Meme principe, avec un camion et une tolerance d'erreurs reduite.

## Attribution des licences

En cas de reussite :

| Examen | Licence attribuee |
|---|---|
| Voiture | `drive` |
| Moto | `drive_bike` |
| Poids lourd | `drive_truck` |

La licence est ajoutee automatiquement via esx_license et est permanente.

## Echec

En cas d'echec a un examen pratique :

- Le vehicule d'examen est supprime.
- Vous devez repayer les frais pour retenter.
- Aucun cooldown n'est impose (sauf si configure).

## Conseils

- Revisez les questions avant de passer l'examen du code.
- Conduisez prudemment pendant les examens pratiques.
- Attention aux pietons : une collision avec un pieton entraine un echec immediat.
