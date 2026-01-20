# 🤖 Sistema de Agentes QA Multi-Célula para Generación Automática de Test Cases

> Sistema modular de generación de casos de prueba E2E organizado por células (Kepler, Pixel, Rocket, Skynet, Transversales) con integración directa a Azure DevOps.
---

## �📋 Tabla de Contenidos

- [Descripción General](#descripción-general)
- [Estructura del Proyecto](#estructura-del-proyecto)
- [Células y Modelos](#células-y-modelos)
- [Quick Start](#quick-start)
- [Agregar Nuevo Modelo](#agregar-nuevo-modelo)
- [Agregar Nueva Célula](#agregar-nueva-célula)
- [Arquitectura](#arquitectura)

---

## � Organización por Células y Equipos

### 🤖 **Célula A - Skynet**
**Alcance:** PCO, Mastercard, BAC  
**Líder TM:** Juan Camilo Estrada 
**Equipo QA:**
- Jenny Marcela Florez Hinestroza
- Carlos Alberto Rubio Gallego
- Natalia Gallego Rios
 
---

### 📦 **Célula B - Kepler**
**Alcance:** PPM (Pichincha Miles, BGR Miles, Club Miles Ecuador, Club Millas Perú, Promerica Rewards)  

**Líder TM:** Oscar Julian Buitrago Castro

**Líder TL:** Fernando Zapata Montes

**PO PPM:** Santiago Alvarez Perez

**PO ILS:** Daniela Garcia Dederle

**Equipo QA:**
- Jose Eulises Barbosa Colorado
- Jesus Ernesto Marin Hernandez
- Jeferson Daniel Romero Quintero

**FronTend:**
- Victor Alejandro Prada Noreña
- Sergio Alejandro Riaños Acosta
- Cristian David Velez Torres

**Backend:**
- Juan Carlos GHonzalez Sancjez

**Agentes Activos:** 5 (PM, BGR, CME, CMP, Promerica) ✅

---

### 🎯 **Célula C - Pixel**
**Alcance:** Aereo, Autos, Disney, Hoteles, Modernización  
**Líder:** Santiago Monsalve Calderon  
**Equipo QA:**
- Camilo Pelaez Ramirez
- Yhonatan Urrea Tascon
- Andres Felipe Sanchez Caicedo

---

### 🚀 **Célula E - Rocket**
**Alcance:** Proyecto Fidelity / Muscle Interno  
**Líder:** Cristian Garzon Sanchez  
**Equipo QA:**
- Diego Fernando Castellanos Vargas
- Juan David Ceballos Cogollo
- Emma Del Carmen Gonzalez Sanchez

---

### 📊 Resumen de Células

| Célula | Líder | # Miembros | Agentes QA |
|--------|-------|------------|------------|
| 🤖 **A-Skynet** | Juan Camilo Estrada | 3 | Pendiente |
| 📦 **B-Kepler** | Oscar Julian Buitrago Castro | 3 | ✅ 5 activos |
| 🎯 **C-Pixel** | Santiago Monsalve Calderon | 3 | Pendiente |
| 🚀 **E-Rocket** | Cristian Garzon Sanchez | 3 | Pendiente |

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
├── docs/                                  ← Documentación técnica organizada por modelo de negocio
│   ├── GLOSSARY.md                       (Glosario de términos)
│   ├── ARCHITECTURE.md                   (Decisiones arquitecturales)
│   ├── CONTRIBUTING.md                   (Guía de contribución)
│   ├── QUICK_ADD_MODEL.md                (Guía rápida para agregar modelos)
│   ├── AGENT_ARCHITECTURE_SECURITY.md     (Seguridad de agentes)
│   ├── AGENT_RESPONSE_PERMISSIONS.md      (Permisos de respuesta de agentes)
│   ├── comparisons/                      (Comparativas por célula)
│   │   ├── Kepler_Models_Comparison.md
│   │   └── All_Cells_Comparison.md
│   │
│   ├── B2B2C/                            ← Modelo B2B2C (PPM)
│   │   └── PPM/
│   │       ├── PM/
│   │       │   └── README.md
│   │       ├── BGR/
│   │       │   └── README.md
│   │       ├── CME/
│   │       │   └── README.md
│   │       └── CMP/
│   │           └── README.md
│   │
│   ├── B2B/                              ← Modelo B2B
│   │   ├── PPM/
│   │   │   └── CORPORATIVO USD/
│   │   │       └── README.md
│   │   └── ULTRA/
│   │       ├── CONSOLIDACION COP/
│   │       │   └── README.md
│   │       └── CONSOLIDACION USD/
│   │           └── README.md
│   │
│   └── B2C/                              ← Modelo B2C
│       ├── ULTRA/
│       │   ├── VACACIONAL COP/
│       │   │   └── README.md
│       │   └── VACACIONAL USD/
│       │       └── README.md
│       └── AVASA/
│           └── VIVA AEROBUS/
│               └── README.md
│
├── templates/                             ← Plantillas reutilizables
│   ├── product-template.md               (Para agregar productos)
│   └── portal-template.md                (Para agregar portales)
│
├── agents/                                ← AGENTES QA
│   ├── QA_LEAD_Assistant.agent.md        (PADRE - Orquestador global)
│   ├── PM_QA_Assistant.agent.md          (Pichincha Miles - Kepler)
│   ├── BGR_QA_Assistant.agent.md         (BGR Miles - Kepler)
│   └── CME_QA_Assistant.agent.md         (Club Miles Ecuador - Kepler)
│   
│   [Nota: Futuros agentes por célula se agregarán en esta carpeta]
│
├── shared/                                ← REGLAS COMPARTIDAS
│   ├── SHARED_QA_RULES.md                (Universal - Todos los modelos)
│   ├── AGENT_CONTEXT_VALIDATION.md        (Validación de contexto de agentes)
│   │
│   └── Kepler/                           ← Célula Kepler
│       ├── PM_COMMON_RULES.md            (Reglas comunes Pichincha Miles)
│       ├── BGR_COMMON_RULES.md           (Reglas comunes BGR Miles)
│       └── CME_COMMON_RULES.md           (Reglas comunes Club Miles Ecuador)
│
├── products/                              ← FLUJOS E2E POR PRODUCTO Y MODELO DE NEGOCIO
│   ├── B2B2C/                            ← Modelo B2B2C (PPM)
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
│   │           └── README.md             (Pendiente documentar productos)
│   │
│   ├── B2B/                              ← Modelo B2B
│   │   ├── PPM/
│   │   │   └── CORPORATIVO USD/
│   │   │       └── README.md
│   │   └── ULTRA/
│   │       ├── CONSOLIDACION COP/
│   │       │   └── README.md
│   │       └── CONSOLIDACION USD/
│   │           └── README.md
│   │
│   └── B2C/                              ← Modelo B2C
│       ├── ULTRA/
│       │   ├── VACACIONAL COP/
│       │   │   └── README.md
│       │   └── VACACIONAL USD/
│       │       └── README.md
│       └── AVASA/
│           └── VIVA AEROBUS/
│               └── README.md
│
├── imagenes/                              ← Recursos visuales (alias)
└── images/                                ← Recursos visuales
    └── [imágenes del proyecto]
```

---

## 🏢 Células y Modelos

### **📦 Célula KEPLER** (5 modelos configurados)

| Modelo | Agente | Prefijo | País | Estado |
|--------|--------|---------|------|--------|
| **Pichincha Miles** | Kepler/PM_QA_Assistant | [PM] | Ecuador | ✅ Activo |
| **BGR Miles** | Kepler/BGR_QA_Assistant | [BGR] | Ecuador | ✅ Activo |
| **Correos Millas Ecuador** | Kepler/CME_QA_Assistant | [CME] | Ecuador | ✅ Activo |
| **Correos Millas Panamá** | Kepler/CMP_QA_Assistant | [CMP] | Panamá | ⏳ Pendiente |
| **Promerica Rewards** | Kepler/PROM_QA_Assistant | [PROM] | - | ⏳ Pendiente |

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

#### 🎯 **Agente Estratégico (Liderazgo)**

| Agente | Archivo | Cuándo usar |
|--------|---------|-------------|
| **QA Lead Assistant** | [QA_LEAD_Assistant.agent.md](agents/QA_LEAD_Assistant.agent.md) | Visión global, orquestación multi-célula, comparaciones estratégicas, análisis cross-portal |

#### 🔷 **Célula KEPLER - Agentes Especializados**

| Agente | Archivo | Portal/Modelo | Cuándo usar |
|--------|---------|---------------|-------------|
| **PM QA Assistant** | [PM_QA_Assistant.agent.md](agents/PM_QA_Assistant.agent.md) | Pichincha Miles (Ecuador) | Crear casos de prueba específicos para PM |
| **BGR QA Assistant** | [BGR_QA_Assistant.agent.md](agents/BGR_QA_Assistant.agent.md) | BGR Miles (Ecuador) | Crear casos de prueba específicos para BGR |
| **CME QA Assistant** | [CME_QA_Assistant.agent.md](agents/CME_QA_Assistant.agent.md) | Club Miles Ecuador | Crear casos de prueba específicos para CME |
| _CMP, Promerica_ | _Pendiente configurar_ | Club Millas Perú, Promerica | Agentes por implementar |

#### 🎯 **Célula PIXEL - Agentes Especializados**

| Estado | Mensaje |
|--------|---------|
| 📦 Sin modelos configurados | Ver [Pixel/README.md](agents/Pixel/README.md) para agregar modelos |

#### 🚀 **Célula ROCKET - Agentes Especializados**

| Estado | Mensaje |
|--------|---------|
| 📦 Sin modelos configurados | Ver [Rocket/README.md](agents/Rocket/README.md) para agregar modelos |

#### 🤖 **Célula SKYNET - Agentes Especializados**

| Estado | Mensaje |
|--------|---------|
| 📦 Sin modelos configurados | Ver [Skynet/README.md](agents/Skynet/README.md) para agregar modelos |

#### 🔄 **Célula TRANSVERSALES - Agentes Especializados**

| Estado | Mensaje |
|--------|---------|
| 📦 Sin modelos configurados | Ver [Transversales/README.md](agents/Transversales/README.md) para agregar modelos |

### 2. Arquitectura Multi-Célula

```
                                QA_LEAD_Assistant
                               (Orquestador Global)
                            │
        ┌───────────────────┬───────────┼──────────┬────────────┬──────────┐
        │                   │           │          │            │          │
    KEPLER                PIXEL       ROCKET    SKYNET      TRANSVERSALES  |
        │                   │           │          │            │          |
  ┌─────┴─────────|         │           │          │            │          |
  │  │   │   │    |         │           │          │            │          │
 PM BGR CME CMP PMRICA      │           │          │            │          |
                       [modelos]    [modelos]   [modelos]     [modelos]
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
# Para PM (Pichincha Miles)
Copy-Item templates/product-template.md products/B2B2C/PPM/PM/PM_NUEVO_PRODUCTO.md

# Para BGR (BGR Miles)
Copy-Item templates/product-template.md products/B2B2C/PPM/BGR/BGR_NUEVO_PRODUCTO.md

# Para CME (Club Miles Ecuador)
Copy-Item templates/product-template.md products/B2B2C/PPM/CME/CME_NUEVO_PRODUCTO.md
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
🎨 [PM_NUEVO_PRODUCTO.md](../products/B2B2C/PPM/PM/PM_NUEVO_PRODUCTO.md) - Flujo E2E completo de Nuevo Producto
```

### Paso 5: Actualizar COMMON_RULES

Agregar a la tabla de proveedores en `shared/Kepler/PM_COMMON_RULES.md`:

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

# Crear reglas comunes (ajustar ruta según célula)
Copy-Item templates/portal-template.md shared/[CELULA]/NUEVO_PORTAL_COMMON_RULES.md

# Crear carpeta de productos (ajustar modelo de negocio: B2B2C, B2B, B2C)
New-Item -ItemType Directory -Path products/[MODELO_NEGOCIO]/[EMPRESA]/NUEVO_PORTAL/
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
# Ajustar ruta según modelo de negocio y empresa
Copy-Item templates/product-template.md products/[MODELO_NEGOCIO]/[EMPRESA]/NUEVO_PORTAL/NUEVO_PORTAL_VUELOS.md
Copy-Item templates/product-template.md products/[MODELO_NEGOCIO]/[EMPRESA]/NUEVO_PORTAL/NUEVO_PORTAL_HOTELES.md
# ... etc
```

### Paso 5: Actualizar documentación

- Agregar portal a este README.md
- Actualizar CHANGELOG.md
- Documentar diferencias en ARCHITECTURE.md

---

## 🔧 Mantenimiento

### Actualizar flujo de producto existente

1. Abrir archivo en `products/B2B2C/PPM/PM/PM_PRODUCTO.md` o `products/B2B2C/PPM/BGR/BGR_PRODUCTO.md`
2. Editar sección correspondiente
3. Actualizar metadata `ultima_actualizacion`
4. Documentar cambio en CHANGELOG.md

### Cambiar modelo de negocio

1. Editar `shared/Kepler/PM_COMMON_RULES.md` o `shared/Kepler/BGR_COMMON_RULES.md`
2. Revisar impacto en productos afectados
3. Actualizar productos si es necesario
4. Versionar cambio en CHANGELOG.md

### Agregar nueva validación

**Si es común a todos los productos:**
- Agregar a `shared/SHARED_QA_RULES.md` (aplica a PM y BGR)

**Si es específica de un portal:**
- Agregar a `shared/Kepler/PM_COMMON_RULES.md` o `shared/Kepler/BGR_COMMON_RULES.md`

**Si es específica de un producto:**
- Agregar a `products/B2B2C/PPM/[PORTAL]/[PORTAL]_PRODUCTO.md`

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

- **Agentes activos:** 3 (PM, BGR, CME) + 1 Lead (QA_LEAD)
- **Células configuradas:** 1 (Kepler)
- **Modelos de negocio:** 3 (B2B2C, B2B, B2C)
- **Productos por portal Kepler:** 5 (Vuelos, Hoteles, Autos, Actividades, Disney)
- **Total archivos de flujos PM:** 5
- **Total archivos de flujos BGR:** 5
- **Total archivos de flujos CME:** 5
- **Reglas compartidas:** 4 (SHARED_QA, PM_COMMON, BGR_COMMON, CME_COMMON)
- **Líneas de documentación:** ~8,000+
- **Optimización:** 50% reducción vs arquitectura monolítica

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
