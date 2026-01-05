# 🤖 Sistema de Agentes QA para Generación Automática de Test Cases

> Sistema modular de generación de casos de prueba E2E para portales de redención de millas PM (Pichincha Miles) y BGR (BGR Miles) con integración directa a Azure DevOps.

---

## 📋 Tabla de Contenidos

- [Descripción General](#descripción-general)
- [Estructura del Proyecto](#estructura-del-proyecto)
- [Portales Soportados](#portales-soportados)
- [Quick Start](#quick-start)
- [Agregar Nuevo Producto](#agregar-nuevo-producto)
- [Agregar Nuevo Portal](#agregar-nuevo-portal)
- [Mantenimiento](#mantenimiento)
- [Arquitectura](#arquitectura)

---

## 🎯 Descripción General

Este sistema proporciona agentes QA especializados que:
- ✅ Generan casos de prueba E2E completos según ISTQB
- ✅ Crean test cases directamente en Azure DevOps Test Plans **mediante herramientas MCP**
- ✅ Mantienen trazabilidad con User Stories (HU)
- ✅ Aplican validaciones específicas por portal y producto
- ✅ Optimizan uso de tokens mediante arquitectura modular

> **IMPORTANTE:** Todas las operaciones de Azure DevOps (crear casos, actualizar campos, agregar a suites, obtener HU) se ejecutan **exclusivamente mediante herramientas MCP** (Model Context Protocol). No se requiere intervención manual.

---

## 📁 Estructura del Proyecto

```
.github/
├── README.md                      ← Este archivo
├── CHANGELOG.md                   ← Historial de cambios
│
├── docs/                          ← Documentación técnica
│   ├── GLOSSARY.md               (Glosario de términos)
│   ├── ARCHITECTURE.md           (Decisiones arquitecturales)
│   └── CONTRIBUTING.md           (Guía de contribución)
│
├── templates/                     ← Plantillas reutilizables
│   ├── product-template.md       (Para agregar productos)
│   └── portal-template.md        (Para agregar portales)
│
├── agents/                        ← Agentes QA (*.agent.md)
│   ├── PM_QA_Assistant.agent.md  (Agente Pichincha Miles)
│   └── BGR_QA_Assistant.agent.md (Agente BGR Miles)
│
├── shared/                        ← Reglas compartidas
│   ├── SHARED_QA_RULES.md        (Fundamentos ISTQB + Azure DevOps)
│   ├── PM_COMMON_RULES.md        (Reglas comunes PM)
│   └── BGR_COMMON_RULES.md       (Reglas comunes BGR)
│
├── products/                      ← Flujos E2E por producto
│   ├── PM_VUELOS.md              (Pichincha Miles - Vuelos)
│   ├── PM_HOTELES.md             (Pichincha Miles - Hoteles)
│   ├── PM_AUTOS.md               (Pichincha Miles - Autos)
│   ├── PM_ACTIVIDADES.md         (Pichincha Miles - Actividades)
│   ├── PM_DISNEY.md              (Pichincha Miles - Disney)
│   ├── BGR_VUELOS.md             (BGR Miles - Vuelos)
│   ├── BGR_HOTELES.md            (BGR Miles - Hoteles)
│   ├── BGR_AUTOS.md              (BGR Miles - Autos)
│   ├── BGR_ACTIVIDADES.md        (BGR Miles - Actividades)
│   └── BGR_DISNEY.md             (BGR Miles - Disney)
│
└── imagenes/                      ← Recursos visuales
    ├── PM/                        (Pantallas Pichincha Miles)
    │   └── vuelos/               (11 capturas del flujo)
    └── BGR/                       (Pantallas BGR Miles)
```

---

## 🌐 Portales Soportados

### **Pichincha Miles (PM)**
- **URL:** https://pichinchamiles-ec.preprodppm.com/
- **País:** Ecuador
- **Prefijo:** [PM]
- **Modelo:** 100% Millas + Fee (solo vuelos con tarjeta)
- **Emisión:** Automática
- **Agente:** `PM_QA_Assistant.agent.md`

### **BGR Miles (BGR)**
- **URL:** https://bgrmiles-ec.preprodppm.com/
- **País:** Ecuador
- **Prefijo:** [BGR]
- **Modelo:** Slider (Solo Millas o Millas + Plata)
- **Emisión:** Automática (100% millas) / Manual (mixto)
- **Agente:** `BGR_QA_Assistant.agent.md`

---

## 🚀 Quick Start

### 1. Seleccionar el agente correcto

| Portal | Agente | Cuándo usar |
|--------|--------|-------------|
| **Pichincha Miles** | `PM_QA_Assistant` | URL pichinchamiles-ec.preprodppm.com, 100% millas + fee |
| **BGR Miles** | `BGR_QA_Assistant` | URL bgrmiles-ec.preprodppm.com, slider millas/plata |

### 2. Preparar información

Antes de generar casos, ten listo:
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

### 3. Solicitar generación de casos

**Ejemplo para PM Vuelos:**
```
"Genera un caso de prueba para PM Vuelos ida y vuelta SABRE con 1 adulto clase económica"
```

**Ejemplo para BGR Hoteles:**
```
"Genera un caso para BGR Hoteles 3 noches HotelBeds con pago Solo Millas automático"
```

### 4. Revisar y aprobar

El agente presentará una tabla con los casos generados. Revisa y confirma:
```
¿Procedo a crear los {N} casos en Azure DevOps en planId=121536 suiteId=121850? (sí/no/ajusta)
```

### 5. Validación automática

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

**Última actualización:** 2026-01-05  
**Versión:** 1.0.0  
**Mantenido por:** QA Team Ultragroup
