---
title: "Changelog"
description: "Historique des modifications du script foltone_blackmarket"
script: "foltone-blackmarket"
section: "Blackmarket"
order: 4
version: "1.0.0"
---

# Changelog

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
