---
title: "Traductions"
description: "Systeme de traduction Ultra HUD"
script: "foltone-ultra-hud"
section: "Ultra HUD"
order: 5
version: "1.0.0"
---

# Traductions — foltone_ultra_hud

Le script inclut un systeme de traduction complet pour les messages Lua et le panneau admin NUI.

## Definir la langue

Dans `config.lua` :

```lua
Config.locale = "en" -- "en", "fr", etc.
```

## Langues disponibles

| Code | Langue | Fichier |
|---|---|---|
| `en` | Anglais | `locales/en.lua` |
| `fr` | Francais | `locales/fr.lua` |

## Ajouter une nouvelle langue

1. Copiez `locales/en.lua` vers `locales/xx.lua` (ou `xx` est votre code langue)
2. Traduisez toutes les valeurs (gardez les cles inchangees)
3. Changez la premiere ligne de `Locales["en"]` a `Locales["xx"]`
4. Definissez `Config.locale = "xx"`

**Exemple — creer une traduction allemande :**

```lua
-- locales/de.lua
Locales["de"] = {
    no_permission = "Du hast keine Berechtigung.",
    settings_saved = "Einstellungen gespeichert!",
    -- ... traduire toutes les cles
}
```

## Utiliser les traductions en Lua

La fonction `L()` est disponible globalement (shared script) :

```lua
L("key")              -- Traduction simple
L("key", arg1, arg2)  -- Traduction avec arguments string.format
```

Si une cle est absente dans la locale courante, le systeme retombe sur l'anglais. Si absente en anglais aussi, la cle elle-meme est retournee.

## Cles de traduction

Le systeme de traduction couvre :

- **Messages serveur** : erreurs de permission, confirmations de sauvegarde
- **Panneau admin** : tous les titres de sections, labels, options, boutons
- **Parametres de notifications** : noms des positions
- **Notifications de test** : tous les messages de test

Tous les textes du panneau admin NUI utilisent des attributs HTML `data-locale` qui sont automatiquement remplaces quand la locale est appliquee.
