---
title: "Utilisation"
description: "Guide d'utilisation du script Foltone Garage"
script: "foltone-garage"
section: "Foltone Garage"
order: 3
version: "2.0.0"
---

# Utilisation — foltone_garage

## Fonctionnement general

Foltone Garage est un systeme de garage complet pour FiveM. Il permet aux joueurs de stocker et recuperer leurs vehicules, de les ranger a la fourriere, et de leur attribuer des labels personnalises. Le script supporte les voitures, bateaux, avions et helicopteres, avec un systeme de fourriere a prix dynamique.

## Acces au garage

L'interface s'ouvre en interagissant avec le PED gestionnaire de garage place aux coordonnees configurees dans `config_garage.lua`.

Le mode d'interaction depend de `Config.InteractionType` :

| Mode | Comment interagir |
|------|--------------------|
| `ox_target` / `qb-target` / `interact` | Viser le PED avec le curseur cible |
| `drawtext` | S'approcher du PED et appuyer sur **E** |
| `marker` | Entrer dans le marqueur et appuyer sur **E** |

## Mode NUI (panel HTML)

Le panel NUI comporte **4 onglets** :

### Onglet Vehicules

Affiche tous les vehicules stockes dans le garage courant.

Pour chaque vehicule :
- **Modele** et **label** (si defini)
- **Plaque** d'immatriculation
- **Statut** (disponible, sorti, en fourriere)
- **Bouton Sortir** — fait apparaitre le vehicule a la position de spawn configuree

> Seuls les vehicules du type correspondant au garage sont affiches (voitures, bateaux, avions ou helicopteres).

### Onglet Ranger

Permet de ranger le vehicule actuellement conduit dans le garage.

1. Approchez le vehicule de la zone de rangement (`storeVeh`)
2. Ouvrez l'interface du garage
3. Cliquez sur **Ranger**
4. Le vehicule disparait et est marque comme stocke en DB

> La distance de rangement est configurable par garage (`distanceStore`).

#### Vehicules de service

Pour les garages de job avec `serviceVehicles` definis, l'onglet Ranger propose egalement une liste de vehicules de service a faire sortir directement.

### Onglet Fourriere

Affiche les vehicules du joueur actuellement en fourriere.

Pour chaque vehicule en fourriere :
- **Plaque** et **modele**
- **Prix de recuperation** calcule dynamiquement en fonction du temps ecoule
- **Bouton Recuperer** — debite le montant et fait sortir le vehicule

#### Calcul du prix

```
Prix = basePrice + (heures_ecoulees × pricePerHour)
Prix = max(minPrice, min(maxPrice, Prix))
```

Exemple avec la configuration par defaut (basePrice 500, pricePerHour 100) :
- Apres 2h : 500 + 200 = **700 $**
- Apres 10h : 500 + 1000 = **1500 $** (plafonné a maxPrice si depasse)

### Onglet Label

> Disponible uniquement en mode `Config.MenuType = "nui"`.

Permet d'attribuer un nom personnalise a un vehicule du joueur.

1. Selectionnez un vehicule dans la liste
2. Tapez le label souhaite (30 caracteres maximum)
3. Cliquez sur **Enregistrer**

Le label s'affiche a la place du modele dans l'onglet Vehicules.

---

## Mode RageUI (menu classique)

Le mode RageUI propose **3 sous-menus** accessibles via un menu principal :

| Sous-menu | Equivalent NUI |
|-----------|----------------|
| Vehicules | Onglet Vehicules |
| Ranger | Onglet Ranger |
| Fourriere | Onglet Fourriere |

> Le label personnalise n'est pas disponible en mode RageUI.

---

## Garages de job

Les garages avec `job`, `job2` ou `annyJob` definis sont restreints aux joueurs ayant le job correspondant.

| Parametre | Comportement |
|-----------|-------------|
| `job = "ambulance"` | Acces exclusif aux joueurs avec le job `ambulance` |
| `job2 = "famillies"` | Acces via le gang / job secondaire `famillies` |
| `annyJob = "police"` | Acces a n'importe quel grade du job `police` |

Les vehicules de service (si configures) sont accessibles uniquement par les membres du job.

---

## Fourriere

Les vehicules peuvent etre mis en fourriere manuellement (par un administrateur via les outils serveur) ou via d'autres scripts compatibles.

Un joueur peut recuperer son vehicule depuis n'importe quelle fourriere du bon type (voiture, bateau, avion ou helicoptere).

Le prix augmente automatiquement avec le temps. Une fois paye, le vehicule est rendu disponible et sort a la position de spawn de la fourriere.

---

## Types de vehicules

| Type | Description |
|------|-------------|
| `car` | Voitures, motos et vehicules terrestres |
| `boat` | Bateaux et vehicules nautiques |
| `plane` | Avions et jets |
| `heli` | Helicopteres |

Chaque type a sa propre liste de garages et de fourrieres configuree dans `config_garage.lua`.
