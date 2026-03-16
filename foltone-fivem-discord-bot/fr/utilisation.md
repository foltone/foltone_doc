---
title: "Utilisation"
description: "Utilisation du script Foltone FiveM Discord Bot"
script: "foltone-fivem-discord-bot"
section: "Discord Bot"
order: 3
version: "1.0.0"
---

# Utilisation — foltone_fivem_discord_bot

## Commandes slash Discord

Toutes les commandes s'executent depuis Discord avec le prefixe `/`.

### Joueurs

| Commande | Description | Permission |
|----------|-------------|------------|
| `/playerlist` | Liste des joueurs connectes avec ID serveur et identifiants | moderator |
| `/playerinfo [id]` | Informations detaillees sur un joueur (identifiants, job, argent) | moderator |
| `/kick [id] [raison]` | Expulser un joueur du serveur | moderator |
| `/ban [id] [duree] [raison]` | Bannir un joueur (ex: duree `7d`, `permanent`) | admin |
| `/unban [identifier]` | Lever le bannissement d'un joueur | admin |
| `/spectate [id]` | Se mettre en mode spectateur sur un joueur | moderator |

### Moderation

| Commande | Description | Permission |
|----------|-------------|------------|
| `/warn [id] [raison]` | Avertir un joueur (loggue en base de donnees) | moderator |
| `/mute [id] [duree] [raison]` | Muter un joueur dans le chat in-game | moderator |
| `/unmute [id]` | Demuter un joueur | moderator |
| `/freeze [id]` | Immobiliser un joueur | moderator |
| `/unfreeze [id]` | Liberer un joueur immobilise | moderator |
| `/slap [id] [force]` | Projeter un joueur | moderator |
| `/heal [id]` | Soigner entierement un joueur | moderator |
| `/revive [id]` | Ramener un joueur a la vie | admin |
| `/sanctions [id]` | Consulter l'historique des sanctions d'un joueur | moderator |

### Economie

| Commande | Description | Permission |
|----------|-------------|------------|
| `/givemoney [id] [montant] [compte]` | Donner de l'argent a un joueur | admin |
| `/removemoney [id] [montant] [compte]` | Retirer de l'argent a un joueur | admin |
| `/setmoney [id] [montant] [compte]` | Definir l'argent d'un joueur | admin |
| `/giveitem [id] [item] [quantite]` | Donner un item a un joueur | admin |
| `/removeitem [id] [item] [quantite]` | Retirer un item d'un joueur | admin |

### Vehicules & Teleportation

| Commande | Description | Permission |
|----------|-------------|------------|
| `/tp [id] [cible_id]` | Teleporter un joueur vers un autre | admin |
| `/spawnvehicle [id] [modele]` | Faire apparaitre un vehicule pour un joueur | admin |
| `/deletevehicle [id]` | Supprimer le vehicule du joueur | admin |

### Emploi

| Commande | Description | Permission |
|----------|-------------|------------|
| `/setjob [id] [job] [grade]` | Changer le job d'un joueur | admin |

### Serveur

| Commande | Description | Permission |
|----------|-------------|------------|
| `/announce [message]` | Envoyer une annonce a tous les joueurs en jeu | admin |
| `/weather [type]` | Changer la meteo du serveur | admin |
| `/time [heure]` | Changer l'heure du serveur | admin |
| `/whitelist [add/remove] [identifier]` | Gerer la whitelist du serveur | admin |
| `/serverstatus` | Afficher les statistiques du serveur | all |

### Suivi & Planification

| Commande | Description | Permission |
|----------|-------------|------------|
| `/watchlist [add/remove/list] [identifier]` | Gerer la liste de surveillance | admin |
| `/schedule [add/remove/list]` | Gerer les taches programmees | founder |

---

## Dashboard Discord

Le dashboard est un embed Discord mis a jour automatiquement (toutes les X secondes selon `Config.Dashboard.refreshInterval`).

Il affiche :
- Nombre de joueurs connectes / maximum
- Uptime du serveur
- Dernieres connexions et deconnexions
- Dernieres actions administratives
- Boutons d'action rapide (kick rapide, voir liste joueurs)

Le dashboard se met a jour automatiquement et ne necessite aucune interaction.

---

## Systeme de Tickets

### Depuis Discord

Les joueurs peuvent ouvrir un ticket en utilisant les boutons disponibles dans votre salon d'accueil ou via une commande configuree.

A la creation :
1. Un canal prive est cree dans la categorie configuree
2. Le joueur et les admins y ont acces
3. Le canal est nomme `ticket-{nom}-{id}`

A la fermeture :
1. Un admin clique sur le bouton **Fermer le ticket**
2. Le transcript est sauvegarde (si `transcriptEnabled = true`)
3. Le canal est supprime et un log est envoye dans `logsChannelId`

### Depuis le jeu

Les joueurs peuvent ouvrir un ticket directement depuis FiveM :
- Commande : `/{Config.Tickets.command}` (defaut: `/ticket`)
- Touche raccourci : `Config.Tickets.keybind` (defaut: F6)

Les messages du ticket sont synchronises en temps reel entre Discord et le jeu.

---

## Chat synchronise

Le chat est bidirectionnel entre Discord et le jeu :
- Les messages envoyes dans le canal Discord configure apparaissent en jeu avec le prefixe `[DISCORD]`
- Les messages des joueurs en jeu apparaissent sur Discord avec leur nom

Les messages Discord affichent le nom et l'avatar de l'utilisateur.

---

## Alertes intelligentes

Le systeme d'alertes envoie automatiquement des notifications dans le canal configure selon les regles definies :

| Alerte | Declencheur |
|--------|-------------|
| Avertissements excessifs | Joueur avec X warns en Y minutes |
| Transaction suspecte | Transaction depassant le seuil |
| Serveur vide | Nombre de joueurs sous le seuil |
| Serveur plein | Nombre de joueurs au-dessus du seuil |
| Joueur surveille | Connexion d'un joueur dans la watchlist |
| Tueur en serie | Joueur avec X kills en Y minutes |
| Crash massif | X joueurs deconnectes en Y minutes |

Les alertes mentionnent le role configure dans `mentionRoleId` pour les alertes urgentes.

---

## Panel NUI Admin (in-game)

Le panel NUI est accessible uniquement aux admins en jeu.

### Acces

- Commande : `/adminpanel` (ou commande configuree dans `Config.Panel.command`)
- Touche raccourci : F7 (ou touche configuree dans `Config.Panel.keybind`)
- Fermeture : meme touche ou touche Echap

### Pages disponibles

| Page | Description |
|------|-------------|
| **Dashboard** | Vue d'ensemble : joueurs en ligne, stats serveur, uptime |
| **Joueurs** | Liste des joueurs, actions rapides (kick, ban, tp, heal, revive) |
| **Economie** | Gestion argent et inventaire des joueurs |
| **Logs** | Historique des logs serveur avec filtres par type |
| **Tickets** | Vue et gestion des tickets ouverts |
| **Planificateur** | Gestion des taches programmees (redemarrage, annonces) |

### Actions rapides (panel joueurs)

Dans l'onglet joueurs, selectionnez un joueur pour acceder a :
- Kick / Ban
- Teleporter vers / Teleporter a
- Donner argent / items
- Heal / Revive / Freeze
- Voir sanctions

---

## Planificateur de taches

Les taches programmees (restarts, annonces) sont gerees via le planificateur :

### Depuis Discord

```
/schedule add daily_restart restart "0 4 * * *" 30,15,5,1
/schedule list
/schedule remove daily_restart
```

### Depuis le panel NUI

L'onglet **Planificateur** du panel NUI permet de voir et gerer les taches sans quitter le jeu.

### Format Cron

| Expression | Description |
|------------|-------------|
| `0 4 * * *` | Tous les jours a 4h00 |
| `0 */6 * * *` | Toutes les 6 heures |
| `0 12 * * 1` | Tous les lundis a 12h00 |
