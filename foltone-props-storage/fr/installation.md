---
title: "Installation"
description: "Installation du script Props Storage"
script: "foltone-props-storage"
section: "foltone_props_storage"
order: 1
version: "1.0.0"
---

# Installation — foltone_props_storage

## Prérequis

- **ESX Legacy** (v1.12.3 ou supérieur)
- **oxmysql** — Librairie MySQL
- **ox_lib** *(optionnel)* — Pour les dialogues de saisie
- **ox_inventory** *(optionnel)* — Système d'inventaire alternatif
- **ox_target** *(optionnel)* — Nécessaire si vous utilisez ox_inventory

## Téléchargement

Téléchargez le script depuis votre espace Tebex et placez le dossier dans votre répertoire `resources/`.

## Base de données

Importez la table SQL dans votre base de données :

```sql
CREATE TABLE IF NOT EXISTS `props_inventory` (
  `id` INT PRIMARY KEY AUTO_INCREMENT,
  `owner` VARCHAR(255) NOT NULL,
  `inventory` JSON NOT NULL,
  `position` JSON NOT NULL,
  `prop` VARCHAR(100) NOT NULL,
  `pin` VARCHAR(10) NOT NULL,
  `bucket` INT DEFAULT NULL
);
```

## Configuration serveur

Ajoutez dans votre `server.cfg` :

```ini
ensure ox_lib
ensure oxmysql
ensure es_extended
ensure foltone_props_storage
```

> **Important** : `foltone_props_storage` doit être démarré **après** `es_extended` et `oxmysql`.

## Ajout des items

Ajoutez les items de coffre dans votre base de données ESX :

```sql
INSERT INTO `items` (`name`, `label`, `weight`, `rare`, `can_remove`) VALUES
  ('big_safe', 'Grand Coffre', 5, 0, 1),
  ('safe', 'Coffre', 3, 0, 1);
```

Si vous utilisez **ox_inventory**, ajoutez les items dans `ox_inventory/data/items.lua` :

```lua
['big_safe'] = {
    label = 'Grand Coffre',
    weight = 5000,
    stack = false,
},
['safe'] = {
    label = 'Coffre',
    weight = 3000,
    stack = false,
},
```

## ox_lib (optionnel)

Si vous souhaitez utiliser ox_lib pour les dialogues de saisie, décommentez la ligne dans `fxmanifest.lua` :

```lua
shared_scripts {
    '@ox_lib/init.lua', -- décommentez cette ligne
    "config.lua",
    "trad.lua",
    "locales/*.lua"
}
```

## Vérification

Après redémarrage du serveur :

1. Donnez-vous un item coffre : `/giveitem [id] big_safe 1`
2. Utilisez l'item — l'interface de placement doit apparaître
3. Placez le coffre et définissez un code PIN
4. Vérifiez les logs dans la console serveur

## Webhook Discord

Pour activer les logs Discord, éditez le fichier `server/sv_editable.lua` et remplacez l'URL du webhook :

```lua
PerformHttpRequest("https://discord.com/api/webhooks/VOTRE_WEBHOOK_ICI", ...)
```
