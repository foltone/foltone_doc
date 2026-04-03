---
title: "Changelog"
description: "Historique des modifications du script Vigneron"
script: "foltone-vigneron"
section: "Vigneron"
order: 4
version: "2.0.0"
---

# Changelog — foltone_vigneron

## v2.0.0

Refonte complète avec architecture modulaire.

### Nouveautés
- Architecture modulaire (bridge/, client/modules/, server/modules/)
- Bridge ox_target optionnel avec fallback markers + touche E
- Bridge ox_inventory optionnel avec fallback esx_addoninventory
- Multi-coffres avec permissions par grade
- Menus dual : RageUI ou ox_lib context
- Prise de service (duty) avec sync serveur
- Sécurité : rate limiting, validation serveur, anti-cheat
- Logs Discord optionnels
- Pipeline amélioré : progress bars ox_lib, annulable
- Escrow-friendly : cl_editable.lua et sv_editable.lua séparés
- Notifications `lib.notify()`, inputs `lib.inputDialog()`, confirmations `lib.alertDialog()`
- Traductions FR et EN

## v1.0.0

Version initiale.
