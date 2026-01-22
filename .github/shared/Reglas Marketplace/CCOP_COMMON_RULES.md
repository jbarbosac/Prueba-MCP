# 📋 REGLAS COMUNES CONSOLIDACIÓN COP (CCOP)

Documento de referencia con reglas, validaciones y estructura compartida para todos los productos de Consolidación COP.

---

## 🎯 IDENTIFICACIÓN Y ALCANCE

**Portal:** [URL A DEFINIR]  
**País:** Colombia  
**Prefijo obligatorio:** [CCOP]  

**Productos disponibles:**
- ✅ Vuelos
- ✅ Hoteles
- ✅ Autos
- ✅ Actividades
- ✅ Disney (Tickets parques)
- ✅ Asistencias (Seguros de viaje)

---

## 💰 MODELO DE NEGOCIO

### ECUACIÓN DE PAGO:

**[PRODUCTO 1]:**
```
[A DEFINIR]
```

**[PRODUCTO 2]:**
```
[A DEFINIR]
```

### EMISIÓN:
- **[A DEFINIR]** - Automática / Manual / Semiautomática
- [ESPECIFICAR FLUJO DE EMISIÓN]
- [ESPECIFICAR ESTADOS DE RESERVA]

---

## 📦 ESTRUCTURA DE PROVEEDORES

```
CONSOLIDACIÓN COP (CCOP)
├─ ✈️ VUELOS [Framework a definir]
│  ├─ [PROVEEDOR A DEFINIR - ej: AGGREGATOR NETACTICA]
│  ├─ [PROVEEDOR A DEFINIR - ej: AGGREGATOR SABRE]
│  └─ [PROVEEDOR A DEFINIR - ej: SABRE EDIFACT]
│
├─ 🏨 HOTELES [Framework a definir]
│  ├─ HotelBeds (típico)
│  └─ [PROVEEDOR A DEFINIR - ej: DerbySoft]
│
├─ 🚗 AUTOS [Framework a definir]
│  └─ Sabre (Hertz, Dollar, Thrifty, etc.)
│
├─ 🎯 ACTIVIDADES [Framework a definir]
│  └─ HotelBeds (típico)
│
├─ 🎢 DISNEY [Framework a definir]
│  └─ [PROVEEDOR A DEFINIR - ej: DerbySoft/OffLine]
│
└─ 🛡️ ASISTENCIAS [Framework a definir]
   └─ [PROVEEDOR A DEFINIR - ej: Universal Assistance/Assist Card]
```

---

## 🎨 FRAMEWORKS POR PRODUCTO

| Producto | Framework | Observaciones |
|----------|-----------|---------------|
| Vuelos | [A definir] | Múltiples proveedores, emisión [A definir] |
| Hoteles | [A definir] | Confirmación típicamente inmediata |
| Autos | [A definir] | Tarjeta crédito obligatoria para depósito |
| Actividades | [A definir] | Confirmación puede tardar hasta 24h |
| Disney | [A definir] | Tickets digitales, fechas específicas |
| Asistencias | [A definir] | Pólizas digitales, cobertura por región |

---

## ✅ VALIDACIONES CRÍTICAS COMUNES

### 1️⃣ VALIDACIÓN DE SALDO

**¿Cuándo se valida?**
- [A DEFINIR]

**Mensajes de error:**
- [A DEFINIR]

**Casos de prueba relacionados:**
- [A DEFINIR]

---

### 2️⃣ VALIDACIÓN DE CHECKOUT

**Flujo:**
```
[A DEFINIR]
```

**Estados posibles:**
- [A DEFINIR]

---

### 3️⃣ VALIDACIÓN DE EMISIÓN

**Emisión automática:** [Sí/No]
- [CRITERIOS A DEFINIR]

**Emisión manual:** [Sí/No]
- [CRITERIOS A DEFINIR]

**Emisión semiautomática:** [Sí/No]
- [CRITERIOS A DEFINIR]

---

## 🔍 ESTADOS DE RESERVA

| Estado | Descripción | Transiciones posibles |
|--------|-------------|----------------------|
| [ESTADO_1] | [Descripción] | [Estados siguientes] |
| [ESTADO_2] | [Descripción] | [Estados siguientes] |
| [ESTADO_3] | [Descripción] | [Estados siguientes] |
| [ESTADO_4] | [Descripción] | [Estados siguientes] |

---

## 📍 REGLAS ESPECÍFICAS DE PAÍS

**Colombia (COP):**
- [REGLA 1 A DEFINIR]
- [REGLA 2 A DEFINIR]
- [REGLA 3 A DEFINIR]

**Moneda:** COP (Pesos Colombianos)
**Conversión:** [A DEFINIR]

---

## 🎯 FORMATO DE TÍTULO DE CASOS DE PRUEBA

```
[CCOP] {Producto} - {Escenario} - {Proveedor} - {Variante} - {Contexto}
```

**Ejemplos:**
- [CCOP] [Producto] - [Escenario] - [Proveedor] - [Variante]
- [CCOP] [Producto] - [Escenario] - [Proveedor] - [Variante]

---

## 🚦 FLUJO GENERAL DE COMPRA

```mermaid
graph TD
    A[Búsqueda] --> B{Validación saldo}
    B -->|Saldo OK| C[Mostrar resultados]
    B -->|Saldo insuficiente| D[Mensaje error]
    C --> E[Selección producto]
    E --> F[Checkout]
    F --> G{[TIPO DE EMISIÓN]}
    G -->|[OPCIÓN 1]| H[Estado final 1]
    G -->|[OPCIÓN 2]| I[Estado final 2]
```

---

## 📚 DOCUMENTACIÓN DE PRODUCTOS

**Documentos específicos:**
- 📋 [CCOP_VUELOS.md](../../products/B2B/Ultra/CONSOLIDACION%20COP/CCOP_VUELOS.md) ✅
- 📋 [CCOP_HOTELES.md](../../products/B2B/Ultra/CONSOLIDACION%20COP/CCOP_HOTELES.md) ✅
- 📋 [CCOP_AUTOS.md](../../products/B2B/Ultra/CONSOLIDACION%20COP/CCOP_AUTOS.md) ✅
- 📋 [CCOP_ACTIVIDADES.md](../../products/B2B/Ultra/CONSOLIDACION%20COP/CCOP_ACTIVIDADES.md) ✅
- 📋 [CCOP_DISNEY.md](../../products/B2B/Ultra/CONSOLIDACION%20COP/CCOP_DISNEY.md) ✅
- 📋 [CCOP_ASISTENCIAS.md](../../products/B2B/Ultra/CONSOLIDACION%20COP/CCOP_ASISTENCIAS.md) ✅

---

## 🔗 REFERENCIAS

**Reglas compartidas globales:**
- 📋 [SHARED_QA_RULES.md](../SHARED_QA_RULES.md)
- 📋 [AGENT_CONTEXT_VALIDATION.md](../AGENT_CONTEXT_VALIDATION.md)

**Agente especializado:**
- 🤖 [CCOP_QA_Assistant.agent.md](../../agents/CCOP_QA_Assistant.agent.md)

---

## 📝 NOTAS DE IMPLEMENTACIÓN

**Estado del documento:** 🔄 PENDIENTE DEFINICIÓN

**Pendientes:**
- [ ] Definir URL del portal
- [ ] Definir productos disponibles
- [ ] Definir modelo de negocio (millas/puntos/efectivo)
- [ ] Definir tipo de emisión
- [ ] Definir proveedores por producto
- [ ] Definir frameworks tecnológicos
- [ ] Definir estados de reserva
- [ ] Crear documentación específica por producto
- [ ] Definir validaciones críticas
- [ ] Configurar Azure DevOps (planId, suiteId)

**Última actualización:** 2026-01-22  
**Responsable:** [A DEFINIR]  
**Célula:** Kepler (asumido, validar si corresponde)
