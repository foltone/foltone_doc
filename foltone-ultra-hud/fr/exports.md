---
title: "Exports & Events"
description: "Reference API Ultra HUD pour developpeurs"
script: "foltone-ultra-hud"
section: "Ultra HUD"
order: 3
version: "1.0.0"
---

# Exports & Events — foltone_ultra_hud

## Exports Client

### Notify

Envoyer une notification simple (sans image).

```lua
exports.foltone_ultra_hud:Notify(message, type, duration)
```

| Parametre | Type | Requis | Description |
|---|---|---|---|
| `message` | string | oui | Texte de la notification |
| `type` | string | non | `"success"`, `"error"`, `"warning"`, `"info"` (defaut : neutre) |
| `duration` | number | non | Duree en ms (defaut : 5000) |

**Exemple :**

```lua
exports.foltone_ultra_hud:Notify("Vous avez recu 500$", "success")
exports.foltone_ultra_hud:Notify("Acces refuse", "error", 3000)
```

### AdvancedNotify

Envoyer une notification avec image (style GTA).

```lua
exports.foltone_ultra_hud:AdvancedNotify(image, title, message, subtitle, duration)
```

| Parametre | Type | Requis | Description |
|---|---|---|---|
| `image` | string | oui | URL ou chemin de l'image |
| `title` | string | oui | Titre en gras |
| `message` | string | oui | Corps du message |
| `subtitle` | string | non | Sous-titre sous le titre |
| `duration` | number | non | Duree en ms (defaut : 5000) |

**Exemple :**

```lua
exports.foltone_ultra_hud:AdvancedNotify(
    "https://i.imgur.com/example.png",
    "LESTER CREST",
    "J'ai un travail pour toi. Viens me voir.",
    "Nouvelle mission",
    7000
)
```

### ShowHud / HideHud

Afficher ou masquer le HUD entier.

```lua
exports.foltone_ultra_hud:ShowHud()
exports.foltone_ultra_hud:HideHud()
```

**Exemple :**

```lua
-- Masquer le HUD pendant une cinematique
exports.foltone_ultra_hud:HideHud()
Wait(5000)
exports.foltone_ultra_hud:ShowHud()
```

## Events Client

### foltone_ultra_hud:notify

Notification simple via event (utilisable cote client ou declenche depuis le serveur).

```lua
-- Cote client
TriggerEvent("foltone_ultra_hud:notify", message, type, duration)

-- Cote serveur (vers un joueur specifique)
TriggerClientEvent("foltone_ultra_hud:notify", source, message, type, duration)

-- Cote serveur (vers tous les joueurs)
TriggerClientEvent("foltone_ultra_hud:notify", -1, message, type, duration)
```

### foltone_ultra_hud:advancedNotify

Notification avancee via event.

```lua
-- Cote client
TriggerEvent("foltone_ultra_hud:advancedNotify", image, title, message, subtitle, duration)

-- Cote serveur
TriggerClientEvent("foltone_ultra_hud:advancedNotify", source, image, title, message, subtitle, duration)
```

### foltone_ultra_hud:enableHud / foltone_ultra_hud:disableHud

Afficher ou masquer le HUD via events (utile pour le controle cote serveur).

```lua
-- Cote serveur : masquer le HUD d'un joueur
TriggerClientEvent("foltone_ultra_hud:disableHud", source)

-- Cote serveur : afficher le HUD d'un joueur
TriggerClientEvent("foltone_ultra_hud:enableHud", source)
```

## Types de notification

| Type | Couleur | Icone | Utilisation |
|---|---|---|---|
| *(aucun)* | Blanc | Aucune | Messages generaux |
| `"success"` | Vert | Coche | Confirmations, actions completees |
| `"error"` | Rouge | Croix | Erreurs, actions refusees |
| `"warning"` | Jaune | Triangle | Avertissements, notices importantes |
| `"info"` | Bleu | Cercle info | Messages informatifs |

## Commande de test

Utilisez `/testnotif` pour tester les notifications en jeu :

```
/testnotif all       -- Envoyer tous les types
/testnotif simple    -- Notification neutre
/testnotif success   -- Notification succes
/testnotif error     -- Notification erreur
/testnotif warning   -- Notification avertissement
/testnotif info      -- Notification info
/testnotif advanced  -- Notification avancee avec image
```
