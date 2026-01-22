# 📋 REGLAS COMUNES CONSOLIDACIÓN COP (CCOP)

Documento de referencia con reglas, validaciones y estructura compartida para todos los productos de Consolidación COP.

---

## 🎯 IDENTIFICACIÓN Y ALCANCE

**Portal:** [URL A DEFINIR]  
**País:** Colombia  
**Prefijo obligatorio:** [CCOP]  

**Productos disponibles:**
- ✅ Vuelos (En el checkout de este producto se puede adicionar seguro de cancelación)
- ✅ Autos
- ✅ Disney (Tickets parques)
- ✅ Disney Eventos Especiales
- ✅ Asistencias (Seguros de viaje)
- ✅ Actividades
- ✅ Hoteles Disney

---

## 💰 MODELO DE NEGOCIO

### ECUACIÓN DE PAGO:

**DOS MÉTODOS DE PAGO DISPONIBLES:**

```
MÉTODO 1: Tarjeta de Crédito/Débito
   → Pago: 100% TARJETA DE CRÉDITO/DÉBITO
   → Datos requeridos: Sí (se diligencian en checkout)
   → Emisión: AUTOMÁTICA
   → Flujo:
      • Transacción APROBADA → Estado: EMITIDA (email enviado)
      • Transacción RECHAZADA → Estado: PENDIENTE PAGO (sin reintento de pago permitido)
   → Estado final: EMITIDA o PENDIENTE PAGO

MÉTODO 2: Pago en Agencia
   → Pago: 100% EFECTIVO O TARJETA EN AGENCIA
   → Datos requeridos: No (no se diligencia tarjeta en checkout)
   → Emisión: MANUAL (requiere confirmación de pago)
   → Proceso:
      1. Cliente selecciona "Pago en Agencia" en checkout
      2. Reserva queda en estado PENDIENTE PAGO
      3. Cliente acude a agencia física
      4. Cliente paga (efectivo o tarjeta en agencia)
      5. Agente confirma pago en Admin
      6. Agente emite la reserva desde Admin
      7. Estado cambia a EMITIDA
      8. Se envía email automático al cliente
   → Estado final: PENDIENTE PAGO → EMITIDA (tras confirmación en Admin)
```

### CARGOS ADICIONALES (FEES) POR PRODUCTO:

**VUELOS:**
```
1. Tarifa Administrativa (Visible)
   → Tipo: Fija o Porcentual
   → Visibilidad: Cliente ve el cargo desglosado
   → Se suma al precio final

2. Fee Oculto (No Visible)
   → Tipo: Fijo o Porcentual
   → Visibilidad: Cliente NO lo ve desglosado
   → Incluido en precio final
```

**ACTIVIDADES:**
```
Markup (No Desglosado)
   → Tipo: Fijo o Porcentual
   → Visibilidad: No se desglosa en tarifa del cliente
   → Observable: Se puede ver en endpoint de disponibilidad/pagos
```

**OTROS PRODUCTOS (Autos, Disney, Disney Eventos, Asistencias, Hoteles Disney):**
```
Sin cargos adicionales
   → Precio = Precio del proveedor
   → Sin fees ni markups
```

### EMISIÓN:

**Emisión Automática (Default):**
- Todos los productos con **pago tarjeta de crédito/débito** → AUTOMÁTICA
- Flujo:
  1. Cliente ingresa datos de tarjeta en checkout
  2. Transacción procesada en pasarela de pago
  3. Si transacción **APROBADA** → Emisión inmediata
  4. Estado: **EMITIDA**
  5. Email automático enviado al cliente
- Tiempo de emisión: **Inmediato** (segundos tras aprobación)

**Emisión Manual (Excepción):**
- Todos los productos con **pago en agencia** → MANUAL
- Flujo:
  1. Cliente selecciona "Pago en Agencia" en checkout
  2. Reserva creada en estado: **PENDIENTE PAGO**
  3. Cliente recibe instrucciones (email/pantalla) para pagar en agencia
  4. Cliente acude a agencia física y paga (efectivo o tarjeta en agencia)
  5. **Agente confirma pago en Admin**
  6. **Agente emite la reserva desde Admin**
  7. Estado cambia a: **EMITIDA**
  8. Email automático enviado al cliente
- Tiempo de emisión: **Variable** (depende de cuándo cliente pague en agencia)
- Herramienta: **Admin de Consolidación COP**

---

## 📦 ESTRUCTURA DE PROVEEDORES

```
CONSOLIDACIÓN COP (CCOP)
├─ ✈️ VUELOS [Framework Angular]
│  ├─ [AGGREGATOR NETACTICA]
│  ├─ [AGGREGATOR SABRE]
│  └─ [SABRE EDIFACT]
│
├─ 🚗 AUTOS [Framework React]
│  ├─ Localidades de Estados Unidos y Europa proveedor Sabre (Rentadoras: Hertz, Dollar, Thrifty)
│  └─ Localidades de México proveedor Thermeon (Rentadoras: Hertz, Dollar, Thrifty)
│
├─ 🎢 DISNEY [Framework React]
│  └─ [DerbySoft]
│
├─ 🎢 DISNEY EVENTOS ESPECIALES [Framework React]
│  └─ [DerbySoft]
│
│  🛡️ ASISTENCIAS [Framework Angular]
│   └─ [AssistViaje]
│
├─ 🎯 ACTIVIDADES [Framework Angular]
│  └─ HotelBeds
│
└─ 🏨 HOTELES DISNEY [Framework Angular]
   └─ HotelBeds
```

---

## 🎨 FRAMEWORKS POR PRODUCTO

| Producto | Framework | Observaciones |
|----------|-----------|---------------|
| Vuelos | [Angular] | Múltiples proveedores, emisión Automatica |
| Autos | [React] | Dos proveedores, emisión Automatica |
| Disney | [React] | Un proveedor, emisión Automatica |
| Disney Eventos Especiales | [React] | Un proveedor, emisión Automatica |
| Asistencias | [Angular] | Un proveedor, emisión Automatica |
| Actividades | [Angular] | Un proveedor, emisión automatica |
| Hoteles Disney | [Angular] | Un proveedor, emisión automatica |

---

## ✅ VALIDACIONES CRÍTICAS COMUNES

### 1️⃣ VALIDACIÓN DE SALDO

**❌ NO APLICA PARA ESTE MODELO**

- Este marketplace **NO maneja saldo ni crédito**
- Las agencias **NO tienen cupo asignado**
- El cliente paga **100% directamente** (tarjeta o efectivo en agencia)
- No hay validación de saldo en búsqueda, selección ni checkout

---

### 2️⃣ VALIDACIÓN DE CHECKOUT

**DATOS OBLIGATORIOS:**

✅ **1. Datos de Pasajeros/Usuarios**
   - Nombre completo
   - Documento de identidad
   - [Otros campos según producto - Ver doc específica]

✅ **2. Datos de Contacto**
   - Email
   - Teléfono

✅ **3. Datos de Facturación**
   - Tipo de persona: **Natural** o **Jurídica**
   - **Persona Natural:**
     - Nombres
     - Apellidos
     - Tipo de documento
     - Número de documento
   - **Persona Jurídica:**
     - Razón social
     - Tipo de documento
     - Número de documento (NIT)
   - Dirección
   - Ciudad
   - Teléfono

✅ **4. Términos y Condiciones**
   - Aceptación obligatoria

✅ **5. Método de Pago**
   - Selección: Tarjeta o Pago en Agencia

**VALIDACIONES POR MÉTODO DE PAGO:**

**TARJETA DE CRÉDITO/DÉBITO:**
```
✓ Número de tarjeta (formato válido)
✓ CVV (3 o 4 dígitos)
✓ Fecha de expiración (formato MM/AA, no vencida)
✓ Nombre titular
✓ Validaciones adicionales de pasarela de pago
```

**PAGO EN AGENCIA:**
```
✓ Solo confirmar selección de método
✓ No requiere datos adicionales de pago
✓ Cliente recibe instrucciones para acudir a agencia
```

**VALIDACIONES GENERALES:**
- ✅ Todos los campos obligatorios diligenciados
- ✅ Formatos correctos (email, teléfono, documentos)
- ✅ Términos y condiciones aceptados

---

### 3️⃣ VALIDACIÓN DE EMISIÓN

**CRITERIO PRINCIPAL:**
- ✅ **Pago APROBADO** (tarjeta) o **Pago CONFIRMADO en Admin** (agencia)

**FLUJO DE EMISIÓN:**

```
1. Validar pago aprobado/confirmado
2. Llamar endpoint de emisión del proveedor
3. Respuesta del proveedor:
   ├─ ✅ ÉXITO → Reserva pasa a EMITIDA
   └─ ❌ FALLA → Reserva queda en PENDIENTE
```

**ESCENARIO: FALLA DE EMISIÓN**

⚠️ **¿Puede fallar emisión después de pago aprobado?**  
→ **SÍ**, el endpoint del proveedor puede fallar

**¿Qué ocurre cuando falla?**
```
Pago: APROBADO ✅
Emisión: FALLIDA ❌
Estado: PENDIENTE (requiere intervención manual)
```

**GESTIÓN DE REINTENTO:**
- ❌ **NO hay reintento automático**
- 🔧 **Gestión manual:** Agente debe reintentar emisión desde **Admin**
- 🔔 **Notificación:** Se notifica al **agente** (NO al cliente)
- 👤 **Responsable:** Agente en Admin gestiona el reintento
- ✅ **Resolución:** Una vez emitida exitosamente → Estado: **EMITIDA** + Email al cliente

**TIPOS DE EMISIÓN:**
- ✅ **Emisión Automática:** Pago con tarjeta aprobado → Emisión inmediata
- ✅ **Emisión Manual:** Pago en agencia confirmado por agente → Emisión desde Admin
- ❌ **Emisión Semiautomática:** NO APLICA

---

## 🔍 ESTADOS DE RESERVA

| Estado | Descripción | ¿Cómo se llega a este estado? | Transiciones posibles |
|--------|-------------|-------------------------------|----------------------|
| **EMITIDA** | Reserva confirmada y emitida con proveedor. Cliente recibe voucher/confirmación por email. | **1.** Pago con tarjeta APROBADO + Emisión exitosa<br>**2.** Pago en agencia confirmado por agente + Emisión exitosa | → **[A DEFINIR]** (¿Cancelada? ¿Modificada?) |
| **PENDIENTE PAGO** | Reserva creada pero esperando pago. Cliente debe acudir a agencia física. | **1.** Cliente selecciona "Pago en Agencia" en checkout<br>**2.** Pago con tarjeta RECHAZADO (no hay reintento) | → **EMITIDA** (tras pago confirmado en agencia)<br>→ **[A DEFINIR]** (¿Expirada? ¿Cancelada?) |
| **PENDIENTE** | Reserva con pago aprobado pero emisión con proveedor falló. Requiere intervención manual. | **1.** Pago APROBADO pero endpoint de emisión del proveedor **FALLÓ** | → **EMITIDA** (tras reintento exitoso)<br>→ **[A DEFINIR]** (¿Cancelada? ¿Reembolsada?) |
| **[A DEFINIR]** | [¿Existen otros estados? Ej: Cancelada, Modificada, Expirada, Reembolsada, etc.] | [A definir] | [A definir] |

**NOTAS:**
- 📧 **Email automático se envía solo cuando reserva pasa a EMITIDA** (tanto para tarjeta como agencia)
- 🔄 **Transiciones adicionales:** ¿Se pueden cancelar reservas? ¿Modificar? ¿Reembolsar? [A DEFINIR]
- ❌ **Rechazo de tarjeta:** NO hay reintento de pago. Reserva pasa a PENDIENTE PAGO y cliente debe acudir a agencia
- 🔀 **Dos caminos a PENDIENTE PAGO:** (1) Cliente elige "Pago en Agencia", (2) Pago con tarjeta rechazado
- ⚠️ **PENDIENTE (falla emisión):** Pago aprobado pero emisión falló. Agente gestiona reintento desde Admin. NO hay reintento automático.

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
