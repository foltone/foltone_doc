---
title: "Configuration"
description: "Configuration du script Foltone Banking"
script: "foltone-banking"
section: "foltone_banking"
order: 2
version: "1.0.0"
---

# Configuration — foltone_banking

Toute la configuration se fait dans le fichier `config.lua` a la racine du script.

## Langue

```lua
Config.Locale = "fr" -- "fr" ou "en"
```

Les traductions sont dans le dossier `locales/`. Vous pouvez ajouter vos propres langues en creant un nouveau fichier (ex: `locales/de.lua`).

## Framework

```lua
Config.Framework = "esx" -- "esx", "qbcore" ou "qbx"
```

| Valeur | Framework | Dependances requises |
|--------|-----------|---------------------|
| `"esx"` | ESX Legacy | `es_extended`, `oxmysql`, `esx_addonaccount` |
| `"qbcore"` | QBCore | `qb-core`, `oxmysql`, `qb-banking` |
| `"qbx"` | QBX | `qbx_core`, `oxmysql`, `qb-banking` |

## Mode d'interaction

```lua
Config.InteractionType = "drawtext" -- "marker", "ox_target", "qb-target", "qtarget", "drawtext"
```

| Mode | Description | Dependance |
|------|-------------|------------|
| `"marker"` | Marqueur au sol avec touche E | Aucune |
| `"ox_target"` | Cible 3D eye via ox_target | `ox_target` |
| `"qb-target"` | Cible 3D eye via qb-target | `qb-target` |
| `"qtarget"` | Cible 3D eye via qtarget | `qtarget` |
| `"drawtext"` | Texte d'aide a l'ecran avec touche E | Aucune |

## IBAN et Compte

```lua
Config.IBANPrefix = "FB"          -- prefixe pour les IBAN generes
Config.DefaultPIN = "0000"        -- PIN par defaut des nouveaux comptes
Config.StartingBalance = 0        -- solde initial des nouveaux comptes
```

| Parametre | Description |
|-----------|-------------|
| `IBANPrefix` | Prefixe ajoute devant chaque IBAN genere (ex: `FB-123456`) |
| `DefaultPIN` | Code PIN attribue par defaut a la creation du compte |
| `StartingBalance` | Montant credite automatiquement a l'ouverture du compte |

## ATM

```lua
Config.ATMs = {
    models = {"prop_atm_01", "prop_atm_02", "prop_atm_03", "prop_fleeca_atm"},
    features = {"deposit", "withdraw", "balance", "transfer", "history"},
    distance = 1.5,
    blip = false,
}
```

| Parametre | Description |
|-----------|-------------|
| `models` | Liste des modeles de props ATM detectes automatiquement sur la map |
| `features` | Fonctionnalites accessibles depuis un ATM |
| `distance` | Distance d'interaction en metres |
| `blip` | `false` pour desactiver, ou table `{ sprite, color, scale, label }` pour afficher un blip |

> Les comptes joints, l'epargne et la crypto ne sont **pas accessibles** depuis les ATM, uniquement depuis les banques.

## Banques

```lua
Config.Banks = {
    ped = { model = "s_m_m_bankman_01", scenario = "WORLD_HUMAN_CLIPBOARD" },
    features = {"deposit", "withdraw", "balance", "transfer", "history", "card", "pin"},
    distance = 2.0,
    blip = { sprite = 108, color = 2, scale = 0.8, label = "Banque" },
    positions = {
        { pos = vector3(149.0, -1040.0, 29.4), heading = 336.0 },
        { pos = vector3(314.2, -278.7, 54.2), heading = 336.0 },
        { pos = vector3(-351.5, -49.5, 49.0), heading = 336.0 },
        { pos = vector3(-1212.9, -330.1, 37.8), heading = 336.0 },
        { pos = vector3(-2962.5, 482.6, 15.7), heading = 336.0 },
        { pos = vector3(1175.0, 2706.8, 38.1), heading = 336.0 },
    },
}
```

| Parametre | Description |
|-----------|-------------|
| `ped.model` | Modele du PED banquier |
| `ped.scenario` | Animation du PED (scenario GTA) |
| `features` | Fonctionnalites accessibles en banque (plus complet qu'un ATM) |
| `distance` | Distance d'interaction en metres |
| `blip` | Configuration du blip sur la carte (`false` pour desactiver) |
| `positions` | Liste des positions de banque avec coordonnees et heading |

### Ajouter une nouvelle banque

Ajoutez une entree dans le tableau `positions` :

```lua
{ pos = vector3(x, y, z), heading = 0.0 },
```

> Le PED banquier sera automatiquement cree a chaque position configuree.

## Cartes bancaires

```lua
Config.CardSystem = {
    useItem = false,          -- true = carte comme item ox_inventory
    cardItem = "bank_card",   -- nom de l'item dans ox_inventory
    reissuePrice = 500,       -- prix de reedition de carte
    pinChangePrice = 100,     -- prix de changement de PIN
}
```

| Parametre | Description |
|-----------|-------------|
| `useItem` | `true` pour utiliser la carte comme item physique (necessite `ox_inventory`), `false` pour une carte virtuelle |
| `cardItem` | Nom de l'item dans ox_inventory (uniquement si `useItem = true`) |
| `reissuePrice` | Cout en $ pour reediter une carte (perdue ou volee) |
| `pinChangePrice` | Cout en $ pour changer le code PIN |

## Virements

```lua
Config.Transfer = {
    allowByServerId = true,
    allowByIBAN = true,
    offlineTransfer = true,
}
```

| Parametre | Description |
|-----------|-------------|
| `allowByServerId` | Autoriser les virements par ID serveur du joueur |
| `allowByIBAN` | Autoriser les virements par numero IBAN |
| `offlineTransfer` | Autoriser les virements vers des joueurs hors ligne (via IBAN) |

## Historique

```lua
Config.History = {
    perPage = 50,
}
```

| Parametre | Description |
|-----------|-------------|
| `perPage` | Nombre de transactions affichees par page dans l'historique |

## Theme

```lua
Config.theme = {}
```

Le theme par defaut est le **Blue Edition** (bleu electrique sur fond sombre). La table `theme` permet de surcharger les variables CSS si necessaire. En laissant la table vide `{}`, le theme par defaut est applique.

> **Attention** : Le design system impose des regles strictes. N'utilisez jamais de noir pur, de blanc, de dore/orange ou de violet/cyan.

## Notifications

```lua
Config.Notification = function(message)
    SetNotificationTextEntry("STRING")
    AddTextComponentString(message)
    DrawNotification(false, false)
end
```

Remplacez cette fonction par votre systeme de notification prefere (ex: okokNotify, ox_lib notify, etc.).

## Texte d'aide

```lua
Config.DisplayText = function(text)
    SetTextComponentFormat("STRING")
    AddTextComponentString(text)
    DisplayHelpTextFromStringLabel(0, 0, 1, -1)
end
```

Personnalisez l'affichage du texte d'aide (affiche quand un joueur est pres d'un PED ou d'un ATM).

## Societes

```lua
Config.Society = {
    defaultGrades = {"boss", "manager"},
    jobs = {
        -- Override par job : ["police"] = { grades = {"boss", "lieutenant"} },
    },
    features = {"balance", "deposit", "withdraw", "transfer", "payroll", "history"},
    positions = {
        -- { job = "police", pos = vector3(440.0, -981.0, 30.7), heading = 0.0 },
        -- { job = "ambulance", pos = vector3(311.0, -592.0, 43.3), heading = 0.0 },
    },
    distance = 2.0,
    ped = { model = "s_m_m_accountant_01", scenario = "WORLD_HUMAN_CLIPBOARD" },
    blip = false,
}
```

| Parametre | Description |
|-----------|-------------|
| `defaultGrades` | Grades ayant acces aux comptes societe par defaut |
| `jobs` | Overrides par job pour specifier des grades differents |
| `features` | Fonctionnalites societe activees |
| `positions` | Positions des PED societe sur le lieu de travail |
| `distance` | Distance d'interaction avec le PED societe |
| `ped.model` | Modele du PED comptable |
| `ped.scenario` | Animation du PED |
| `blip` | Configuration du blip (`false` pour desactiver) |

### Ajouter un PED societe

Ajoutez une entree dans le tableau `positions` :

```lua
{ job = "police", pos = vector3(440.0, -981.0, 30.7), heading = 0.0 },
```

> Le PED n'est visible que par les joueurs ayant le grade requis pour le job correspondant. L'acces aux comptes societe est egalement disponible depuis les banques et ATM (onglet societe).

### Override de grades par job

```lua
jobs = {
    ["police"] = { grades = {"boss", "lieutenant"} },
    ["ambulance"] = { grades = {"boss"} },
},
```

> Si un job n'a pas d'override, les `defaultGrades` sont utilises.

## Score de credit

```lua
Config.CreditScore = {
    default = 500,
    min = 0,
    max = 1000,
    rewards = {
        deposit = 2,
        withdraw = -1,
        transfer_out = 1,
        transfer_in = 1,
        upgrade = 5,
    },
}
```

| Parametre | Description |
|-----------|-------------|
| `default` | Score de credit initial pour les nouveaux comptes |
| `min` | Score minimum possible |
| `max` | Score maximum possible |
| `rewards` | Points ajoutes (+) ou retires (-) par type d'operation |

### Table des rewards

| Action | Points | Description |
|--------|--------|-------------|
| `deposit` | +2 | Chaque depot effectue |
| `withdraw` | -1 | Chaque retrait effectue |
| `transfer_out` | +1 | Chaque virement envoye |
| `transfer_in` | +1 | Chaque virement recu |
| `upgrade` | +5 | Passage au niveau superieur |

## Niveaux de compte

```lua
Config.AccountLevels = {
    standard = {
        label = "Standard",
        interestRate = 0.5,
        interestCap = 5000,
        transferMax = 50000,
        taxReduction = 0,
    },
    premium = {
        label = "Premium",
        interestRate = 1.5,
        interestCap = 20000,
        transferMax = 200000,
        taxReduction = 25,
        upgradePrice = 50000,
        minCreditScore = 700,
    },
}
```

### Comparaison Standard vs Premium

| Parametre | Standard | Premium | Description |
|-----------|----------|---------|-------------|
| `interestRate` | 0.5% | 1.5% | Taux d'interet par cycle |
| `interestCap` | $5 000 | $20 000 | Plafond d'interets par periode |
| `transferMax` | $50 000 | $200 000 | Montant maximum par virement |
| `taxReduction` | 0% | 25% | Reduction sur les taxes |
| `upgradePrice` | — | $50 000 | Cout de l'upgrade |
| `minCreditScore` | — | 700 | Score minimum requis pour upgrade |

## Interets

```lua
Config.Interest = {
    interval = 60,       -- minutes entre chaque cycle de cron
    resetPeriod = 1440,  -- minutes avant reinitialisation du cap d'interets (24h)
}
```

| Parametre | Description |
|-----------|-------------|
| `interval` | Intervalle en minutes entre chaque calcul d'interets |
| `resetPeriod` | Duree en minutes avant que le plafond d'interets ne se reinitialise (1440 = 24 heures) |

> Les interets ne sont credites qu'aux joueurs **connectes** (online-only by design).

## Taxation progressive

```lua
Config.Tax = {
    deposit = {
        { from = 0, to = 10000, rate = 0 },
        { from = 10000, to = 50000, rate = 2 },
        { from = 50000, to = 0, rate = 5 },
    },
    withdraw = {
        { from = 0, to = 10000, rate = 0 },
        { from = 10000, to = 50000, rate = 1 },
        { from = 50000, to = 0, rate = 3 },
    },
    transfer = {
        { from = 0, to = 10000, rate = 0 },
        { from = 10000, to = 50000, rate = 1.5 },
        { from = 50000, to = 0, rate = 4 },
    },
}
```

| Parametre | Description |
|-----------|-------------|
| `from` | Debut de la tranche (inclus) |
| `to` | Fin de la tranche (exclus). `0` signifie **illimite** (derniere tranche) |
| `rate` | Taux de taxation en pourcentage pour cette tranche |

### Fonctionnement par tranches

La taxation est **progressive** : chaque portion du montant est taxee au taux de sa tranche.

**Exemple** : Un depot de $60 000 avec la configuration par defaut :

| Tranche | Montant taxe | Taux | Taxe |
|---------|-------------|------|------|
| $0 - $10 000 | $10 000 | 0% | $0 |
| $10 000 - $50 000 | $40 000 | 2% | $800 |
| $50 000+ | $10 000 | 5% | $500 |
| **Total** | **$60 000** | — | **$1 300** |

> **Important** : Les tranches doivent etre contigues et ordonnees. Les operations de societe, les comptes joints, l'epargne et la crypto sont **exempts de taxation**.

> Les comptes Premium beneficient d'une reduction de 25% sur les taxes (configurable via `taxReduction`).

## Comptes joints

```lua
Config.JointAccount = {
    enabled = true,
    maxMembers = 4,
    maxAccountsPerPlayer = 2,
    transferMax = 50000,
    features = {"deposit", "withdraw", "transfer", "history"},
}
```

| Parametre | Description |
|-----------|-------------|
| `enabled` | Activer/desactiver les comptes joints |
| `maxMembers` | Nombre maximum de membres par compte joint |
| `maxAccountsPerPlayer` | Nombre maximum de comptes joints auxquels un joueur peut appartenir |
| `transferMax` | Montant maximum par virement depuis un compte joint |
| `features` | Fonctionnalites disponibles sur les comptes joints |

> Les comptes joints sont accessibles **uniquement en banque** (pas depuis les ATM). Ils ne sont pas soumis a la taxation, aux interets ni au score de credit.

## Notifications telephone

```lua
Config.PhoneNotifications = {
    enabled = true,
    resource = "lb_phone",
    events = {
        transfer_received = true,
        society_payroll_received = true,
        interest_credited = true,
        joint_deposit = true,
        joint_withdraw = true,
        joint_transfer = true,
        joint_member_added = true,
        joint_member_left = true,
    },
    appTitle = "Fleeca Bank",
    appIcon = "bank",
}
```

| Parametre | Description |
|-----------|-------------|
| `enabled` | Activer/desactiver les notifications telephone |
| `resource` | Script telephone utilise : `"lb_phone"`, `"qs-smartphone"` ou `"gksphone"` |
| `events` | Activation/desactivation par type d'evenement |
| `appTitle` | Titre affiche dans la notification telephone |
| `appIcon` | Icone de l'application dans la notification |

### Events disponibles

| Event | Description |
|-------|-------------|
| `transfer_received` | Virement recu sur le compte personnel |
| `society_payroll_received` | Salaire recu depuis la caisse societe |
| `interest_credited` | Interets credites sur le compte |
| `joint_deposit` | Depot sur un compte joint dont vous etes membre |
| `joint_withdraw` | Retrait sur un compte joint dont vous etes membre |
| `joint_transfer` | Virement depuis/vers un compte joint |
| `joint_member_added` | Nouveau membre ajoute a un compte joint |
| `joint_member_left` | Un membre a quitte un compte joint |

## Webhook Discord

```lua
Config.Webhook = {
    enabled = true,
    url = "",
    botName = "Fleeca Bank",
    color = 3899126,
}
```

| Parametre | Description |
|-----------|-------------|
| `enabled` | Activer/desactiver les webhooks Discord |
| `url` | URL du webhook Discord (laisser vide pour desactiver) |
| `botName` | Nom du bot affiche dans Discord |
| `color` | Couleur de l'embed Discord (entier decimal, `3899126` = bleu #3b82f6) |

> Toutes les operations sont loguees : depots, retraits, virements, operations societe, comptes joints, epargne et crypto.

## Epargne

```lua
Config.Savings = {
    enabled = true,
    interestRate = 3.0,
    interestCap = 50000,
    maxWithdrawalsPerDay = 1,
    minLockAmount = 1000,
    locks = {
        { days = 3,  rate = 2.0,  label = "3 jours"  },
        { days = 7,  rate = 5.0,  label = "7 jours"  },
        { days = 14, rate = 12.0, label = "14 jours" },
        { days = 30, rate = 30.0, label = "30 jours" },
    },
}
```

| Parametre | Description |
|-----------|-------------|
| `enabled` | Activer/desactiver le systeme d'epargne |
| `interestRate` | Taux d'interet de l'epargne classique (% par cycle de cron) |
| `interestCap` | Plafond maximum d'interets gagnes par periode |
| `maxWithdrawalsPerDay` | Nombre maximum de retraits depuis l'epargne par 24 heures |
| `minLockAmount` | Montant minimum pour un placement a terme |
| `locks` | Tableau des options de placement a terme |

### Options de placement a terme

| Parametre | Description |
|-----------|-------------|
| `days` | Duree du placement en jours |
| `rate` | Taux d'interet fixe applique a la fin du placement (%) |
| `label` | Libelle affiche dans l'interface |

> L'epargne est accessible **uniquement en banque** (pas depuis les ATM). Les interets sont calcules par un cron separe, online-only. L'epargne est exemptee de taxation.

## Crypto

```lua
Config.Crypto = {
    enabled = true,
    apiSource = "binance",
    refreshInterval = 5,
    coins = {
        { id = "bitcoin",  symbol = "BTC", label = "Bitcoin"  },
        { id = "ethereum", symbol = "ETH", label = "Ethereum" },
        { id = "litecoin", symbol = "LTC", label = "Litecoin" },
    },
    currency = "usd",
    minTradeAmount = 100,
    historyPerPage = 50,
}
```

| Parametre | Description |
|-----------|-------------|
| `enabled` | Activer/desactiver le trading crypto |
| `apiSource` | Source des prix : `"binance"`, `"coincap"` ou `"coinpaprika"` |
| `refreshInterval` | Intervalle en minutes entre chaque mise a jour des prix |
| `coins` | Liste des cryptomonnaies disponibles au trading |
| `currency` | Devise de reference pour les prix (ex: `"usd"`) |
| `minTradeAmount` | Montant minimum en $ pour un trade |
| `historyPerPage` | Nombre de trades affiches par page dans l'historique |

### Ajouter une cryptomonnaie

Ajoutez une entree dans le tableau `coins` :

```lua
{ id = "dogecoin", symbol = "DOGE", label = "Dogecoin" },
```

| Parametre | Description |
|-----------|-------------|
| `id` | Identifiant de la cryptomonnaie sur l'API (ex: `"bitcoin"`, `"ethereum"`) |
| `symbol` | Symbole court affiche dans l'interface (ex: `"BTC"`, `"ETH"`) |
| `label` | Nom complet affiche dans l'interface |

> L'identifiant `id` doit correspondre au slug utilise par l'API configuree (`apiSource`). Le crypto est accessible **uniquement en banque**. Les trades sont exempts de taxation.
