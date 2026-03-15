---
title: "Locales"
description: "Ultra HUD translation system"
script: "foltone-ultra-hud"
section: "foltone_ultra_hud"
order: 5
version: "1.0.0"
---

# Locales — foltone_ultra_hud

The script includes a full translation system for both Lua-side messages and the NUI admin panel.

## Setting the Language

In `config.lua`:

```lua
Config.locale = "en" -- "en", "fr", etc.
```

## Available Languages

| Code | Language | File |
|---|---|---|
| `en` | English | `locales/en.lua` |
| `fr` | French | `locales/fr.lua` |

## Adding a New Language

1. Copy `locales/en.lua` to `locales/xx.lua` (where `xx` is your language code)
2. Translate all values (keep the keys unchanged)
3. Change the first line from `Locales["en"]` to `Locales["xx"]`
4. Set `Config.locale = "xx"`

**Example — creating a German translation:**

```lua
-- locales/de.lua
Locales["de"] = {
    no_permission = "Du hast keine Berechtigung.",
    settings_saved = "Einstellungen gespeichert!",
    -- ... translate all keys
}
```

## Using Translations in Lua

The `L()` function is globally available (shared script):

```lua
L("key")              -- Simple translation
L("key", arg1, arg2)  -- Translation with string.format arguments
```

If a key is missing in the current locale, it falls back to English. If missing in English too, the key itself is returned.

## Translation Keys

The translation system covers:

- **Server messages**: permission errors, save confirmations
- **Admin panel**: all section titles, labels, options, buttons
- **Notifications settings**: position names
- **Test notifications**: all test messages

All NUI admin panel text uses `data-locale` HTML attributes that are automatically replaced when the locale is applied.
