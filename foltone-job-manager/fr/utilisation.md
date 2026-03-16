---
title: "Utilisation"
description: "Guide d'utilisation du script Job Manager"
script: "foltone-job-manager"
section: "Job Manager"
order: 3
version: "1.0.0"
---

# Utilisation — foltone_job_manager

## Fonctionnement général

Le script fournit une interface tablette NUI permettant aux boss de société de gérer leur entreprise : argent, employés, salaires et virements. Seuls les joueurs ayant le grade boss configuré peuvent accéder à l'interface.

## Accéder à l'interface

1. Avoir le **grade boss** (ou le grade configuré dans `bossGrade`) du job
2. Se rendre au **marqueur** de la société (position configurée dans `config.lua`)
3. Appuyer sur **E** pour ouvrir l'interface tablette

> Le marqueur n'apparaît que si le joueur a le grade boss du job correspondant.

## Onglet Argent

L'onglet de gestion de l'argent permet de :

- **Voir le solde** actuel de la société
- **Ajouter de l'argent** — Transférer de l'argent personnel vers la caisse de la société
- **Retirer de l'argent** — Transférer de l'argent de la société vers le joueur
- **Graphique des revenus** — Visualiser les revenus des 10 derniers jours via un graphique

> Les revenus sont enregistrés automatiquement toutes les heures dans le fichier `server/data.json`.

## Onglet Employés

L'onglet de gestion des employés affiche la liste de tous les employés de la société avec :

- **Nom** et **Prénom**
- **Grade** actuel

### Actions disponibles

| Action | Description |
|--------|-------------|
| **Promouvoir** | Augmente le grade de l'employé d'un niveau |
| **Rétrograder** | Diminue le grade de l'employé d'un niveau |
| **Virer** | Licencie l'employé (le met au job `unemployed`) |

> Les actions ne fonctionnent que si l'employé cible est **en ligne**.

## Onglet Salaires

Cet onglet affiche tous les grades du job avec leur salaire actuel. Le boss peut **modifier le salaire** de chaque grade directement dans le champ de saisie.

> Sur ESX, les salaires sont mis à jour dans la table `job_grades` de la base de données.

## Onglet Virements

Le boss peut effectuer des virements depuis la caisse de la société vers :

### Virement vers un joueur

1. Sélectionner le type **"Personne"**
2. Entrer l'**ID serveur** du joueur destinataire
3. Entrer le **montant**
4. Cliquer sur **"Envoyer le virement"**

### Virement vers une autre société

1. Sélectionner le type **"Société"**
2. Choisir la **société destinataire** dans la liste déroulante
3. Entrer le **montant**
4. Cliquer sur **"Envoyer le virement"**

> Seules les sociétés configurées dans `Config.SocietyList` apparaissent dans la liste.

## Mode clair / sombre

L'interface dispose d'un toggle jour/nuit en haut à droite. Le choix du thème est sauvegardé dans le `localStorage` du navigateur et persiste entre les sessions.

## Historique des revenus

Le script enregistre automatiquement le solde de chaque société **toutes les heures** dans le fichier `server/data.json`. Ces données alimentent le graphique des revenus affiché dans l'onglet Argent.

## Events disponibles

### Events serveur

```lua
-- Ajouter de l'argent à la société
TriggerServerEvent("foltone_job_manager:addSocietyMoney", companyName, amount)

-- Retirer de l'argent de la société
TriggerServerEvent("foltone_job_manager:removeSocietyMoney", companyName, amount)

-- Promouvoir un employé
TriggerServerEvent("foltone_job_manager:promoteEmployee", companyName, targetIdentifier)

-- Rétrograder un employé
TriggerServerEvent("foltone_job_manager:unpromoteEmployee", companyName, targetIdentifier)

-- Virer un employé
TriggerServerEvent("foltone_job_manager:fireEmployee", companyName, targetIdentifier)

-- Modifier le salaire d'un grade
TriggerServerEvent("foltone_job_manager:updateSalary", companyName, gradeId, salary)

-- Virement vers un joueur
TriggerServerEvent("foltone_job_manager:transferSocietyMoneyToPlayer", companyName, targetId, amount)

-- Virement vers une société
TriggerServerEvent("foltone_job_manager:transferSocietyMoneyToSociety", companyName, targetCompany, amount)

-- Définir le job d'un joueur
TriggerServerEvent("foltone_job_manager:setJob", targetId, companyName, grade)
```

### Callbacks serveur

```lua
-- Récupérer les données de la société (solde, employés, grades, revenus)
TriggerServerFoltoneJMCallback("foltone_job_manager:getData", function(data)
    -- data.money.balance : solde
    -- data.money.revenueLastDays : tableau des revenus des 10 derniers jours
    -- data.employees : liste des employés
    -- data.grades : liste des grades avec salaires
end, companyName)
```
