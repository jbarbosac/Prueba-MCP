# 🤖 Sistema de Agentes QA Multi-Célula para Generación Automática de Test Cases

> Sistema modular de generación de casos de prueba E2E organizado por células (Kepler, Pixel, Rocket, Skynet, Transversales) con integración directa a Azure DevOps.

---

## 📋 Tabla de Contenidos

- [Descripción General](#descripción-general)
- [Estructura del Proyecto](#estructura-del-proyecto)
- [Células y Modelos](#células-y-modelos)
- [Quick Start](#quick-start)
- [Agregar Nuevo Modelo](#agregar-nuevo-modelo)
- [Agregar Nueva Célula](#agregar-nueva-célula)
- [Arquitectura](#arquitectura)

---

## 🎯 Descripción General

Este sistema proporciona **arquitectura de agentes QA en 3 capas** organizados por células:
- ✅ **Agente Padre (QA_LEAD):** Orquestación global de las 5 células
- ✅ **Agentes Hijos por Célula:** Especialización por modelo/portal
- ✅ Generan casos de prueba E2E completos según ISTQB
- ✅ Crean test cases directamente en Azure DevOps Test Plans **mediante herramientas MCP**
- ✅ Mantienen trazabilidad con User Stories (HU)
- ✅ Optimizan uso de tokens mediante arquitectura modular y delegación inteligente

> **IMPORTANTE:** Todas las operaciones de Azure DevOps (crear casos, actualizar campos, agregar a suites, obtener HU) se ejecutan **exclusivamente mediante herramientas MCP** (Model Context Protocol). No se requiere intervención manual.

---

## 📁 Estructura del Proyecto

```
.github/
├── README.md                              ← Este archivo
├── CHANGELOG.md                           ← Historial de cambios
│
├── docs/                                  ← Documentación técnica
│   ├── GLOSSARY.md                       (Glosario de términos)
│   ├── ARCHITECTURE.md                   (Decisiones arquitecturales)
│   ├── CONTRIBUTING.md                   (Guía de contribución)
│   └── comparisons/                      (Comparativas por célula)
│       ├── Kepler_Models_Comparison.md
│       ├── Pixel_Models_Comparison.md
│       └── All_Cells_Comparison.md
│
├── templates/                             ← Plantillas reutilizables
│   ├── product-template.md               (Para agregar productos)
│   ├── portal-template.md                (Para agregar portales)
│   └── common-rules-template.md
│
├── agents/                                ← AGENTES QA
│   ├── QA_LEAD_Assistant.agent.md        (PADRE - Orquestador global)
│   │
│   ├── Kepler/                           ← CÉLULA KEPLER
│   │   ├── README.md
│   │   ├── PM_QA_Assistant.agent.md
│   │   ├── BGR_QA_Assistant.agent.md
│   │   ├── CME_QA_Assistant.agent.md
│   │   ├── CMP_QA_Assistant.agent.md
│   │   └── PROM_QA_Assistant.agent.md
│   │
│   ├── Pixel/                            ← CÉLULA PIXEL
│   │   └── README.md                     (Listo para agregar modelos)
│   │
│   ├── Rocket/                           ← CÉLULA ROCKET
│   │   └── README.md                     (Listo para agregar modelos)
│   │
│   ├── Skynet/                           ← CÉLULA SKYNET
│   │   └── README.md                     (Listo para agregar modelos)
│   │
│   └── Transversales/                    ← CÉLULA TRANSVERSALES
│       └── README.md                     (Listo para agregar modelos)
│
├── shared/                                ← REGLAS COMPARTIDAS
│   ├── SHARED_QA_RULES.md                (Universal - Todas las células)
│   │
│   ├── Kepler/
│   │   ├── PM_COMMON_RULES.md
│   │   ├── BGR_COMMON_RULES.md
│   │   └── [otros modelos...]
│   │
│   ├── Pixel/                            (Listo para agregar)
│   ├── Rocket/                           (Listo para agregar)
│   ├── Skynet/                           (Listo para agregar)
│   └── Transversales/                    (Listo para agregar)
│
├── products/                              ← FLUJOS E2E POR PRODUCTO
│   ├── Kepler/
│   │   ├── PM/
│   │   │   ├── PM_VUELOS.md
│   │   │   ├── PM_HOTELES.md
│   │   │   └── ...
│   │   ├── BGR/
│   │   │   ├── BGR_VUELOS.md
│   │   │   └── ...
│   │   └── [otros modelos]/
│   │
│   ├── Pixel/                            (Listo para agregar)
│   ├── Rocket/                           (Listo para agregar)
│   ├── Skynet/                           (Listo para agregar)
│   └── Transversales/                    (Listo para agregar)
│
└── imagenes/                              ← Recursos visuales
    ├── Kepler/
    │   ├── PM/
    │   └── BGR/
    ├── Pixel/
    ├── Rocket/
    ├── Skynet/
    └── Transversales/
```

---

## 🏢 Células y Modelos

### **📦 Célula KEPLER** (5 modelos configurados)

| Modelo | Agente | Prefijo | País | Estado |
|--------|--------|---------|------|--------|
| **Pichincha Miles** | Kepler/PM_QA_Assistant | [PM] | Ecuador | ✅ Activo |
| **BGR Miles** | Kepler/BGR_QA_Assistant | [BGR] | Ecuador | ✅ Activo |
| **Correos Millas Ecuador** | Kepler/CME_QA_Assistant | [CME] | Ecuador | ⏳ Pendiente |
| **Correos Millas Panamá** | Kepler/CMP_QA_Assistant | [CMP] | Panamá | ⏳ Pendiente |
| **Promerica Rewards** | Kepler/PROM_QA_Assistant | [PROM] | - | ⏳ Pendiente |

[Ver detalle →](agents/Kepler/README.md)

### **🎯 Célula PIXEL**

**Sin modelos configurados.** [Ver cómo agregar →](agents/Pixel/README.md)

### **🚀 Célula ROCKET**

**Sin modelos configurados.** [Ver cómo agregar →](agents/Rocket/README.md)

### **🤖 Célula SKYNET**

**Sin modelos configurados.** [Ver cómo agregar →](agents/Skynet/README.md)

### **🔄 Célula TRANSVERSALES**

**Sin modelos configurados.** [Ver cómo agregar →](agents/Transversales/README.md)

---

## 🚀 Quick Start

### 1. Seleccionar el agente correcto

| Rol/Necesidad | Agente | Cuándo usar |
|---------------|--------|-------------|
| **QA Lead / PM / Director** | `QA_LEAD_Assistant` | Visión global, orquestación multi-célula, análisis estratégico |
| **QA Kepler** | `Kepler/[MODELO]_QA_Assistant` | Crear casos PM, BGR, CME, CMP, Promerica |
| **QA Pixel** | `Pixel/[MODELO]_QA_Assistant` | Crear casos de modelos Pixel |
| **QA Rocket** | `Rocket/[MODELO]_QA_Assistant` | Crear casos de modelos Rocket |
| **QA Skynet** | `Skynet/[MODELO]_QA_Assistant` | Crear casos de modelos Skynet |
| **QA Transversales** | `Transversales/[MODELO]_QA_Assistant` | Crear casos de modelos Transversales |

### 2. Arquitectura Multi-Célula

```
                    QA_LEAD_Assistant
                    (Orquestador Global)
                            │
        ┌───────────┬───────┼──────┬──────────┬──────────┐
        │           │       │      │          │          │
    KEPLER      PIXEL   ROCKET  SKYNET  TRANSVERSALES
        │           │       │      │          │
  ┌─────┴────┐      │       │      │          │
  │  │  │  │ │      │       │      │          │
 PM BGR CME...      │       │      │          │
                [modelos] [modelos] [modelos] [modelos]
```

### 3. Preparar información (QA ejecutores)

### 3. Preparar información (QA ejecutores)

Antes de generar casos con **PM_QA_Assistant** o **BGR_QA_Assistant**, ten listo:
- ✅ `planId` (ID del Test Plan en Azure DevOps)
- ✅ `suiteId` (ID del Test Suite donde crear los casos)
- ✅ HU o contexto del caso a probar
- ✅ Producto específico (Vuelos, Hoteles, Autos, etc.)

**Ejemplo URL Azure DevOps:**
```
https://dev.azure.com/ultragrouplaorg/ultragroupla/_testPlans/define?planId=121536&suiteId=121850
                                                                            ↑            ↑
                                                                         planId      suiteId
```

### 4. Solicitar generación de casos (QA ejecutores)

**Ejemplo para PM Vuelos:**
```
"Genera un caso de prueba para PM Vuelos ida y vuelta SABRE con 1 adulto clase económica"
```

**Ejemplo para BGR Hoteles:**
```
"Genera un caso para BGR Hoteles 3 noches HotelBeds con pago Solo Millas automático"
```

### 5. Revisar y aprobar

El agente presentará una tabla con los casos generados. Revisa y confirma:
```
¿Procedo a crear los {N} casos en Azure DevOps en planId=121536 suiteId=121850? (sí/no/ajusta)
```

### 6. Validación automática

El agente creará los casos **UNO POR UNO** y mostrará un resumen:
```
✅ 5 casos creados exitosamente
✅ 5 casos agregados al suite 121850
✅ Trazabilidad establecida con HU #12345
```

---

## ➕ Agregar Nuevo Producto

### Paso 1: Copiar template

```powershell
# Para PM
Copy-Item templates/product-template.md products/PM_NUEVO_PRODUCTO.md

# Para BGR
Copy-Item templates/product-template.md products/BGR_NUEVO_PRODUCTO.md
```

### Paso 2: Completar metadata

```yaml
---
version: "1.0.0"
portal: "PM"  # o "BGR"
producto: "Nuevo Producto"
proveedor: "Nombre del proveedor"
ultima_actualizacion: "2026-01-05"
autor: "QA Team"
---
```

### Paso 3: Documentar flujo E2E

Completar:
- Pasos obligatorios desde login (mínimo 15-30 pasos)
- Validaciones críticas específicas
- Variaciones según escenarios
- Formato de título recomendado

### Paso 4: Actualizar agente

Agregar referencia en el agente correspondiente:

**PM_QA_Assistant.agent.md:**
```markdown
🎨 [PM_NUEVO_PRODUCTO.md](../products/PM_NUEVO_PRODUCTO.md) - Flujo E2E completo de Nuevo Producto
```

### Paso 5: Actualizar COMMON_RULES

Agregar a la tabla de proveedores en `PM_COMMON_RULES.md`:

```markdown
├─ 🎨 NUEVO PRODUCTO [Tecnología]
│  └─ Proveedor
```

### Paso 6: Validar

```powershell
# Ejecutar validación
.\validation\validate-structure.ps1
```

---

## 🌍 Agregar Nuevo Portal

### Paso 1: Crear estructura base

```powershell
# Crear archivo de agente
Copy-Item templates/portal-template.md agents/NUEVO_PORTAL_QA_Assistant.agent.md

# Crear reglas comunes
Copy-Item templates/portal-template.md shared/NUEVO_PORTAL_COMMON_RULES.md

# Crear carpeta de productos
New-Item -ItemType Directory -Path products/NUEVO_PORTAL/
```

### Paso 2: Configurar agente

En `NUEVO_PORTAL_QA_Assistant.agent.md`:
- Definir identificación (URL, país, prefijo)
- Establecer alcance y modelo de negocio
- Configurar referencias a COMMON_RULES
- Definir flujo de trabajo

### Paso 3: Documentar reglas comunes

En `NUEVO_PORTAL_COMMON_RULES.md`:
- Modelo de negocio específico
- Ecuación de pago
- Estructura de proveedores
- Formato de título específico
- Validaciones comunes

### Paso 4: Crear productos base

Por cada producto (Vuelos, Hoteles, etc.):
```powershell
Copy-Item templates/product-template.md products/NUEVO_PORTAL_VUELOS.md
```

### Paso 5: Actualizar documentación

- Agregar portal a este README.md
- Actualizar CHANGELOG.md
- Documentar diferencias en ARCHITECTURE.md

---

## 🔧 Mantenimiento

### Actualizar flujo de producto existente

1. Abrir archivo en `products/PM_PRODUCTO.md` o `BGR_PRODUCTO.md`
2. Editar sección correspondiente
3. Actualizar metadata `ultima_actualizacion`
4. Documentar cambio en CHANGELOG.md

### Cambiar modelo de negocio

1. Editar `shared/PM_COMMON_RULES.md` o `BGR_COMMON_RULES.md`
2. Revisar impacto en productos afectados
3. Actualizar productos si es necesario
4. Versionar cambio en CHANGELOG.md

### Agregar nueva validación

**Si es común a todos los productos:**
- Agregar a `shared/SHARED_QA_RULES.md` (aplica a PM y BGR)

**Si es específica de un portal:**
- Agregar a `shared/PM_COMMON_RULES.md` o `BGR_COMMON_RULES.md`

**Si es específica de un producto:**
- Agregar a `products/PORTAL_PRODUCTO.md`

---

## 🏗️ Arquitectura

### Principios de diseño

1. **Modularidad:** Cada archivo tiene un propósito único
2. **Carga bajo demanda:** Los agentes solo cargan lo necesario
3. **DRY:** Sin duplicación de información crítica
4. **Autocontenido:** Cada producto es independiente
5. **Escalabilidad:** Fácil agregar portales/productos

### Jerarquía de información

```
SHARED_QA_RULES.md (Universal)
        ↓
    COMMON_RULES (Por portal)
        ↓
    PRODUCT (Por producto específico)
        ↓
    AGENTE (Orchestrator)
```

### Optimización de tokens

| Arquitectura | Tokens por caso | Reducción |
|--------------|----------------|-----------|
| Monolítica (antes) | ~15,000 | - |
| Modular (actual) | ~7,500 | 50% |
| Con metadata | ~7,000 | 53% |

---

## 📚 Documentación Adicional

- [GLOSSARY.md](docs/GLOSSARY.md) - Glosario de términos técnicos
- [ARCHITECTURE.md](docs/ARCHITECTURE.md) - Decisiones arquitecturales (ADR)
- [CONTRIBUTING.md](docs/CONTRIBUTING.md) - Guía para contribuir
- [CHANGELOG.md](CHANGELOG.md) - Historial de cambios

---

## 📊 Estadísticas

- **Agentes:** 2 (PM, BGR)
- **Productos por portal:** 5 (Vuelos, Hoteles, Autos, Actividades, Disney)
- **Total archivos de flujos:** 10
- **Reglas compartidas:** 3 (SHARED, PM_COMMON, BGR_COMMON)
- **Líneas de código:** ~2,500
- **Optimización:** 45% reducción vs arquitectura monolítica

---

## ✅ Checklist de Calidad

Antes de crear casos de prueba, verificar:

- [ ] Agente correcto seleccionado (PM vs BGR)
- [ ] planId y suiteId disponibles
- [ ] Producto identificado (Vuelos, Hoteles, etc.)
- [ ] Proveedor conocido (si aplica)
- [ ] Modelo de pago definido (PM: millas+fee, BGR: slider)
- [ ] Criterios de aceptación claros
- [ ] Flujo E2E completo entendido

---

## 📚 Más Información

- 📘 [Comparación entre Modelos de Kepler](docs/comparisons/Kepler_Models_Comparison.md)
- 📋 [Reglas Comunes Compartidas](shared/SHARED_QA_RULES.md)
- ➕ [Guía Rápida: Agregar Nuevo Modelo](docs/QUICK_ADD_MODEL.md)
- 📝 [Historial de Cambios (CHANGELOG)](docs/CHANGELOG.md)

---

## 🤝 Contribución

Para agregar nuevos productos, portales o mejoras:

1. Consultar [CONTRIBUTING.md](docs/CONTRIBUTING.md)
2. Usar templates disponibles en `templates/`
3. Seguir convenciones de nomenclatura
4. Actualizar CHANGELOG.md
5. Validar con scripts de `validation/`

---

## 📝 Licencia

Uso interno Ultragroup La.

---

**Última actualización:** 2026-01-06  
**Versión:** 1.1.0  
**Mantenido por:** Sistema QA Multi-Célula
