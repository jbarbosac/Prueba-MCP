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
│   ├── Kepler/
│   │   ├── README.md
│   │   ├── PM_QA_Assistant.agent.md
│   │   └── BGR_QA_Assistant.agent.md
│   ├── Pixel/
│   │   └── README.md
│   ├── Rocket/
│   │   └── README.md
│   ├── Skynet/
│   │   └── README.md
│   └── Transversales/
│       └── README.md
│
├── shared/
│   ├── SHARED_QA_RULES.md
│   └── Kepler/
│       ├── PM_COMMON_RULES.md
│       └── BGR_COMMON_RULES.md
│
├── products/
│   └── Kepler/
│       ├── PM/
│       │   ├── PM_VUELOS.md
│       │   ├── PM_HOTELES.md
│       │   ├── PM_AUTOS.md
│       │   ├── PM_ACTIVIDADES.md
│       │   └── PM_DISNEY.md
│       └── BGR/
│           └── BGR_VUELOS.md
│
├── docs/
│   ├── comparisons/
│   │   └── Kepler_Models_Comparison.md
│   ├── QUICK_ADD_MODEL.md                 (nuevo)
│   └── CHANGELOG.md                        (este archivo)
│
└── templates/
    ├── portal-template.md
    └── product-template.md
```

#### 🔄 Migrado
- **Agentes:** Movidos de raíz a `agents/Kepler/`
- **Reglas Comunes:** Movidas a `shared/Kepler/`
- **Productos:** Movidos a `products/Kepler/`
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
