---
title: "Instalacion"
description: "Guia de instalacion del script foltone_blackmarket"
script: "foltone-blackmarket"
section: "Blackmarket"
order: 1
version: "1.0.0"
---

# Instalacion

## Requisitos

- **ox_lib** (obligatorio)
- **Un framework** : ESX, QBCore, QBox o standalone
- **Un inventario** : ox_inventory (recomendado), qs-inventory, esx o qb-inventory
- **Un sistema de target** (opcional pero recomendado) : ox_target, qb-target o qtarget

## Pasos de instalacion

### 1. Descargar el script

Coloque la carpeta `foltone_blackmarket` en su directorio `resources/[foltone]/`.

### 2. Anadir a server.cfg

```cfg
ensure foltone_blackmarket
```

Asegurese de que las dependencias se inician **antes** de este script :

```cfg
ensure ox_lib
ensure ox_inventory
ensure ox_target
ensure es_extended    # o qb-core / qbx_core
ensure foltone_blackmarket
```

### 3. Declarar los items del inventario

Si usa **ox_inventory**, los items ya se han anadido a `[OX]/ox_inventory/data/items.lua` :

- `bm_encrypted_phone` — telefono desechable que revela la posicion del van
- `bm_contact` — contacto underground (opcional, usado con `Config.RequireContactItem`)

Si usa otro inventario, anada estos dos items manualmente (vea Configuracion).

### 4. Configurar el script

Edite `config.lua` segun su servidor (locale, framework, dinero, ubicaciones, items...). Vea la seccion Configuracion.

### 5. Reiniciar el servidor

Reinicie su servidor, o ejecute en la consola :

```
refresh
ensure foltone_blackmarket
```

Al iniciar, el script muestra su version. Si hay una nueva version disponible, aparece una advertencia amarilla en la consola.

## Estructura de archivos

```
foltone_blackmarket/
├── bridge/           # Abstraccion multi-framework (ESX/QB/QBox/standalone)
├── client/           # Logica cliente (van, ped, menu, phone, preview)
├── server/           # Logica servidor (spawn, transactions, version check)
├── src/              # Libreria RageUI (menu in-game)
├── html/             # Menu NUI (alternativa HTML/CSS)
├── locales/          # Traducciones (fr / en / es)
├── config.lua        # Configuracion principal
├── trad.lua          # Sistema de traduccion
└── fxmanifest.lua
```

## Problemas comunes

| Problema | Solucion |
|---|---|
| La interaccion no funciona | Compruebe que ox_target / qb-target esta iniciado, o ponga `Config.TargetSystem = 'none'` |
| Las armas 3D no se muestran | Build de GTA V reciente : verifique que `RequestWeaponAsset` funciona en consola |
| El menu no se abre | Compruebe `Config.MenuType` (`'rageui'` o `'nui'`) |
| El van nunca aparece | Compruebe que `Config.SpawnLocations` no esta vacio |
| Telefono cifrado sin efecto | Verifique que el item esta declarado en items.lua de su inventario con `server.export` hacia `foltone_blackmarket.useEncryptedPhone` |
