---
title: "Utilisation"
description: "Guide d'utilisation du script foltone_blackmarket"
script: "foltone-blackmarket"
section: "Blackmarket"
order: 3
version: "1.1.0"
---

# Utilisation

## Trouver le van

Le van apparait automatiquement selon le cycle de spawn du serveur (`FirstSpawnDelaySeconds` puis `LifetimeSeconds` / `RespawnCooldownSeconds`). Il choisit un emplacement aleatoire dans `Config.SpawnLocations`.

Plusieurs facons de le trouver :

1. **Item telephone crypte** : le joueur utilise `bm_encrypted_phone` depuis son inventaire. Un blip 161 clignotant apparait pendant 20 secondes (zone approximative), puis la position precise du van pendant 60 secondes.
2. **Blip permanent** : si `Config.ShowBlip = true`. Optionnellement gate par `Config.RequireContactItem`.
3. **Roleplay** : le joueur apprend l'emplacement via d'autres joueurs, contacts, etc.

## Interagir avec le marchand

Approchez-vous du van. Selon `Config.TargetSystem` :

- **ox_target / qb-target / qtarget** : une option target apparait autour du marchand (zone 2m×2m autour du siege du vendeur).
- **none / fallback** : un textUI propose d'appuyer sur **E** a courte distance.

Le menu du shop s'ouvre (RageUI in-game ou NUI HTML, selon `Config.MenuType`).

## Deroule d'un achat

Le menu propose plusieurs categories :

1. **Armes** — pistolets, SMG, fusil a pompe, etc. Chacun a sa preview 3D, ses stats et un marqueur "serial scratched".
2. **Items** — munitions.
3. **Protection** — gilets pare-balles, gilet lourd, trousse de soin.
4. **Customs** — composants (silencieux, lunette, chargeur etendu...) et tints. Seules les armes que le joueur **possede deja** sont proposees ici.

Preview 3D : quand un item est survole, le modele est affiche devant le van. **La molette de la souris** permet de zoomer/dezoomer.

Pour les customs : un selecteur d'arme avec des fleches permet de switcher entre les armes customisables possedees.

## Risque et heat

- Chaque achat a une chance (`PoliceAlertChance`, 10% par defaut) de declencher une alerte police avec les coordonnees de l'acheteur.
- Chaque achat ajoute de la **chaleur** au van. Au-dela du seuil (8 par defaut), le van despawn automatiquement et les flics recoivent un blip temporaire.
- Un flic qui entre dans un rayon de 80m **fait fuir le marchand** (van + ped disparaissent).

## Commandes admin

La commande `bm_van` est disponible pour les admins (ACE ou groupe). Elle necessite que `Bridge.IsAdmin` retourne true.

| Commande | Description |
|---|---|
| `bm_van spawn [idx]` | Force le spawn du van (idx optionnel pour choisir l'emplacement) |
| `bm_van despawn` | Force le despawn immediat |
| `bm_van status` | Affiche l'etat du van (emplacement, heat) dans la console |

## Permissions

| Action | Requis |
|---|---|
| Trouver via blip permanent | `Config.ShowBlip = true` |
| Trouver via telephone | Item `bm_encrypted_phone` dans l'inventaire |
| Acheter une arme | Argent suffisant + reputation minimale si `minRep > 0` |
| Acheter un custom | Posseder deja l'arme + argent suffisant |
| Commandes `bm_van` | ACE `foltone_blackmarket.admin` ou groupe dans `Config.AdminGroups` |

## Reputation (optionnel)

Si vous definissez une fonction `GetPlayerReputation(src)` dans un fichier serveur, les items avec `minRep > 0` seront verrouilles pour les joueurs en dessous du seuil. Sans cette fonction definie, aucune gate de reputation n'est appliquee.

## Mise a jour

A chaque demarrage, le serveur verifie sa version contre la version distante. Si une nouvelle version est disponible, un message jaune apparait dans la console avec les instructions.
