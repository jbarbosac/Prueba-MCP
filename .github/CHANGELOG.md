# Changelog

Todos los cambios notables en este proyecto serán documentados en este archivo.

El formato está basado en [Keep a Changelog](https://keepachangelog.com/es-ES/1.0.0/),
y este proyecto adhiere a [Semantic Versioning](https://semver.org/lang/es/).

---

## [1.0.0] - 2026-01-05

### 🎉 Added - Implementación inicial

#### Arquitectura Base
- ✅ Sistema modular de agentes QA para PM y BGR
- ✅ Separación clara: `agents/`, `shared/`, `products/`, `imagenes/`
- ✅ 2 agentes especializados: `PM_QA_Assistant` y `BGR_QA_Assistant`
- ✅ 3 archivos de reglas compartidas: SHARED_QA_RULES, PM_COMMON_RULES, BGR_COMMON_RULES

#### Productos Implementados
- ✅ **PM (Pichincha Miles):**
  - PM_VUELOS.md (26 pasos E2E + 11 imágenes de referencia)
  - PM_HOTELES.md (26 pasos E2E)
  - PM_AUTOS.md (23 pasos E2E)
  - PM_ACTIVIDADES.md (24 pasos E2E)
  - PM_DISNEY.md (22 pasos E2E)

- ✅ **BGR (BGR Miles):**
  - BGR_VUELOS.md (29 pasos E2E)
  - BGR_HOTELES.md (30 pasos E2E)
  - BGR_AUTOS.md (30 pasos E2E con Drop-off fee)
  - BGR_ACTIVIDADES.md (27 pasos E2E)
  - BGR_DISNEY.md (26 pasos E2E)

#### Funcionalidades Core
- ✅ Generación automática de test cases en Azure DevOps
- ✅ Creación secuencial UNO POR UNO (evita cancelación del sistema)
- ✅ Formato HTML para campos Descriptions y Considerations
- ✅ Validación de campos obligatorios (planId, suiteId)
- ✅ Trazabilidad con User Stories (HU)
- ✅ 6 reglas obligatorias ISTQB aplicadas
- ✅ Inicio desde login en todos los flujos

#### Documentación
- ✅ README.md principal con Quick Start
- ✅ CHANGELOG.md para control de versiones
- ✅ Templates para agregar productos y portales
- ✅ Docs técnicos (GLOSSARY, ARCHITECTURE, CONTRIBUTING)
- ✅ Scripts de validación básica

### 🔧 Changed - Optimizaciones

#### Reducción de Duplicación
- 🔄 Eliminado 45% de contenido duplicado (253 líneas)
- 🔄 PM_COMMON_RULES: 214 → 95 líneas (-56%)
- 🔄 BGR_COMMON_RULES: 353 → 219 líneas (-38%)
- 🔄 Consolidado reglas universales en SHARED_QA_RULES.md

#### Reorganización de Estructura
- 🔄 Movido `agents/shared/` → `.github/shared/`
- 🔄 Movido `agents/products/` → `.github/products/`
- 🔄 Movido `agents/SHARED_QA_RULES.md` → `.github/shared/SHARED_QA_RULES.md`
- 🔄 Actualizado todas las referencias de rutas en agentes

#### Optimización de Tokens
- 🔄 Arquitectura monolítica: ~15,000 tokens/caso
- 🔄 Arquitectura modular: ~7,500 tokens/caso (50% reducción)
- 🔄 Carga bajo demanda: solo archivos necesarios por producto

### 🐛 Fixed - Correcciones

- ✅ Eliminadas reglas duplicadas en COMMON_RULES
- ✅ Corregida dispersión SABRE EDIFACT (solo en PM, no en BGR)
- ✅ Eliminados archivos obsoletos:
  - `/chatmodes/` (carpeta vacía)
  - `/Prompts/` (prompts obsoletos)
  - `copilot-instructions.md` (archivo vacío)
  - `Create-E2ETestCases-Asistencias.ps1` (script no usado)
  - `Create-E2ETestCases.ps1` (script no usado)

### 📋 Technical Details

#### Proveedores por Portal

**PM (Pichincha Miles):**
- Vuelos: AGGREGATOR NETACTICA, AGGREGATOR SABRE, SABRE EDIFACT (con dispersión)
- Autos: Sabre → Hertz, Dollar, Thrifty
- Hoteles: HotelBeds
- Actividades: HotelBeds
- Disney: DerbySoft

**BGR (BGR Miles):**
- Vuelos: AGGREGATOR NETACTICA, AGGREGATOR SABRE, SABRE EDIFACT (sin dispersión)
- Autos: Sabre → Hertz, Dollar, Thrifty
- Hoteles: HotelBeds
- Actividades: HotelBeds
- Disney: OffLine

#### Tecnologías por Producto
- Vuelos: Angular (TypeScript/JavaScript)
- Hoteles: Angular (TypeScript/JavaScript)
- Autos: Meteor (JavaScript/MongoDB)
- Actividades: Angular (TypeScript/JavaScript)
- Disney: React (TypeScript/JavaScript)

#### Modelos de Pago

**PM:**
- Vuelos: 100% Millas + Fee (tarjeta en lightbox)
- Otros: 100% Millas (sin fee, sin tarjeta)
- Emisión: Automática siempre

**BGR:**
- Opción 1: Solo Millas (100%) → Emisión AUTOMÁTICA
- Opción 2: Millas + Plata (slider) → Emisión MANUAL
- Opción 3: Solo Plata → ❌ NO PERMITIDO
- Slider mínimo: Vuelos 2875 millas, Otros 20%

### 📊 Estadísticas Finales

| Métrica | Valor |
|---------|-------|
| Agentes | 2 |
| Productos totales | 10 (5 PM + 5 BGR) |
| Archivos de reglas | 3 |
| Líneas totales | ~2,500 |
| Reducción duplicación | 45% |
| Optimización tokens | 50% |
| Imágenes de flujo PM | 11 (Vuelos) |

---

## [Unreleased] - Futuras mejoras

### Planificado
- [ ] Agregar portal Perú (si aplica)
- [ ] Agregar portal Colombia (si aplica)
- [ ] Implementar validación automática de links entre archivos
- [ ] Generar diagramas de flujo automáticos (Mermaid)
- [ ] Crear dashboard de métricas de casos generados

### Considerado
- [ ] Integración con GitHub Actions para CI/CD
- [ ] Versionado automático de agentes
- [ ] Exportación de casos a formato Excel
- [ ] Generación de reportes de coverage

---

## Notas de Versión

### Formato de Versiones
- **MAJOR:** Cambios incompatibles en la API/estructura
- **MINOR:** Nueva funcionalidad compatible con versiones anteriores
- **PATCH:** Corrección de bugs compatible con versiones anteriores

### Tipos de Cambios
- `Added` - Nueva funcionalidad
- `Changed` - Cambios en funcionalidad existente
- `Deprecated` - Funcionalidad que será removida
- `Removed` - Funcionalidad removida
- `Fixed` - Corrección de bugs
- `Security` - Correcciones de seguridad

---

**Mantenido por:** QA Team Ultragroup  
**Última actualización:** 2026-01-05
