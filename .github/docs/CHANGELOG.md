# 📝 CHANGELOG - Sistema QA Multi-Célula

Registro de cambios del sistema de agentes QA para Azure DevOps.

---

## [v1.1.0] - 2026-01-06

### 🎉 Nueva Arquitectura: Multi-Célula

#### ➕ Agregado
- **Estructura Multi-Célula:** Reorganización completa del sistema en 5 células independientes:
  - 🔷 **Kepler:** Célula principal (5 modelos: PM, BGR, CME, CMP, Promerica)
  - 🎯 **Pixel:** Estructura lista, sin modelos configurados
  - 🚀 **Rocket:** Estructura lista, sin modelos configurados
  - 🤖 **Skynet:** Estructura lista, sin modelos configurados
  - 🔄 **Transversales:** Estructura lista, sin modelos configurados

- **Agente QA_LEAD_Assistant:** Agente padre con capacidad de orquestación global
  - Puede delegar a un solo agente de cualquier célula
  - Puede orquestar todos los modelos de una célula
  - Puede orquestar múltiples células simultáneamente
  - Puede ejecutar operaciones globales en TODAS las células

- **README por Célula:** Cada célula tiene su propio README con:
  - Tabla de modelos (vacía o poblada)
  - Instrucciones paso a paso para agregar modelos
  - Estructura esperada de carpetas
  - Enlaces a templates y ejemplos

- **Guía Rápida:** `docs/QUICK_ADD_MODEL.md` con proceso completo de agregar modelos

#### 📂 Estructura de Carpetas
```
.github/
├── agents/
│   ├── QA_LEAD_Assistant.agent.md         (padre global)
│   ├── PM_QA_Assistant.agent.md           (Kepler/PM)
│   ├── BGR_QA_Assistant.agent.md          (Kepler/BGR)
│   └── CME_QA_Assistant.agent.md          (Kepler/CME)
│
├── shared/
│   ├── SHARED_QA_RULES.md
│   ├── AGENT_CONTEXT_VALIDATION.md
│   └── Kepler/
│       ├── PM_COMMON_RULES.md
│       ├── BGR_COMMON_RULES.md
│       └── CME_COMMON_RULES.md
│
├── products/
│   ├── B2B2C/
│   │   └── PPM/
│   │       ├── PM/
│   │       │   ├── PM_VUELOS.md
│   │       │   ├── PM_HOTELES.md
│   │       │   ├── PM_AUTOS.md
│   │       │   ├── PM_ACTIVIDADES.md
│   │       │   └── PM_DISNEY.md
│   │       ├── BGR/
│   │       │   ├── BGR_VUELOS.md
│   │       │   ├── BGR_HOTELES.md
│   │       │   ├── BGR_AUTOS.md
│   │       │   ├── BGR_ACTIVIDADES.md
│   │       │   └── BGR_DISNEY.md
│   │       ├── CME/
│   │       │   ├── CME_VUELOS.md
│   │       │   ├── CME_HOTELES.md
│   │       │   ├── CME_AUTOS.md
│   │       │   ├── CME_ACTIVIDADES.md
│   │       │   └── CME_DISNEY.md
│   │       └── CMP/
│   ├── B2B/
│   │   └── [modelos B2B]
│   └── B2C/
│       └── [modelos B2C]
│
├── docs/
│   ├── B2B2C/PPM/
│   │   ├── PM/README.md
│   │   ├── BGR/README.md
│   │   ├── CME/README.md
│   │   └── CMP/README.md
│   ├── comparisons/
│   │   ├── Kepler_Models_Comparison.md
│   │   └── All_Cells_Comparison.md
│   ├── QUICK_ADD_MODEL.md
│   ├── ARCHITECTURE.md
│   └── CHANGELOG.md                        (este archivo)
│
├── images/
│   └── [recursos visuales]
│
└── templates/
    ├── portal-template.md
    └── product-template.md
```

#### 🔄 Migrado
- **Agentes:** Organizados en raíz de `agents/` sin subcarpetas por célula
- **Reglas Comunes:** Organizadas en `shared/Kepler/`
- **Productos:** Organizados por modelo de negocio `products/B2B2C/PPM/`
- **Docs:** Organizados por modelo de negocio `docs/B2B2C/PPM/`
- **Referencias:** Todas las rutas actualizadas en agentes existentes

#### ✅ Capacidades de Orquestación

**Nivel 1: Delegación Simple**
- QA_LEAD → Agente de modelo específico
- Ejemplo: "Crea caso de checkout para PM"

**Nivel 2: Orquestación de Célula**
- QA_LEAD → Todos los modelos de Kepler
- Ejemplo: "Crea caso de checkout para todos los modelos de Kepler"

**Nivel 3: Orquestación Multi-Célula**
- QA_LEAD → Modelos específicos de múltiples células
- Ejemplo: "Crea caso de checkout para Kepler y Pixel"

**Nivel 4: Orquestación Global**
- QA_LEAD → TODAS las células
- Ejemplo: "Crea caso de checkout para TODAS las células"

#### 📋 Uso según Rol

**QA Lead (global):**
- Usa: `QA_LEAD_Assistant`
- Alcance: Todas las células
- Casos de uso: Visión global, casos masivos, comparaciones

**QA de Célula (táctico):**
- Usa: Agente específico del modelo (ej: `PM_QA_Assistant`)
- Alcance: Un modelo específico
- Casos de uso: Ejecución detallada, casos específicos

---

## [v1.0.0] - 2026-01-05

### 🎉 Versión Inicial

#### ➕ Agregado
- **Agentes Especializados:**
  - `PM_QA_Assistant.agent.md` (Pichincha Miles)
  - `BGR_QA_Assistant.agent.md` (BGR Miles)

- **Reglas Comunes:**
  - `SHARED_QA_RULES.md` (reglas globales)
  - `PM_COMMON_RULES.md` (específicas PM)
  - `BGR_COMMON_RULES.md` (específicas BGR)

- **Flujos de Productos:**
  - PM: Vuelos, Hoteles, Autos, Actividades, Disney
  - BGR: Vuelos

- **Templates:**
  - `portal-template.md`
  - `product-template.md`

- **Documentación:**
  - `README.md` principal
  - `Kepler_Models_Comparison.md`

#### 🔧 Configuración
- Integración con Azure DevOps via MCP
- Formato obligatorio: `[PREFIJO] [Producto] - [Escenario] - [Variante]`
- Estados de reserva: 10-15 (PM), 14-15 (BGR)

---

## 🔮 Roadmap

### v1.2.0 (Pendiente)
- [ ] Completar modelos de Kepler (CME, CMP, Promerica)
- [ ] Primer modelo en Pixel
- [ ] Comparación automática entre células

### v1.3.0 (Pendiente)
- [ ] Poblado de Rocket, Skynet, Transversales
- [ ] Dashboard de cobertura por célula
- [ ] Métricas de casos por modelo

### v2.0.0 (Futuro)
- [ ] Integración con CI/CD
- [ ] Ejecución automática de casos
- [ ] Reportes automáticos de cobertura

---

**Última actualización:** 2026-01-06  
**Mantenido por:** Sistema QA Multi-Célula
