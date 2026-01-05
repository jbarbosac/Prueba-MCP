# 🏗️ Decisiones Arquitecturales (ADR)

> Architecture Decision Records - Documentación de decisiones clave en el diseño del sistema.

---

## ADR-001: Arquitectura modular basada en archivos Markdown

**Fecha:** 2026-01-05  
**Estado:** ✅ Aceptado  
**Contexto:** Se requiere un sistema escalable para generar test cases E2E de múltiples portales (PM, BGR) y productos (Vuelos, Hoteles, Autos, Actividades, Disney).

### Decisión
Implementar arquitectura modular basada en archivos Markdown (.md) con separación clara de responsabilidades:
- `agents/` - Agentes orchestradores
- `shared/` - Reglas comunes
- `products/` - Flujos E2E específicos
- `imagenes/` - Recursos visuales

### Razones
✅ **Simplicidad:** Archivos planos, fáciles de editar y versionar  
✅ **Escalabilidad:** Agregar portales/productos sin modificar código existente  
✅ **Mantenibilidad:** Cambios localizados en archivos específicos  
✅ **Sin dependencias:** No requiere base de datos, API o infraestructura compleja  
✅ **Rendimiento:** Carga bajo demanda reduce consumo de tokens 50%  
✅ **Trazabilidad:** Git rastrea todos los cambios automáticamente  

### Consecuencias
✅ Fácil agregar nuevos productos (copiar template)  
✅ Fácil agregar nuevos portales (duplicar estructura)  
⚠️ Requiere disciplina para mantener consistencia de formato  
⚠️ Links entre archivos deben actualizarse manualmente  

### Alternativas consideradas
- ❌ Base de datos relacional: Sobrecompleja para este caso de uso
- ❌ API REST: Requiere infraestructura adicional innecesaria
- ❌ JSON/YAML: Menos legible para humanos que Markdown

---

## ADR-002: Separación PM/BGR en agentes independientes

**Fecha:** 2026-01-05  
**Estado:** ✅ Aceptado  
**Contexto:** PM y BGR tienen modelos de negocio significativamente diferentes que pueden causar confusión si se manejan en un solo agente.

### Decisión
Crear dos agentes especializados e independientes:
- `PM_QA_Assistant.agent.md` - Solo Pichincha Miles
- `BGR_QA_Assistant.agent.md` - Solo BGR Miles

Cada agente tiene:
- Identificación clara de su alcance
- Referencias a su propio COMMON_RULES
- Validación de contexto (rechaza si usuario pide el portal equivocado)

### Razones
✅ **Claridad:** Usuario sabe exactamente qué agente usar  
✅ **Especialización:** Cada agente domina su portal  
✅ **Prevención de errores:** Validación automática de alcance  
✅ **Optimización tokens:** Solo carga reglas del portal relevante  
✅ **Mantenibilidad:** Cambios en PM no afectan BGR y viceversa  

### Consecuencias
✅ Usuario no puede confundir lógica PM con BGR  
✅ Casos de prueba más precisos y relevantes  
✅ Fácil agregar nuevo portal (clonar agente existente)  
⚠️ Duplicación intencional de reglas ISTQB universales  

### Alternativas consideradas
- ❌ Agente único con switch PM/BGR: Complejo, propenso a errores
- ❌ Parámetro de configuración: Usuario debe recordar configurar antes de cada uso

---

## ADR-003: Duplicación intencional de reglas obligatorias en agentes

**Fecha:** 2026-01-05  
**Estado:** ✅ Aceptado  
**Contexto:** Las 6 reglas obligatorias ISTQB están en SHARED_QA_RULES.md pero también aparecen en ambos agentes.

### Decisión
**CONSERVAR** la duplicación de las 6 reglas obligatorias en archivos de agentes.

### Razones
✅ **Visibilidad inmediata:** Agente tiene reglas críticas sin cargar archivos externos  
✅ **Reducción latencia:** No requiere lectura adicional de SHARED_QA_RULES  
✅ **Autonomía:** Agente funciona sin dependencias en caso de error de carga  
✅ **Priorización:** Reglas críticas siempre visibles en contexto principal  
✅ **Experiencia usuario:** Más rápido mostrar reglas cuando se solicitan  

### Consecuencias
✅ Agentes son autocontenidos y resilientes  
✅ Rendimiento óptimo (menos lecturas de archivos)  
⚠️ Si cambian reglas ISTQB, actualizar 3 archivos (SHARED + 2 agentes)  
⚠️ ~100 líneas duplicadas intencionalmente  

### Alternativas consideradas
- ❌ Eliminar de agentes: Requiere carga adicional de SHARED, aumenta latencia
- ❌ Solo en SHARED: Agentes pierden autonomía

---

## ADR-004: Modelo de pago en cada archivo de producto

**Fecha:** 2026-01-05  
**Estado:** ✅ Aceptado  
**Contexto:** Información de "Modelo de pago" aparece en COMMON_RULES y también en cada archivo de producto individual.

### Decisión
**CONSERVAR** la línea "Modelo de pago" en cada archivo de producto.

**Ejemplo:**
```markdown
PM_VUELOS.md:
**Modelo de pago:** 100% Millas + Fee de procesamiento

BGR_HOTELES.md:
**Modelo de pago:** Millas (100%) o Millas + Plata (slider con mínimo 20%)
```

### Razones
✅ **Archivos autocontenidos:** Producto tiene contexto completo sin leer COMMON  
✅ **Legibilidad:** Inmediato entender modelo al abrir archivo  
✅ **Independencia:** Producto no depende de otros archivos  
✅ **Impacto mínimo:** Solo 1 línea por archivo (10 archivos = 10 líneas)  
✅ **Patrón consistente:** Todos los productos siguen la misma estructura  

### Consecuencias
✅ Developer/QA entiende contexto inmediatamente  
✅ Archivos son documentos completos y portables  
⚠️ Si cambia modelo de pago, actualizar 11 archivos (COMMON + 10 productos)  

### Alternativas consideradas
- ❌ Solo en COMMON: Productos pierden contexto, menos legibles
- ❌ Variable/placeholder: Sobrecompleja para 1 línea

---

## ADR-005: Creación secuencial de test cases (UNO POR UNO)

**Fecha:** 2026-01-05  
**Estado:** ✅ Aceptado  
**Contexto:** Azure DevOps cancela automáticamente operaciones cuando se crean múltiples test cases en paralelo.

### Decisión
**PROHIBIR** creación en paralelo. Flujo obligatorio:

```
Para cada caso:
1. Create test case → obtener ID
2. Update HTML fields (Descriptions + Considerations)
3. Add to suite
4. Validar agregado
5. Continuar con siguiente caso
```

### Razones
✅ **Confiabilidad:** Azure DevOps no cancela operaciones  
✅ **Trazabilidad:** Saber exactamente qué caso falló si hay error  
✅ **Consistencia:** Todos los casos se crean con misma lógica  
✅ **Validación:** Verificar cada caso antes de continuar  
✅ **Experiencia usuario:** Progress visible caso por caso  

### Consecuencias
✅ 100% éxito en creación de casos  
✅ Errores fáciles de identificar y corregir  
⚠️ Más lento que paralelo (5 casos = ~30 segundos vs ~10 segundos)  
⚠️ Requiere disciplina de no usar batch operations  

### Alternativas consideradas
- ❌ Creación en paralelo: Sistema cancela automáticamente
- ❌ Batch API: No soportado por Azure DevOps Test Plans

---

## ADR-006: Inicio obligatorio desde login en todos los flujos

**Fecha:** 2026-01-05  
**Estado:** ✅ Aceptado  
**Contexto:** ISTQB recomienda reproducibilidad completa. Usuario puede solicitar casos que inicien en "home" o "checkout".

### Decisión
**FORZAR** inicio desde login en TODOS los casos sin excepción.

Si usuario pide caso iniciando en otra pantalla, **corregir automáticamente** agregando pasos de login.

### Razones
✅ **Reproducibilidad completa:** Cualquiera puede ejecutar el caso desde cero  
✅ **Estándar ISTQB:** Mejores prácticas de testing  
✅ **Consistencia:** Todos los casos siguen mismo patrón  
✅ **Validación estado:** Confirma que usuario está autenticado  
✅ **Contexto completo:** No asume precondiciones  

### Consecuencias
✅ Casos ejecutables en cualquier momento  
✅ No requiere setup previo manual  
⚠️ Casos más largos (+2 pasos login)  
⚠️ Usuario puede sentir que son repetitivos  

### Alternativas consideradas
- ❌ Inicio flexible: Pierde reproducibilidad, no cumple ISTQB
- ❌ Precondición "Usuario logueado": Dificulta ejecución automatizada

---

## ADR-007: Metadata YAML en archivos (implementación futura)

**Fecha:** 2026-01-05  
**Estado:** 🔄 Propuesto  
**Contexto:** Falta versionado explícito y metadata estructurada en archivos.

### Decisión (Propuesta)
Agregar frontmatter YAML en archivos:

```yaml
---
version: "1.0.0"
portal: "PM"
producto: "Vuelos"
proveedor: "AGGREGATOR NETACTICA"
ultima_actualizacion: "2026-01-05"
autor: "QA Team"
estado: "activo"
---
```

### Razones
✅ **Versionado:** Saber qué versión de flujo se está usando  
✅ **Trazabilidad:** Quién y cuándo actualizó  
✅ **Validación automatizada:** Scripts pueden leer metadata  
✅ **Búsqueda:** Filtrar por portal/producto/proveedor  
✅ **Estándar:** YAML frontmatter es patrón común en Markdown  

### Consecuencias
✅ Archivos más profesionales  
✅ Habilita automatización futura  
⚠️ Requiere actualizar 10 archivos de productos  
⚠️ Disciplina para mantener metadata actualizada  

### Estado
🔄 Propuesto para implementación en v1.1.0

---

## ADR-008: Estructura de carpetas plana vs jerárquica

**Fecha:** 2026-01-05  
**Estado:** ✅ Aceptado  
**Contexto:** Se debe decidir si agrupar productos por portal en subcarpetas o mantener estructura plana.

### Decisión
**MANTENER** estructura plana en `/products`:

```
products/
├── PM_VUELOS.md
├── PM_HOTELES.md
├── BGR_VUELOS.md
├── BGR_HOTELES.md
...
```

**RECHAZAR** estructura jerárquica:
```
products/
├── PM/
│   ├── VUELOS.md
│   ├── HOTELES.md
└── BGR/
    ├── VUELOS.md
    ├── HOTELES.md
```

### Razones
✅ **Nomenclatura clara:** Prefijo PM/BGR identifica portal  
✅ **Búsqueda fácil:** Todos los archivos en un solo nivel  
✅ **Referencias simples:** Paths cortos en agentes  
✅ **Escalabilidad:** Agregar productos sin crear carpetas  
✅ **Consistencia:** Patrón único de nomenclatura  

### Consecuencias
✅ Fácil encontrar cualquier producto  
✅ No hay carpetas vacías si un portal tiene menos productos  
✅ Ordenamiento alfabético natural agrupa por portal  
⚠️ Carpeta products/ puede tener muchos archivos si crece (aceptable)  

### Alternativas consideradas
- ❌ Jerárquica: Paths más largos, complejidad innecesaria
- ❌ Por tipo (vuelos/, hoteles/): No refleja organización por portal

---

## Historial de Cambios

| ADR | Versión | Fecha | Cambio |
|-----|---------|-------|--------|
| ADR-001 | 1.0.0 | 2026-01-05 | Inicial |
| ADR-002 | 1.0.0 | 2026-01-05 | Inicial |
| ADR-003 | 1.0.0 | 2026-01-05 | Inicial |
| ADR-004 | 1.0.0 | 2026-01-05 | Inicial |
| ADR-005 | 1.0.0 | 2026-01-05 | Inicial |
| ADR-006 | 1.0.0 | 2026-01-05 | Inicial |
| ADR-007 | Propuesto | 2026-01-05 | Propuesto para v1.1.0 |
| ADR-008 | 1.0.0 | 2026-01-05 | Inicial |

---

## Template para Nuevas ADR

```markdown
## ADR-XXX: [Título descriptivo]

**Fecha:** YYYY-MM-DD  
**Estado:** [🔄 Propuesto | ✅ Aceptado | ❌ Rechazado | ⚠️ Deprecado]  
**Contexto:** [Descripción del problema o situación]

### Decisión
[Qué se decidió hacer]

### Razones
[Por qué se tomó esta decisión]

### Consecuencias
[Impacto positivo y negativo de la decisión]

### Alternativas consideradas
[Otras opciones evaluadas y por qué se rechazaron]

### Estado
[Información adicional sobre implementación o seguimiento]
```

---

**Última actualización:** 2026-01-05  
**Versión:** 1.0.0  
**Mantenido por:** QA Team Ultragroup
