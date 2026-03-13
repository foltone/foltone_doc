---
title: "Installation générale"
description: "Guide d'installation commun à tous les scripts"
script: "getting-started"
section: "Getting Started"
order: 2
---

# Installation générale

Ce guide s'applique à tous les scripts Foltone.

## Prérequis

- Un serveur FiveM fonctionnel
- **QB-Core** ou **ESX Legacy** installé (sauf scripts standalone)
- Accès FTP ou fichiers du serveur

## Étapes d'installation

### 1. Télécharger le script

**Scripts gratuits :** Clonez le repo GitHub ou téléchargez le ZIP.

```bash
cd resources
git clone https://github.com/foltone/foltone_SCRIPT
```

**Scripts payants :** Téléchargez depuis votre espace Tebex après achat.

### 2. Placer dans les resources

Déplacez le dossier du script dans votre dossier `resources/` :

```
server/
├── resources/
│   ├── [es_extended] ou [qb-core]/
│   └── foltone_SCRIPT/
│       ├── client/
│       ├── server/
│       ├── config.lua
│       └── fxmanifest.lua
```

### 3. Ajouter au server.cfg

```ini
ensure foltone_SCRIPT
```

### 4. Importer la base de données (si nécessaire)

Certains scripts incluent un fichier `sql/install.sql`. Importez-le dans votre base de données :

```sql
-- Exemple : import via HeidiSQL, phpMyAdmin ou CLI
mysql -u root -p votre_base < sql/install.sql
```

### 5. Configurer

Ouvrez `config.lua` et adaptez les paramètres à votre serveur. Consultez la page **Configuration** de chaque script pour les détails.

### 6. Redémarrer

```
restart foltone_SCRIPT
```

## Problèmes courants

| Problème | Solution |
|----------|----------|
| Script non détecté | Vérifiez le nom dans `server.cfg` |
| Erreur SQL | Importez le fichier `install.sql` |
| Dépendance manquante | Installez `ox_lib`, `ox_inventory` si requis |
| Resmon élevé | Vérifiez la version du framework |
