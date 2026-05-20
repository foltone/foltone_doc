---
title: "Changelog"
description: "Historique des modifications du script foltone_blackmarket"
script: "foltone-blackmarket"
section: "Blackmarket"
order: 4
version: "1.1.0"
---

# Changelog

## v1.1.0 — Robustesse i18n + bugfixes

### Ajoute
- Locales **allemand** (`de.lua`) et **espagnol** (`es.lua`) complets
- Nouvelles cles de traduction : `rui_price_format`, `rui_price_stock_format`, `rui_component_suffix`, `rui_tint_suffix`, `rui_weapon_list_title`, `ui_html_title`, `ui_close_tooltip`, `ui_select_weapon` (remplacent les chaines hardcodees du RageUI et du NUI)
- Support de l'attribut HTML `data-i18n-title` dans le NUI (tooltips traduisibles)
- Documentation `configuration.md` reecrite avec **tous** les Config options : modes `MenuType` (nui/rageui), variantes `TargetSystem`, themes RageUI (`classic`/`modern`) avec descriptions visuelles, bannieres disponibles, options NUI Preview 3D, VanCustom, comportement des portes, animations du ped, parametres du phone (rayons / jitter), categories, etc.
- `version.json` consomme par le version check (`raw.githubusercontent.com/foltone/foltone_doc/main/foltone-blackmarket/version.json`)

### Corrige
- **NUI** : `RESOURCE_NAME` resolu via `GetParentResourceName()` → tous les callbacks JS↔Lua continuent de fonctionner si le serveur owner renomme le dossier de la ressource (sinon menu inerte, /restart obligatoire pour fermer le focus NUI)
- **NUI** : `state.customWeaponFilter` est reset a chaque ouverture (evite reference stale vers une arme vendue/disparue si `DefaultCategory = 'customs'`)
- **NUI** : guard `NUI.opening` contre les doubles ouvertures rapides (deux `getCatalog` en parallele)
- **Serveur** : `getCatalog` envoie maintenant un payload locale **mergé** (en de base + locale active en override), donc une cle manquante dans une locale partielle retombe sur l'anglais au lieu d'apparaitre comme cle brute dans l'UI
- **Serveur** : hot reload du resource (`ensure foltone_blackmarket` a chaud) re-broadcast l'etat aux joueurs deja co qui n'auraient pas le van
- **Serveur** : `BM_State.heat` est reset a chaque spawn (evitait le persist d'un cycle a l'autre)
- **Client** : timeout 30s + cleanup des callbacks serveur orphelins en cas de network drop, pcall autour de la callback pour ne pas crasher la queue
- **Client** : log console une fois quand `Config.Locale` pointe vers une locale qui n'existe pas, avec liste des locales disponibles
- **RageUI** : `fmtMoney` formate avec separateur de milliers (`$1,234,567`) comme le NUI
- **Bridge** : `Bridge.HasItem` (ESX/QB) plus robuste si le player object n'est pas trouve
- **Version check** : passe a un endpoint JSON (`json.decode` natif + fallback regex)

### Securite mineure
- `playerDropped` capture `source` dans une variable locale (bonne pratique)
- `applyCustomToOxInventory` : retire un retour multi-valeur inutilise

## v1.0.0 — Sortie initiale

### Ajoute
- Van mobile d'armes illegales avec cycle de spawn aleatoire
- Emplacements de spawn configurables (10 presets LS / campagne)
- Support multi-framework (ESX / QBCore / QBox / standalone)
- Support multi-inventaire (ox_inventory / qs-inventory / esx / qb)
- Support multi-target (ox_target / qb-target / qtarget) + fallback textUI
- Double menu : RageUI (in-game) et NUI (HTML/CSS) au choix via `Config.MenuType`
- Preview 3D des items avec zoom a la molette
- Onglet de customisation d'armes (composants + tints) pour les armes possedees
- Preview en temps reel au survol d'un custom
- Selecteur d'arme avec fleches dans l'onglet customs
- Persistance metadata ox_inventory (components + tint)
- Item telephone crypte avec systeme de blip a deux phases (recherche 161 puis van 110)
- Systeme police & heat (alertes, despawn automatique au seuil)
- Detection des flics a proximite : le marchand fuit si police proche (rayon 80m)
- Variance de stock et de prix par van (+/-30% / +/-10%)
- Gate de reputation (optionnel, hook `GetPlayerReputation`)
- Protections anti-cheat : check de distance, cooldown, validation source, transactions atomiques
- Verification de la possession de l'arme cote serveur pour les customs
- Logging webhook Discord a chaque achat
- Commande admin `bm_van spawn/despawn/status`
- Support multi-langue (fr / en / es)
- Verification de version automatique au demarrage
