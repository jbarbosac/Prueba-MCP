# 📁 KEPLER - Reglas Comunes de Marketplaces

## 🎯 Propósito

Esta carpeta contiene las reglas comunes compartidas para todos los portales marketplace gestionados por la célula **KEPLER**.

---

## 👥 CÉLULA KEPLER

**Team Manager:** Oscar Julian Buitrago Castro  
**Team Lead:** Fernando Zapata Montes  
**Producto Owner:** Maria Elena Osorio Henao  

### Equipo QA:
- Jesus Ernesto Marin Hernandez
- Jeferson Daniel Romero Quintero
- Jose Eulises Barbosa Colorado

### Equipo Frontend:
- Edwin David Molina Narvaez
- Oscar Andres Restrepo Echeverri
- Jorge Eduardo Mora Sepulveda

### Equipo Backend:
- Misael Correa Florez

---

## 📦 Archivos de este directorio

| Archivo | Portal | País | Prefijo | URL |
|---------|--------|------|---------|-----|
| **PM_COMMON_RULES.md** | Pichincha Miles | Ecuador | [PM] | https://pichinchamiles-ec.preprodppm.com/ |
| **BGR_COMMON_RULES.md** | BGR Miles | Ecuador | [BGR] | https://bgrmiles-ec.preprodppm.com/ |
| **CME_COMMON_RULES.md** | Correos Millas Ecuador | Ecuador | [CME] | https://correosmillas-ec.preprodppm.com/ |
| **PROM_COMMON_RULES.md** | Promerica | [Pendiente] | [PROM] | [Pendiente definir] |

---

## 🔗 Relación con Agentes

Cada archivo de reglas comunes está vinculado a un agente QA específico:

- `PM_COMMON_RULES.md` → **PM_QA_Assistant** (`.github/agents/PM_QA_Assistant.agent.md`)
- `BGR_COMMON_RULES.md` → **BGR_QA_Assistant** (`.github/agents/BGR_QA_Assistant.agent.md`)
- `CME_COMMON_RULES.md` → **CME_QA_Assistant** (`.github/agents/CME_QA_Assistant.agent.md`)
- `PROM_COMMON_RULES.md` → **PROM_QA_Assistant** (`.github/agents/PROM_QA_Assistant.agent.md`)

---

## 📚 Estructura de documentación

```
.github/
├── agents/                          # Agentes QA
│   ├── PM_QA_Assistant.agent.md
│   ├── BGR_QA_Assistant.agent.md
│   └── ...
│
├── shared/
│   ├── Kepler/                     # ← ESTÁS AQUÍ
│   │   ├── README.md               # Este archivo
│   │   ├── PM_COMMON_RULES.md      # Reglas PM
│   │   ├── BGR_COMMON_RULES.md     # Reglas BGR
│   │   ├── CME_COMMON_RULES.md     # Reglas CME
│   │   └── PROM_COMMON_RULES.md    # Reglas PROM
│   │
│   ├── SHARED_QA_RULES.md          # Fundamentos ISTQB y Azure DevOps
│   └── AGENT_CONTEXT_VALIDATION.md # Validación de contexto de agentes
│
└── products/
    └── B2B2C/
        └── PPM/
            ├── PM/                # Flujos E2E PM
            │   ├── PM_VUELOS.md
            │   ├── PM_AUTOS.md
            │   ├── PM_HOTELES.md
            │   ├── PM_ACTIVIDADES.md
            │   └── PM_DISNEY.md
            │
            ├── BGR/               # Flujos E2E BGR
            └── CME/               # Flujos E2E CME
```

---

## ✅ Uso recomendado

Cuando trabajes con un agente de Kepler:

1. **Leer primero:** `SHARED_QA_RULES.md` (fundamentos)
2. **Leer segundo:** El archivo `*_COMMON_RULES.md` del portal específico (ej: PM_COMMON_RULES.md)
3. **Leer tercero:** El archivo de flujo del producto específico (ej: PM_VUELOS.md)

---

## 🔄 Actualización

Este directorio debe mantenerse actualizado con:
- Cambios en modelos de negocio
- Nuevos proveedores
- Actualizaciones de equipos
- Nuevas validaciones de QA

**Última actualización:** 2026-02-05
