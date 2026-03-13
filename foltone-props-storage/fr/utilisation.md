---
title: "Utilisation"
description: "Guide d'utilisation du script Props Storage"
script: "foltone-props-storage"
section: "foltone_props_storage"
order: 3
version: "1.0.0"
---

# Utilisation — foltone_props_storage

## Fonctionnement général

Le script permet aux joueurs de placer des coffres-forts physiques dans le monde du jeu. Chaque coffre est protégé par un code PIN et seul le propriétaire peut le récupérer.

## Placer un coffre

1. **Obtenir l'item** — Un joueur doit posséder un item coffre (`big_safe` ou `safe`) dans son inventaire
2. **Utiliser l'item** — En utilisant l'item, l'interface de placement apparaît
3. **Positionner le coffre** :
   - **Flèches directionnelles** — Déplacer le coffre (avant/arrière/gauche/droite)
   - **Touches A / E** — Faire pivoter le coffre
   - **Entrée** — Confirmer le placement
4. **Définir le code PIN** — Un dialogue demande un code PIN (minimum 4 chiffres, codes simples interdits)

Le coffre est alors placé dans le monde et sauvegardé en base de données.

## Accéder au coffre

### Sans ox_inventory (RageUI)

1. Approchez-vous du coffre (distance configurable, par défaut 2.5m)
2. Appuyez sur **E** pour interagir
3. Entrez le **code PIN**
4. Le menu RageUI s'ouvre avec les options :
   - **Déposer/Retirer des items**
   - **Déposer/Retirer de l'argent** (cash + argent sale)
   - **Déposer/Retirer des armes** (avec munitions)
   - **Modifier le PIN** *(propriétaire uniquement)*
   - **Récupérer le coffre** *(propriétaire uniquement, coffre doit être vide)*

### Avec ox_inventory

1. Approchez-vous du coffre
2. Utilisez **ox_target** pour interagir
3. Entrez le **code PIN**
4. L'interface **ox_inventory** s'ouvre comme un stash classique
5. Glissez-déposez les items normalement

## Système de poids

Chaque coffre a une capacité maximale en poids :

| Type | Modèle | Capacité |
|------|--------|----------|
| Grand Coffre | `p_v_43_safe_s` | 50 000 |
| Coffre | `prop_ld_int_safe_01` | 30 000 |

Les items ont un poids défini dans ESX/ox_inventory. Les armes ont un poids configurable dans `config.lua`.

## Sécurité PIN

- Le code PIN doit faire **minimum 4 chiffres**
- Les codes simples sont **interdits** : `0000`, `1111`, `2222`, ..., `9999`, `1234`
- Seul le **propriétaire** peut modifier le PIN
- Seul le **propriétaire** peut récupérer le coffre

## Modifier le code PIN

1. Ouvrez le coffre avec votre PIN actuel
2. Sélectionnez **"Modifier le PIN"** dans le menu
3. Entrez votre nouveau code PIN

> **Note** : Cette option n'est visible que pour le propriétaire du coffre.

## Récupérer un coffre

1. Ouvrez le coffre avec votre PIN
2. **Videz entièrement** le coffre (items, argent, armes)
3. Sélectionnez **"Récupérer le coffre"**
4. L'item coffre retourne dans votre inventaire
5. Le coffre est supprimé du monde et de la base de données

## Instances / Buckets

Le script supporte les **routing buckets** de FiveM. Les coffres placés dans une instance spécifique ne sont visibles que dans cette instance.

Pour synchroniser l'instance d'un joueur depuis un autre script :

```lua
TriggerClientEvent("foltone_props_storage:updatePlayerInstance", playerId, instanceId)
```

## Logs Discord

Toutes les actions sont logguées via un webhook Discord :

- Placement d'un nouveau coffre
- Ouverture d'un coffre
- Dépôt / retrait d'items
- Dépôt / retrait d'argent
- Dépôt / retrait d'armes
- Modification du PIN
- Récupération d'un coffre

## Events disponibles

### Events serveur

```lua
-- Placer un coffre (déclenché automatiquement via l'item)
TriggerServerEvent("foltone_props_storage:addNewPropStorage", ...)

-- Dépôt/Retrait
TriggerServerEvent("foltone_props_storage:putPropMoney", id, type, amount)
TriggerServerEvent("foltone_props_storage:takePropMoney", id, type, amount)
TriggerServerEvent("foltone_props_storage:putPropItem", id, itemName, count)
TriggerServerEvent("foltone_props_storage:takePropItem", id, itemName, count)
TriggerServerEvent("foltone_props_storage:putPropWeapon", id, weaponName, ammo)
TriggerServerEvent("foltone_props_storage:takePropWeapon", id, weaponName)
```

### Callbacks serveur

```lua
-- Vérifier le PIN et ouvrir le coffre
ESX.TriggerServerCallback("foltone_props_storage:tryOpenProp", function(success)
    -- success: true/false
end, propId, pin)

-- Récupérer les données du coffre
ESX.TriggerServerCallback("foltone_props_storage:getPropData", function(data)
    -- data: inventory, weight, etc.
end, propId)

-- Vérifier si le joueur est propriétaire
ESX.TriggerServerCallback("foltone_props_storage:isOwner", function(isOwner)
    -- isOwner: true/false
end, propId)
```

### Events client

```lua
-- Synchroniser l'instance du joueur
TriggerClientEvent("foltone_props_storage:updatePlayerInstance", playerId, instanceId)
```
