---
title: "Configuración"
description: "Configuración del script Brasseur"
script: "foltone-brasseur"
section: "Brasseur"
order: 2
version: "2.0.0"
---

# Configuración — foltone_brasseur

```lua
Config.JobName = 'brasseur'
Config.SocietyName = 'society_brasseur'
```

## Pipeline

| Paso | Producto | Insumo | Pago |
|------|----------|--------|------|
| Cosecha | `houblon` | — | — |
| Transformación | `biere_blonde` | 1x `houblon` | — |
| Transformación | `biere_rousse` | 2x `houblon` | — |
| Venta | — | `biere_blonde` | $5 + $20 |
| Venta | — | `biere_rousse` | $15 + $40 |

3 cofres: Principal (grado 0), Chef (grado 2), Jefe (grado 3).
