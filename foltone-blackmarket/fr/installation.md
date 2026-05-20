---
title: "Installation"
description: "Guide d'installation du script foltone_blackmarket"
script: "foltone-blackmarket"
section: "Blackmarket"
order: 1
version: "1.1.1"
---

# Installation

## Prerequis

- **ox_lib** (obligatoire)
- **Un framework** : ESX, QBCore, QBox ou standalone
- **Un inventaire** : ox_inventory (recommande), qs-inventory, esx ou qb-inventory
- **Un systeme de target** (optionnel mais recommande) : ox_target, qb-target ou qtarget

## Etapes d'installation

### 1. Telecharger le script

Placez le dossier `foltone_blackmarket` dans votre repertoire `resources/[foltone]/`.

### 2. Ajouter au server.cfg

```cfg
ensure foltone_blackmarket
```

Assurez-vous que les dependances sont demarrees **avant** ce script :

```cfg
ensure ox_lib
ensure ox_inventory
ensure ox_target
ensure es_extended    # ou qb-core / qbx_core
ensure foltone_blackmarket
```

### 3. Declarer les items d'inventaire

Si vous utilisez **ox_inventory**, les items ont deja ete ajoutes dans `[OX]/ox_inventory/data/items.lua` :

- `bm_encrypted_phone` — telephone jetable revelant la position du van
- `bm_contact` — contact underground (optionnel, utilise avec `Config.RequireContactItem`)

Si vous utilisez un autre inventaire, ajoutez ces deux items manuellement (voir Configuration).

### 4. Configurer le script

Editez `config.lua` selon votre serveur (locale, framework, money, emplacements, items...). Voir la section Configuration.

### 5. Redemarrer le serveur

Redemarrez votre serveur, ou executez dans la console :

```
refresh
ensure foltone_blackmarket
```

Au demarrage, le script affiche sa version. Si une nouvelle version est disponible, un avertissement jaune s'affiche dans la console.

## Structure des fichiers

```
foltone_blackmarket/
├── bridge/           # Abstraction multi-framework (ESX/QB/QBox/standalone)
├── client/           # Logique client (van, ped, menu, phone, preview)
├── server/           # Logique serveur (spawn, transactions, version check)
├── src/              # Librairie RageUI (menu in-game)
├── html/             # Menu NUI (alternative HTML/CSS)
├── locales/          # Traductions (fr / en / es)
├── config.lua        # Configuration principale
├── trad.lua          # Systeme de traduction
└── fxmanifest.lua
```

## Problemes courants

| Probleme | Solution |
|---|---|
| Interaction ne fonctionne pas | Verifiez qu'ox_target / qb-target est demarre, ou mettez `Config.TargetSystem = 'none'` |
| Les armes 3D ne s'affichent pas | Build GTA V recent : verifiez que `RequestWeaponAsset` fonctionne dans la console |
| Le menu ne s'ouvre pas | Verifiez `Config.MenuType` (`'rageui'` ou `'nui'`) |
| Le van ne spawn jamais | Verifiez que `Config.SpawnLocations` n'est pas vide |
| Telephone crypte sans effet | Verifiez que l'item est bien declare dans l'items.lua de votre inventaire avec `server.export` vers `foltone_blackmarket.useEncryptedPhone` |
