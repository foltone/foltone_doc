---
title: "Utilisation"
description: "Guide d'utilisation du script Foltone Banking"
script: "foltone-banking"
section: "foltone_banking"
order: 3
version: "1.0.0"
---

# Utilisation — foltone_banking

## Fonctionnement general

Foltone Banking est un script bancaire complet pour FiveM avec une interface NUI moderne (design "Street / GTA - Blue Edition"). Il propose des comptes personnels, societe, joints, un systeme d'epargne, du trading crypto, un score de credit, des niveaux de compte et une taxation progressive.

## Acces a l'interface

L'interface bancaire est accessible de trois manieres :

| Point d'acces | Description | Fonctionnalites |
|---------------|-------------|-----------------|
| **PED Banquier** | PED present dans chaque banque configuree | Toutes les fonctionnalites (perso, societe, joint, epargne, crypto) |
| **ATM** | Distributeur automatique sur la map | Fonctionnalites de base (depot, retrait, virement, historique) |
| **PED Societe** | PED comptable sur le lieu de travail | Acces direct au compte societe du job |

Le mode d'interaction depend de la configuration (`Config.InteractionType`) :

- **marker** / **drawtext** : Approchez-vous et appuyez sur **E**
- **ox_target** / **qb-target** / **qtarget** : Visez le PED/ATM avec le curseur 3D

## Tableau de bord

Le tableau de bord est la page d'accueil de l'interface bancaire. Il affiche :

- **Solde actuel** du compte personnel
- **Numero IBAN** unique du compte
- **Courbe d'evolution** du solde dans le temps
- **Score de credit** avec barre de progression (0-1000)
- **Niveau du compte** (Standard ou Premium) avec badge
- **Bouton d'upgrade** vers Premium (si eligible)

### Depot et retrait

1. Entrez le montant souhaite
2. Un **apercu de la taxe** s'affiche en temps reel sous le champ de saisie
3. Confirmez l'operation
4. Le solde et le score de credit sont mis a jour automatiquement

> La taxe est calculee selon les tranches progressives configurees. Les comptes Premium beneficient d'une reduction de 25%.

## Virements

La page Virements permet d'envoyer de l'argent a un autre joueur.

### Mode ID serveur

1. Selectionnez le mode **ID Serveur**
2. Entrez l'**ID du joueur** destinataire (visible en jeu)
3. Entrez le **montant**
4. L'apercu de la taxe s'affiche
5. Confirmez le virement

### Mode IBAN

1. Selectionnez le mode **IBAN**
2. Entrez le **numero IBAN** du destinataire
3. Le systeme **resout l'IBAN** et affiche le nom du titulaire (comptes personnels et joints)
4. Entrez le **montant**
5. Confirmez le virement

> Les virements par IBAN fonctionnent meme si le destinataire est **hors ligne** (si `offlineTransfer` est active). Les virements vers des IBAN de comptes joints sont egalement supportes.

## Historique des transactions

La page Historique affiche toutes les operations du compte personnel avec pagination.

### Filtres disponibles

| Filtre | Transactions affichees |
|--------|----------------------|
| **Tout** | Toutes les transactions |
| **Depots** | Depots uniquement |
| **Retraits** | Retraits uniquement |
| **Virements** | Virements entrants et sortants |
| **Interets** | Interets credites |
| **Taxes** | Taxes prelevees |

Chaque transaction affiche un **badge** indiquant son type (depot, retrait, virement, interet, taxe, upgrade).

## Carte bancaire

La page Carte affiche les informations de votre carte bancaire :

- **Numero de carte** unique
- **Code PIN** actuel

### Actions disponibles

| Action | Description | Cout |
|--------|-------------|------|
| **Changer le PIN** | Modifier le code PIN de la carte | Configurable (`pinChangePrice`) |
| **Bloquer / Debloquer** | Activer ou desactiver la carte | Gratuit |
| **Reediter** | Obtenir une nouvelle carte (nouveau numero) | Configurable (`reissuePrice`) |

## Comptes societe

Les comptes societe sont accessibles aux joueurs ayant le grade requis (boss, manager, ou grades configures par job).

### Acces

- Depuis une **banque** ou un **ATM** : onglet Societe dans la sidebar (visible uniquement si le joueur a les permissions)
- Depuis le **PED societe** : acces direct si un PED est configure sur le lieu de travail

### Pages societe

#### Dashboard societe

- **Solde** de la caisse societe
- **Depot** depuis l'argent personnel vers la caisse
- **Retrait** de la caisse vers l'argent personnel

#### Virements societe

Virement externe depuis la caisse societe vers un compte personnel :

1. Entrez l'**ID serveur** ou l'**IBAN** du destinataire
2. Entrez le **montant**
3. Confirmez le virement

> Les operations societe sont **exemptees de taxation**.

#### Payroll (Paie)

Payer un employe directement depuis la caisse societe :

1. Entrez l'**ID serveur** de l'employe
2. Entrez le **montant**
3. Confirmez le paiement

Le salaire est credite sur le compte bancaire de l'employe. L'employe recoit une notification telephone (si configuree).

#### Historique societe

Historique complet des operations societe avec :

- **Nom** et **grade** de l'employe ayant effectue l'operation
- **Type** d'operation (depot, retrait, virement, payroll)
- **Montant** et **date**

## Comptes joints

Les comptes joints permettent a plusieurs joueurs de partager un compte bancaire commun.

> **Important** : Les comptes joints sont accessibles **uniquement en banque** (pas depuis les ATM).

### Creer un compte joint

1. Accedez a la section **Compte joint** dans la sidebar
2. Cliquez sur **Creer un compte joint**
3. Un nouveau compte est cree avec un IBAN unique
4. Vous en etes automatiquement le premier membre

### Ajouter un membre

1. Selectionnez le compte joint
2. Entrez l'**ID serveur** du joueur a ajouter
3. Confirmez l'ajout

> Le nombre maximum de membres et de comptes par joueur est configurable.

### Operations sur un compte joint

| Operation | Description |
|-----------|-------------|
| **Depot** | Transferer de l'argent personnel vers le compte joint |
| **Retrait** | Retirer de l'argent du compte joint vers son compte personnel |
| **Virement** | Envoyer de l'argent du compte joint vers un IBAN externe |

### Quitter un compte joint

1. Selectionnez le compte joint
2. Cliquez sur **Quitter**
3. Confirmez la sortie

> Les comptes joints ne sont pas soumis a la taxation, aux interets ni au score de credit. Le serveur valide le membership a chaque operation (anti-triche).

## Epargne classique

L'epargne classique est un compte a part du compte courant, avec un taux d'interet plus eleve.

> Accessible **uniquement en banque**.

### Depot sur l'epargne

1. Accedez a la page **Epargne** dans la sidebar
2. Entrez le montant a placer
3. Confirmez le depot

### Retrait de l'epargne

1. Entrez le montant a retirer
2. Confirmez le retrait

> Le nombre de retraits est **limite par jour** (configurable via `maxWithdrawalsPerDay`).

### Interets de l'epargne

Les interets sont calcules automatiquement par un cron serveur a intervalle regulier. Ils ne sont credites qu'aux joueurs **connectes**.

- **Taux** : configurable (`interestRate`)
- **Plafond** : configurable (`interestCap`)

## Placements a terme

Les placements a terme permettent de bloquer une somme pour une duree fixe en echange d'un taux d'interet garanti.

### Effectuer un placement

1. Sur la page Epargne, choisissez une **duree** parmi les options proposees (3, 7, 14 ou 30 jours)
2. Entrez le **montant** a placer (minimum configurable)
3. Confirmez le placement

### Suivi du placement

- Une **barre de progression** indique l'avancement du placement
- La date de deblocage est affichee

### Recuperer le placement

Une fois la duree ecoulee :

1. Le bouton **Recuperer** devient actif
2. Cliquez pour recuperer le **capital + les interets**
3. Le montant est credite sur votre compte d'epargne

> Les placements utilisent un timestamp absolu (`unlocks_at`), ils survivent aux redemarrages du serveur.

## Trading crypto

Le systeme de trading crypto permet d'acheter et vendre des cryptomonnaies avec des prix en temps reel.

> Accessible **uniquement en banque**.

### Marche

La page Marche affiche les cryptomonnaies disponibles avec :

- **Prix actuel** mis a jour en temps reel (depuis Binance, CoinCap ou CoinPaprika)
- **Variation** du prix

#### Acheter

1. Selectionnez une cryptomonnaie
2. Entrez le **montant en $** a investir (minimum configurable)
3. Confirmez l'achat
4. La quantite de crypto correspondante est creditee dans votre portefeuille

### Portefeuille

La page Portefeuille affiche vos positions :

- **Quantite** detenue par cryptomonnaie
- **Prix moyen d'achat**
- **P&L** (Profit & Loss) en $ et en % pour chaque position
- **P&L total** du portefeuille

#### Vendre

1. Selectionnez une cryptomonnaie dans votre portefeuille
2. Entrez la **quantite a vendre**
3. Ou cliquez sur **Tout vendre** pour vendre la totalite
4. Confirmez la vente
5. Le montant en $ est credite sur votre compte bancaire

### Historique des trades

La page Historique Trades affiche toutes vos operations crypto avec pagination et filtres (achat/vente).

> Les trades crypto sont **exempts de taxation**. Le systeme anti-double-spend verifie le solde en base avant chaque operation.

## Systeme de score de credit

Le score de credit est un indicateur numerique (0-1000) qui reflete le comportement bancaire du joueur.

### Actions qui modifient le score

| Action | Points |
|--------|--------|
| Depot | +2 |
| Retrait | -1 |
| Virement envoye | +1 |
| Virement recu | +1 |
| Upgrade de compte | +5 |

Le score influence :

- Le **taux d'interet** effectif sur le compte courant
- L'**eligibilite a l'upgrade Premium** (score minimum requis)

## Niveaux de compte

### Standard

Le niveau par defaut pour tous les nouveaux comptes.

### Premium

Niveau superieur offrant des avantages :

| Avantage | Standard | Premium |
|----------|----------|---------|
| Taux d'interet | 0.5% | 1.5% |
| Plafond d'interets | $5 000 | $20 000 |
| Limite de virement | $50 000 | $200 000 |
| Reduction taxes | 0% | 25% |

### Conditions d'upgrade

- **Score de credit minimum** : 700 (configurable)
- **Cout de l'upgrade** : $50 000 (configurable)

L'upgrade s'effectue depuis le tableau de bord, via le bouton prevu a cet effet.

## Taxation progressive

La taxation fonctionne par **tranches** sur les depots, retraits et virements personnels.

### Exemple avec la configuration par defaut (depot)

| Tranche | Taux |
|---------|------|
| $0 - $10 000 | 0% (pas de taxe) |
| $10 000 - $50 000 | 2% |
| $50 000+ | 5% |

Seule la portion du montant dans chaque tranche est taxee au taux correspondant.

### Exemptions

Les operations suivantes sont **exemptees de taxation** :

- Operations societe (depot, retrait, virement, payroll)
- Operations sur comptes joints
- Operations d'epargne
- Trades crypto

### Reduction Premium

Les comptes Premium beneficient d'une reduction de **25%** sur le montant total de la taxe.

## Interets

Les interets sont calcules automatiquement par un cron serveur a intervalle configurable (par defaut toutes les 60 minutes).

### Caracteristiques

- **Online-only** : seuls les joueurs connectes recoivent des interets
- **Module par le score de credit** : un score plus eleve ameliore le taux effectif
- **Plafond par niveau** : le montant d'interets est limite par periode (24h par defaut)
- **Cron separe pour l'epargne** : les interets du compte epargne sont calcules independamment

## Notifications telephone

Si un script telephone est configure, certaines operations declenchent une notification in-game :

| Evenement | Description |
|-----------|-------------|
| `transfer_received` | Vous recevez un virement sur votre compte |
| `society_payroll_received` | Vous recevez un salaire depuis la caisse societe |
| `interest_credited` | Des interets sont credites sur votre compte |
| `joint_deposit` | Un membre effectue un depot sur un compte joint partage |
| `joint_withdraw` | Un membre effectue un retrait sur un compte joint partage |
| `joint_transfer` | Un virement est effectue depuis/vers un compte joint partage |
| `joint_member_added` | Un nouveau membre rejoint un compte joint |
| `joint_member_left` | Un membre quitte un compte joint |

> Les notifications telephone ne sont envoyees qu'aux joueurs **connectes**.

## Webhook Discord

Toutes les operations bancaires sont loguees vers un webhook Discord lorsque cette fonctionnalite est activee :

- Depots et retraits (personnels, societe, joint, epargne)
- Virements (personnels, societe, joint)
- Payroll societe
- Trades crypto (achat et vente)
- Interets credites
- Taxes prelevees
- Upgrades de compte
- Creations et modifications de comptes joints
- Placements a terme et reclamations

> Les webhooks sont envoyes en mode **fire-and-forget** via `PerformHttpRequest` et n'impactent pas les performances du serveur.

## Events disponibles

### Callbacks serveur

```lua
-- Recuperer les donnees du compte personnel
TriggerServerFoltoneBKCallback("foltone_banking:getAccountData", function(data)
    -- data.balance, data.iban, data.credit_score, data.account_level, etc.
end)

-- Recuperer l'historique des transactions
TriggerServerFoltoneBKCallback("foltone_banking:getHistory", function(data)
    -- data.transactions, data.total, data.page
end, page, filter)

-- Resoudre un IBAN (perso + joint)
TriggerServerFoltoneBKCallback("foltone_banking:resolveIBAN", function(data)
    -- data.name, data.type ("personal" ou "joint")
end, iban)

-- Recuperer les donnees societe
TriggerServerFoltoneBKCallback("foltone_banking:getSocietyData", function(data)
    -- data.balance
end)

-- Recuperer les comptes joints
TriggerServerFoltoneBKCallback("foltone_banking:getJointAccounts", function(data)
    -- data.accounts (tableau)
end)

-- Recuperer les donnees d'epargne
TriggerServerFoltoneBKCallback("foltone_banking:getSavingsData", function(data)
    -- data.balance, data.locks
end)

-- Recuperer les donnees crypto
TriggerServerFoltoneBKCallback("foltone_banking:getCryptoData", function(data)
    -- data.holdings, data.prices
end)
```

### Events serveur

```lua
-- Operations personnelles
TriggerServerEvent("foltone_banking:deposit", amount)
TriggerServerEvent("foltone_banking:withdraw", amount)
TriggerServerEvent("foltone_banking:transfer", targetId, amount, mode)
TriggerServerEvent("foltone_banking:changePin", newPin)
TriggerServerEvent("foltone_banking:toggleCardBlock")
TriggerServerEvent("foltone_banking:reissueCard")
TriggerServerEvent("foltone_banking:upgradeAccount")

-- Operations societe
TriggerServerEvent("foltone_banking:societyDeposit", amount)
TriggerServerEvent("foltone_banking:societyWithdraw", amount)
TriggerServerEvent("foltone_banking:societyTransfer", targetId, amount, mode)
TriggerServerEvent("foltone_banking:societyPayroll", targetId, amount)

-- Operations compte joint
TriggerServerEvent("foltone_banking:createJointAccount")
TriggerServerEvent("foltone_banking:addJointMember", jointAccountId, targetId)
TriggerServerEvent("foltone_banking:leaveJointAccount", jointAccountId)
TriggerServerEvent("foltone_banking:jointDeposit", jointAccountId, amount)
TriggerServerEvent("foltone_banking:jointWithdraw", jointAccountId, amount)
TriggerServerEvent("foltone_banking:jointTransfer", jointAccountId, targetIBAN, amount)

-- Operations epargne
TriggerServerEvent("foltone_banking:savingsDeposit", amount)
TriggerServerEvent("foltone_banking:savingsWithdraw", amount)
TriggerServerEvent("foltone_banking:savingsLock", amount, lockIndex)
TriggerServerEvent("foltone_banking:savingsClaim", lockId)

-- Operations crypto
TriggerServerEvent("foltone_banking:cryptoBuy", cryptoId, amount)
TriggerServerEvent("foltone_banking:cryptoSell", cryptoId, quantity)
```
