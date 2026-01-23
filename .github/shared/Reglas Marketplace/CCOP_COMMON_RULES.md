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
      • Transacción RECHAZADA → Estado: PENDIENTE (requiere acción del agente)
   → Estado final: EMITIDA o PENDIENTE

MÉTODO 2: Pago en Agencia
   → Pago: 100% EFECTIVO O TARJETA EN AGENCIA
   → Datos requeridos: No (no se diligencia tarjeta en checkout)
   → Emisión: MANUAL (requiere confirmación de pago)
   → Proceso:
      1. Cliente selecciona "Pago en Agencia" en checkout
      2. Reserva queda en estado PENDIENTE
      3. Cliente acude a agencia física
      4. Cliente paga (efectivo o tarjeta en agencia)
      5. Agente confirma pago en Admin
      6. Agente emite la reserva desde Admin
      7. Estado cambia a EMITIDA
      8. Se envía email automático al cliente
   → Estado final: PENDIENTE → EMITIDA (tras confirmación en Admin)
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
   → Observable: Se puede ver en los endpoint de disponibilidad/pagos
```

**OTROS PRODUCTOS (Autos, Disney, Disney Eventos Especiales, Asistencias, Hoteles Disney):**
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
  2. Reserva creada en estado: **PENDIENTE**
  3. Cliente recibe instrucciones (pantalla) para pagar en agencia
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
| **EMITIDA** | Reserva confirmada y emitida con proveedor. Cliente recibe voucher/confirmación por email. | **1.** Pago con tarjeta APROBADO + Emisión exitosa<br>**2.** Pago en agencia confirmado por agente + Emisión exitosa | → **CANCELADA** (solo por agente desde Admin) |
| **PENDIENTE** | Reserva creada pero requiere acción del agente. Puede ser por: pago pendiente en agencia, pago con tarjeta rechazado o emisión fallida con proveedor. | **1.** Cliente selecciona "Pago en Agencia" en checkout<br>**2.** Pago con tarjeta RECHAZADO (requiere gestión del agente)<br>**3.** Pago con tarjeta APROBADO pero endpoint de emisión del proveedor **FALLÓ** | → **EMITIDA** (tras pago confirmado + emisión exitosa)<br>→ **PENDIENTE** (reintento emisión falla, continúa igual)<br>→ **CANCELADA** (por agente desde Admin) |
| **CANCELADA** | Reserva cancelada por el agente desde el Admin. No se puede recuperar. | **1.** Agente cancela desde Admin una reserva en cualquier estado | → **Sin transiciones** (estado final) |

---

### 📋 REGLAS DE ESTADOS

**✅ REGLAS DE CANCELACIÓN:**
- ❌ **Cliente NO puede cancelar:** No existe opción de auto-cancelación para el cliente
- ✅ **Agente SÍ puede cancelar:** Desde Admin, puede cancelar reservas en cualquier estado
- 🔒 **Estado CANCELADA es final:** No hay reversión posible
- ❌ **No existe estado REEMBOLSADA:** Las cancelaciones no generan estado de reembolso

**✅ REGLAS DE MODIFICACIÓN:**
- ❌ **Cliente NO puede modificar:** No existe funcionalidad de modificación de reservas
- ❌ **No existe estado MODIFICADA:** Las reservas mantienen su estado original
- 💡 **Alternativa:** Para cambios, el agente debe cancelar y crear nueva reserva

**✅ REGLAS DE EMISIÓN FALLIDA (PENDIENTE):**
- 🔄 **Reintento manual:** Agente reintenta emisión desde Admin
- ♻️ **Reintento ilimitado:** Si falla, continúa en PENDIENTE para nuevos reintentos
- ⚠️ **Sin reintento automático:** Sistema NO reintenta automáticamente
- 🔧 **Resolución:** Agente decide continuar reintentando o cancelar la reserva

**✅ REGLAS DE EXPIRACIÓN:**
- ❌ **No existe estado EXPIRADA:** Las reservas PENDIENTE no expiran automáticamente
- 🔧 **Gestión manual:** Si el cliente no paga, el agente debe cancelar manualmente desde Admin

**❌ ESTADOS QUE NO EXISTEN:**
- ❌ EXPIRADA
- ❌ REEMBOLSADA
- ❌ MODIFICADA
- ❌ RECHAZADA
- ❌ ERROR
- ❌ EN PROCESO

---

### 📧 NOTIFICACIONES POR ESTADO

| Estado | ¿Envía email al cliente? | ¿Notifica al agente? | Contenido |
|--------|-------------------------|---------------------|-----------|
| **EMITIDA** | ✅ SÍ (automático) | ❌ NO | Voucher/confirmación de reserva |
| **PENDIENTE** | ✅ SÍ (automático) | ❌ NO | **Cliente:** Notificación indicando que la reserva quedó en estado reservado<br>**Agente:** Alerta para gestionar la reserva (pago pendiente, pago rechazado o emisión fallida) |
| **CANCELADA** | ✅ SÍ (automático) | ❌ NO | Notificación de cancelación de reserva |

---

### 🔄 DIAGRAMA DE TRANSICIONES

```
┌─────────────────┐
│  CHECKOUT       │
└────────┬────────┘
         │
         ├──► Pago Tarjeta APROBADO + Emisión OK ──────────────────► EMITIDA ────┐
         │                                                                │         │
         ├──► Pago en Agencia seleccionado ─────────────────────────► PENDIENTE ──┤
         │                                                                │         │
         ├──► Pago Tarjeta RECHAZADO ───────────────────────────────────►  │        │
         │                                                                │         │
         └──► Pago Tarjeta APROBADO + Emisión FALLA ───────────────────►  │        │
                                                                           │         │
                    ┌──────────────────────────────────────────────────────┘         │
                    │                                                                │
                    │  Agente confirma pago + emite                                  │
                    ▼                                                                │
               ┌─────────┐                                                           │
               │ EMITIDA │◄──────────────────────────────────────────────────────────┘
               └────┬────┘                                                            
                    │                                                                
                    │  Agente cancela desde Admin                                    
                    ▼                                                                
            ┌──────────────┐          ┌─────────────────────────────────────────────┘
            │  CANCELADA   │  ◄───────┤ Agente cancela desde Admin
            │(estado final)│          │ (desde cualquier estado)
            └──────────────┘          └─────────────────────────────────────────────
```

---

### 📝 NOTAS IMPORTANTES

- 📧 **Notificaciones por email:**
  - ✅ **EMITIDA:** Email con voucher/confirmación
  - ✅ **PENDIENTE:** Email informando que reserva quedó en estado reservado (requiere gestión)
  - ✅ **CANCELADA:** Email notificando la cancelación de la reserva

- ⚠️ **Estado PENDIENTE tiene 3 causas posibles:**
  - 🏦 Cliente seleccionó "Pago en Agencia" (esperando pago)
  - 💳 Pago con tarjeta RECHAZADO (requiere gestión del agente)
  - ❌ Pago aprobado pero emisión con proveedor FALLÓ (requiere reintento)

- 🔧 **Gestión manual requerida:** Todas las reservas PENDIENTE requieren acción del agente en Admin
- ❌ **Pago rechazado NO reintenta:** Sistema NO permite reintento automático de pago. Agente debe gestionar
- 🔄 **Sin límite de reintentos de emisión:** Cuando falla emisión, se puede reintentar indefinidamente
- 🔒 **Gestión exclusiva por agente:** Solo el agente desde Admin puede cancelar reservas. Cliente no tiene esta opción
- ⏱️ **Sin expiración automática:** Las reservas PENDIENTE NO expiran, deben ser gestionadas manualmente

---

## 📍 REGLAS ESPECÍFICAS DE PAÍS

**País:** Colombia  
**Moneda principal:** COP (Pesos Colombianos)

---

### 🆔 DOCUMENTOS DE IDENTIDAD

**Tipos de documentos aceptados:**
- ✅ **Cédula de Ciudadanía** (Colombia)
- ✅ **Pasaporte** (Internacional)

**Validaciones:**
- ✅ **Cédula de Ciudadanía:** Debe tener exactamente **10 dígitos**
- ✅ **Pasaporte:** Formato alfanumérico estándar internacional

---

### 💰 MONEDA Y CONVERSIÓN

**Regla general:**
- 📍 **Todos los productos** se muestran y cobran en **COP (Pesos Colombianos)**

**Excepciones por producto:**

**🚗 AUTOS:**
```
Disponibilidad: Se muestra en USD por defecto
              → Cliente puede cambiar visualización a COP
Pago final:    Siempre se cobra en COP
Conversión:    Sistema aplica conversión automática USD → COP al momento del pago
```

**🎢 DISNEY (Tickets Parques):**
```
Disponibilidad: Se muestra en USD
Selección:      Se mantiene en USD
Checkout:       Se cobra en USD
Conversión:     NO se hace conversión a COP
Nota:           Cliente paga directamente en dólares (USD)
```

**Resumen de monedas por producto:**
| Producto | Moneda de visualización | Moneda de cobro | ¿Conversión? |
|----------|------------------------|----------------|--------------|
| Vuelos | COP | COP | No aplica |
| Autos | USD (cambiable a COP) | COP | Sí (USD → COP) |
| Disney | USD | USD | No |
| Disney Eventos Especiales | USD | USD | No |
| Asistencias | COP | COP | No aplica |
| Actividades | COP | COP | No aplica |
| Hoteles Disney | COP | COP | No aplica |

---

### 🧾 IMPUESTOS

**VUELOS:**
- ✅ **Impuestos desglosados:** Los impuestos se muestran de forma separada en el desglose de precio
- 📋 **Visibilidad:** Cliente puede ver claramente cuánto corresponde a impuestos

**OTROS PRODUCTOS:**
- 📍 **Sin desglose confirmado:** No se especifica si hay impuestos desglosados
- 💡 **Precio final:** Los precios pueden incluir impuestos, pero no se muestran de forma separada

---

### 💳 FORMAS DE PAGO

**Pasarela de pago:**
- 🏦 **PlacetoPay** (única pasarela habilitada)

**Métodos de pago disponibles:**
1. **Tarjeta de Crédito/Débito** (procesada por PlacetoPay)
2. **Pago en Agencia Física** (efectivo o tarjeta en agencia)

---

### 🚫 REGULACIONES Y RESTRICCIONES

**Restricciones por edad:**
- ✅ **NO hay restricciones por edad** para ningún producto
- 💡 **Nota:** El sistema permite reservas para todas las edades

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
