# 🔐 Arquitectura de Seguridad de Agentes QA

## 📋 Resumen Ejecutivo

Se ha implementado un **sistema de validación de contexto** para garantizar que cada agente QA solo ejecute acciones dentro de su dominio asignado, evitando errores de contexto y asegurando la integridad de los datos en Azure DevOps.

---

## 🎯 Problema Resuelto

**Antes:**
- ❌ Riesgo de crear casos con prefijo incorrecto
- ❌ Posibilidad de mezclar contextos entre portales
- ❌ Falta de validación antes de ejecutar acciones
- ❌ Confusión sobre qué agente usar

**Después:**
- ✅ Validación obligatoria antes de cada acción
- ✅ Bloqueo automático si el contexto es incorrecto
- ✅ Redirección clara al agente correcto
- ✅ 100% de trazabilidad y consistencia

---

## 🏗️ Arquitectura Implementada

### 1️⃣ Documento Central de Validación

**Archivo:** [AGENT_CONTEXT_VALIDATION.md](../shared/AGENT_CONTEXT_VALIDATION.md)

**Contenido:**
- 📊 Matriz de agentes y dominios
- 🔍 Reglas de validación por tipo de agente
- 🚨 Ejemplos de bloqueo y redirección
- 🎯 Keywords de detección por portal
- 📝 Plantillas de respuesta

### 2️⃣ Validación en Agentes Especializados

**Agentes afectados:**
- `PM_QA_Assistant` → Pichincha Miles
- `BGR_QA_Assistant` → BGR Miles
- `CME_QA_Assistant` → Correos Millas Ecuador
- `CMP_QA_Assistant` → Club Millas Perú (futuro)
- `PROM_QA_Assistant` → Promerica Rewards (futuro)

**Validaciones implementadas:**
```markdown
🔍 VALIDACIÓN AUTOMÁTICA:
1. Detectar keywords del portal
2. Validar URLs mencionadas
3. Verificar prefijo requerido
4. Bloquear si no coincide el contexto
5. Redirigir al agente correcto
```

### 3️⃣ Validación en Agente Estratégico

**Agente:** `QA_LEAD_Assistant`

**Validaciones especiales:**
```markdown
🔍 VALIDACIÓN DE TIPO DE REQUEST:
A) Consulta estratégica → Responder directamente
B) Creación UN portal → Delegar al especialista
C) Creación MÚLTIPLES → Orquestar agentes
D) Pregunta técnica → Redirigir al especialista

🚫 PROHIBIDO:
- Ejecutar create_test_case directamente
- Usar MCP tools sin delegar
```

---

## 🔒 Reglas de Seguridad

### Matriz de Permisos

| Agente | Crear Casos | Portal | Prefijo | Delegar | Orquestar |
|--------|-------------|--------|---------|---------|-----------|
| **PM_QA_Assistant** | ✅ Solo PM | pichinchamiles | [PM] | ❌ | ❌ |
| **BGR_QA_Assistant** | ✅ Solo BGR | bgrmiles | [BGR] | ❌ | ❌ |
| **CME_QA_Assistant** | ✅ Solo CME | correosmillas | [CME] | ❌ | ❌ |
| **CMP_QA_Assistant** | ✅ Solo CMP | [Pendiente] | [CMP] | ❌ | ❌ |
| **PROM_QA_Assistant** | ✅ Solo PROM | [Pendiente] | [PROM] | ❌ | ❌ |
| **QA_LEAD_Assistant** | ❌ No directo | Todos | N/A | ✅ | ✅ |

### Keywords de Detección

**Pichincha Miles (PM):**
```
Keywords: "Pichincha Miles", "PM", "pichinchamiles", "100% millas", "automática", "fee"
URL: pichinchamiles-ec.preprodppm.com
Prefijo: [PM]
```

**BGR Miles (BGR):**
```
Keywords: "BGR", "BGR Miles", "bgrmiles", "slider", "millas + plata", "mixto", "semiautomático", "manual"
URL: bgrmiles-ec.preprodppm.com
Prefijo: [BGR]
```

**Correos Millas Ecuador (CME):**
```
Keywords: "CME", "Correos Millas", "correosmillas", "Ecuador" + "100% millas"
URL: correosmillas-ec.preprodppm.com
Prefijo: [CME]
```

---

## 🚦 Flujo de Validación

```
┌─────────────────────────────────┐
│   USUARIO HACE REQUEST         │
└──────────┬──────────────────────┘
           │
           ▼
┌─────────────────────────────────┐
│ 1. IDENTIFICAR AGENTE ACTIVO   │
└──────────┬──────────────────────┘
           │
           ▼
┌─────────────────────────────────┐
│ 2. ANALIZAR REQUEST            │
│    - Keywords                   │
│    - URLs                       │
│    - Prefijos                   │
└──────────┬──────────────────────┘
           │
           ▼
┌─────────────────────────────────┐
│ 3. VALIDAR CONTEXTO            │
│    ¿Coincide con dominio?       │
└──────────┬──────────────────────┘
           │
           ├─── ✅ SÍ ────────────┐
           │                       │
           │                       ▼
           │            ┌─────────────────────┐
           │            │ ✅ EJECUTAR ACCIÓN │
           │            └─────────────────────┘
           │
           └─── ❌ NO ────────────┐
                                  │
                                  ▼
                       ┌─────────────────────┐
                       │ ❌ BLOQUEAR        │
                       │ ✅ REDIRIGIR       │
                       └─────────────────────┘
```

---

## 📝 Ejemplos de Validación

### ✅ Caso 1: Request Correcto

```
👤 Usuario: "Crea un caso de vuelos ida y vuelta para PM"
🤖 Agente Activo: PM_QA_Assistant

🔍 Validación:
- Keyword detectado: "PM" ✅
- Agente correcto: PM_QA_Assistant ✅
- Dominio: Pichincha Miles ✅
- Prefijo: [PM] ✅

✅ RESULTADO: Proceder con la creación del caso
```

### ❌ Caso 2: Request Incorrecto (Bloqueado)

```
👤 Usuario: "Crea un caso de vuelos con slider para BGR"
🤖 Agente Activo: PM_QA_Assistant

🔍 Validación:
- Keywords detectados: "slider", "BGR" ❌
- Agente activo: PM_QA_Assistant
- Request para: BGR_QA_Assistant
- ¿Coinciden? ❌ NO

❌ ACCIÓN BLOQUEADA

📝 Respuesta del agente:
"❌ ACCIÓN BLOQUEADA - Contexto Incorrecto

El request solicitado es para BGR Miles (modelo Millas + Plata con slider) 
pero el agente activo es PM_QA_Assistant que solo trabaja con Pichincha Miles 
(modelo 100% Millas).

✅ SOLUCIÓN:
Cambia al agente: BGR_QA_Assistant
📍 Ubicación: .github/agents/BGR_QA_Assistant.agent.md"
```

### ✅ Caso 3: Delegación QA_LEAD

```
👤 Usuario: "Crea un caso de hoteles para BGR"
🤖 Agente Activo: QA_LEAD_Assistant

🔍 Validación:
- Tipo de request: Creación caso UN portal ✅
- Portal objetivo: BGR ✅
- Agente correcto: BGR_QA_Assistant ✅
- Capacidad de delegar: ✅ SÍ

✅ RESULTADO: Delegar a BGR_QA_Assistant

📝 Respuesta:
"Voy a delegar este request a BGR_QA_Assistant que es el especialista 
en BGR Miles. ¿Confirmas que tienes planId y suiteId?"

[Después de confirmación → Delegar con contexto completo]
```

### ✅ Caso 4: Orquestación Multi-Portal

```
👤 Usuario: "Crea casos de autos para todos los modelos de Kepler"
🤖 Agente Activo: QA_LEAD_Assistant

🔍 Validación:
- Tipo de request: Creación MÚLTIPLES portales ✅
- Célula: Kepler ✅
- Modelos: PM, BGR, CME, CMP, PROM ✅
- Capacidad de orquestar: ✅ SÍ

✅ RESULTADO: Orquestar 5 agentes

📝 Flujo:
1. Confirmar planId/suiteId para cada modelo
2. Delegar secuencialmente:
   - Kepler/PM_QA_Assistant → [PM] Autos
   - Kepler/BGR_QA_Assistant → [BGR] Autos
   - Kepler/CME_QA_Assistant → [CME] Autos
   - Kepler/CMP_QA_Assistant → [CMP] Autos
   - Kepler/PROM_QA_Assistant → [PROM] Autos
3. Consolidar resultados
4. Reportar tabla con 5 casos creados
```

---

## 📊 Beneficios del Sistema

### Para el Usuario
- ✅ **Claridad:** Siempre sabe qué agente usar
- ✅ **Seguridad:** No puede crear casos en contexto incorrecto
- ✅ **Guía:** Recibe instrucciones precisas de redirección
- ✅ **Eficiencia:** Un solo intento para llegar al agente correcto

### Para el Sistema
- ✅ **Integridad:** 100% de casos con prefijo correcto
- ✅ **Trazabilidad:** Cada caso pertenece al portal correcto
- ✅ **Mantenibilidad:** Lógica centralizada en un documento
- ✅ **Escalabilidad:** Fácil agregar nuevos agentes

### Para QA
- ✅ **Confianza:** Los casos siempre están en el contexto correcto
- ✅ **Orden:** Azure DevOps organizado por portal
- ✅ **Métricas:** Estadísticas precisas por portal
- ✅ **Calidad:** Cero errores de prefijo

---

## 🔧 Mantenimiento

### Agregar un Nuevo Agente

1. **Crear archivo del agente:**
   ```
   .github/agents/NUEVO_AGENTE.agent.md
   ```

2. **Incluir sección de validación:**
   ```markdown
   🔐 VALIDACIÓN DE CONTEXTO OBLIGATORIA
   
   Referencia: [AGENT_CONTEXT_VALIDATION.md](../shared/AGENT_CONTEXT_VALIDATION.md)
   
   1. ✅ Validar keywords específicos
   2. ❌ Bloquear otros contextos
   3. 🚫 Nunca usar prefijo de otro portal
   ```

3. **Actualizar matriz en AGENT_CONTEXT_VALIDATION.md:**
   ```markdown
   | NUEVO_AGENTE | [Dominio] | [URL] | [Prefijo] | ✅ SÍ |
   ```

4. **Actualizar QA_LEAD_Assistant:**
   ```markdown
   - NUEVO_AGENTE disponible para delegación
   ```

### Modificar Validaciones

**Archivo central:** [AGENT_CONTEXT_VALIDATION.md](../shared/AGENT_CONTEXT_VALIDATION.md)

**Pasos:**
1. Actualizar keywords de detección
2. Modificar plantillas de respuesta
3. Actualizar matriz de permisos
4. Verificar en todos los agentes

---

## 📈 Métricas de Éxito

**Indicadores:**
- ✅ **100%** de casos con prefijo correcto
- ✅ **0%** de casos en contexto incorrecto
- ✅ **100%** de redirects exitosos
- ✅ **1 intento** promedio para encontrar agente correcto

**Auditoría:**
- Revisar casos creados por prefijo
- Validar trazabilidad por portal
- Verificar logs de bloqueos
- Analizar redirects comunes

---

## 🎓 Capacitación de Usuarios

### ¿Qué agente usar?

**Regla simple:**
1. ¿Qué portal estás probando?
   - **Pichincha Miles** → `PM_QA_Assistant`
   - **BGR Miles** → `BGR_QA_Assistant`
   - **Correos Millas Ecuador** → `CME_QA_Assistant`
   - **Club Millas Perú** → `CMP_QA_Assistant`
   - **Promerica Rewards** → `PROM_QA_Assistant`
   - **Visión global / Comparativas** → `QA_LEAD_Assistant`

2. ¿Necesitas crear casos para MÚLTIPLES portales?
   - Usa `QA_LEAD_Assistant` (él orquesta)

### Identificar Portales por URL

| URL | Agente Correcto |
|-----|-----------------|
| `pichinchamiles-ec.preprodppm.com` | PM_QA_Assistant |
| `bgrmiles-ec.preprodppm.com` | BGR_QA_Assistant |
| `correosmillas-ec.preprodppm.com` | CME_QA_Assistant |

### Identificar por Modelo de Negocio

| Característica | Agente Correcto |
|----------------|-----------------|
| 100% Millas + Fee vuelos | PM_QA_Assistant |
| Slider Millas + Plata | BGR_QA_Assistant |
| 100% Millas Ecuador (Correos) | CME_QA_Assistant |

---

## 🔗 Referencias

- 📋 [AGENT_CONTEXT_VALIDATION.md](../shared/AGENT_CONTEXT_VALIDATION.md) - Documento maestro de validación
- 🎯 [QA_LEAD_Assistant.agent.md](../agents/QA_LEAD_Assistant.agent.md) - Agente estratégico
- 🛫 [PM_QA_Assistant.agent.md](../agents/PM_QA_Assistant.agent.md) - Agente Pichincha Miles
- 🎰 [BGR_QA_Assistant.agent.md](../agents/BGR_QA_Assistant.agent.md) - Agente BGR Miles
- 📮 [CME_QA_Assistant.agent.md](../agents/CME_QA_Assistant.agent.md) - Agente Correos Millas

---

**Última actualización:** 2026-01-08  
**Versión:** 1.0  
**Estado:** ✅ Implementado en todos los agentes  
**Autor:** QA Architecture Team
