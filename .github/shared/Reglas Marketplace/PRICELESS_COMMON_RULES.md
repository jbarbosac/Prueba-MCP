# 📋 REGLAS COMUNES MASTERCARD PRICELESS 2X1 (Priceless)

Documento de referencia con reglas, validaciones y estructura compartida para todos los productos de Mastercard Priceless 2X1.

---

## 🎯 IDENTIFICACIÓN Y ALCANCE

**Portal Test:** https://test-skynet-pmc.smartlinks.dev/es-co  
**Portal Demo:** https://demo-skynet-pmc.smartlinks.dev/es-co  
**Portal Producción:** https://vuelaconoccidente.com/es-co  
**País:** Colombia  
**Prefijo obligatorio:** [Priceless]  
**Célula:** Skynet  
**Tipo de Cliente:** B2C (Business to Consumer)

**Productos disponibles:**
- ✅ Home (Framework: React)
- ✅ Vuelos (Framework: Angular)
- ✅ Hoteles (Framework: Angular)
- ✅ Autos (Framework: React)

---

## 💰 MODELO DE NEGOCIO

### CARACTERÍSTICAS PRINCIPALES:

- **Tipo:** B2C (Business to Consumer)
- **Autenticación:** ❌ NO requiere login/registro (acceso directo al portal)
- **Moneda:** 100% Dinero (COP - Pesos Colombianos)
- **Promociones:** 2X1 o Descuentos según reglas de negocio de Mastercard
- **Pasarela de Pago:** PlacetoPay
- **Dispersión de Fondos:** Sí (habilitada)

### ECUACIÓN DE PAGO:

**TODOS LOS PRODUCTOS:**
```
Producto = 100% DINERO (COP)
Promoción = 2X1 o DESCUENTO (según reglas de negocio Mastercard)
Pasarela = PlacetoPay
Dispersión = SÍ
```

### EMISIÓN:
- **Variable según escenario** (depende de promoción, dispersión y fee oculto)
- Puede ser automática con TC del cliente o TC corporativa
- Emisión en CASH cuando no hay dispersión activa

### CANCELACIONES Y REVERSOS:
- **Cambio de estado:** Cancelación actualiza estado a CANCELADO automáticamente
- **Reversos de TC:** ⚠️ NO son automáticos
- **Proceso manual:** El equipo de operaciones ejecuta todos los reversos manualmente
- **Vuelos (múltiples transacciones):** Reverso manual de TC Cliente + TC Corporativa (si aplica)
- **Hoteles/Autos (transacción única):** Reverso manual de TC Cliente
- **Políticas:** Reembolsos sujetos a políticas del proveedor (pueden incluir penalidades)

---

## 💳 REGLAS DE NEGOCIO: PAGO Y EMISIÓN

### ⚠️ IMPORTANTE: ALCANCE DE ESCENARIOS

**VUELOS:**
- ✅ Aplican los 7 escenarios de pago/emisión (según dispersión, fee oculto, tipo de promoción)
- ✅ Dispersión de fondos condicional
- ✅ Uso de TC Corporativa en escenarios específicos
- ✅ Emisión variable: TC Cliente, TC Corporativa, CASH, Mixta

**HOTELES Y AUTOS:**
- ❌ NO aplican los 7 escenarios
- ✅ Pago directo al Marketplace (Ultragroup) - 1 transacción TC Cliente
- ✅ Emisión SIEMPRE en CASH (automática)
- ❌ NO hay dispersión de fondos
- ❌ NO se usa TC Corporativa

---

### CONCEPTOS CLAVE (SOLO VUELOS):

**Dispersión de Fondos:**
- Distribución automática de pagos entre aerolínea y Ultragroup(Marketplace)
- Solo disponible para aerolíneas con dispersión activa
- Permite emisión directa con TC del cliente
- **⚠️ SOLO APLICA A VUELOS**

**Fee Oculto:**
- Cargo adicional no visible en el precio final mostrado al usuario
- Requiere pago separado con TC corporativa
- Afecta el flujo de emisión de tiquetes
- **⚠️ SOLO APLICA A VUELOS**

**Tarjeta Corporativa (TC Corporativa):**
- Tarjeta de crédito empresarial de Ultragroup
- Utilizada para cubrir segundo tiquete en 2X1 o fees ocultos
- Pago posterior se hace manualmente a la aerolínea
- **⚠️ SOLO SE USA EN VUELOS**

---

## 🔄 ESCENARIOS DE PAGO Y EMISIÓN (SOLO VUELOS)

### **ESCENARIO 1: Edifact - 2X1 SIN fee oculto + Dispersión ACTIVA**

**Pagos:**
- 1 transacción: TC del cliente (vía PlacetoPay - P2P)
- Dispersión de fondos automática:
  - Valor de un solo PQ → Aerolínea
  - Fee transaccional → Ultragroup
- 1 transacción: TC corporativa (valor de un solo PQ a la aerolínea)

**Emisión:**
- 1er Tiquete: Emitido con TC del Cliente
- 2do Tiquete: Emitido con TC Corporativa

---

### **ESCENARIO 2: Edifact - 2X1 SIN fee oculto + Dispersión INACTIVA**

**Pagos:**
- 1 transacción: TC del cliente
- Todo el dinero entra a Ultragroup
- NO hay pago con TC corporativa

**Emisión:**
- 2 tiquetes: Emitidos en CASH (pago manual posterior a aerolínea)

---

### **ESCENARIO 3: 2X1 o Descuento CON fee oculto + Dispersión ACTIVA**

**Pagos:**
- 1 transacción: TC del cliente
- Todo el dinero entra a Ultragroup
- 1 transacción: TC corporativa (valor de los DOS PQ a la aerolínea)

**Emisión:**
- 2 tiquetes: Emitidos con TC Corporativa

---

### **ESCENARIO 4: 2X1 o Descuento CON fee oculto + Dispersión INACTIVA**

**Pagos:**
- 1 transacción: TC del cliente
- Todo el dinero entra a Ultragroup
- NO hay pago con TC corporativa

**Emisión:**
- 2 tiquetes: Emitidos en CASH (pago manual posterior a aerolínea)

---

### **ESCENARIO 5: Edifact - Descuento SIN fee oculto + Dispersión ACTIVA**

**Pagos:**
- 1 transacción: TC del cliente (vía PlacetoPay - P2P)
- Dispersión de fondos automática:
  - Fee transaccional → Ultragroup
  - Restante → Aerolínea
- NO hay pago con TC corporativa

**Emisión:**
- 1er Tiquete: Emitido con TC del Cliente
- 2do Tiquete: Emitido en CASH + TC del Cliente (combinado)

---

### **ESCENARIO 6: Edifact - Descuento SIN fee oculto + Dispersión INACTIVA**

**Pagos:**
- 1 transacción: TC del cliente
- Todo el dinero entra a Ultragroup
- NO hay pago con TC corporativa

**Emisión:**
- 2 tiquetes: Emitidos en CASH (pago manual posterior a aerolínea)

---

### **ESCENARIO 7: Aggregator (Sabre NDC o Netactica)**

**Pagos:**
- 1 transacción: TC del cliente
- Todo el dinero entra a la agencia (Ultragroup)

**Emisión:**
- 2 tiquetes: Emitidos en CASH (pago manual posterior)

**⚠️ Nota:** Los agregadores NO soportan dispersión de fondos automática.

---

## 📊 TABLA RESUMEN: PAGO Y EMISIÓN (SOLO VUELOS)

| Escenario | Promoción | Fee Oculto | Dispersión | Pago TC Cliente | Pago TC Corporativa | Emisión 1er Tiquete | Emisión 2do Tiquete |
|-----------|-----------|------------|------------|-----------------|---------------------|---------------------|---------------------|
| **1** | 2X1 | NO | SÍ | 1 PQ + Fee | 1 PQ | TC Cliente | TC Corporativa |
| **2** | 2X1 | NO | NO | Total | - | Cash | Cash |
| **3** | 2X1/Desc | SÍ | SÍ | Total | 2 PQ | TC Corporativa | TC Corporativa |
| **4** | 2X1/Desc | SÍ | NO | Total | - | Cash | Cash |
| **5** | Descuento | NO | SÍ | Total | - | TC Cliente | Cash + TC Cliente |
| **6** | Descuento | NO | NO | Total | - | Cash | Cash |
| **7** | Cualquiera | - | NO (Aggregator) | Total | - | Cash | Cash |

### **HOTELES Y AUTOS - MODELO SIMPLIFICADO:**

| Producto | Pago | Emisión | Dispersión | TC Corporativa | Markup |
|----------|------|---------|------------|----------------|--------|
| **Hoteles** | TC Cliente → Ultragroup (total) | CASH automática | NO | NO | $10,000 COP/habitación |
| **Autos** | TC Cliente → Ultragroup (total) | CASH automática | NO | NO | Incluido en tarifa |

**Características:**
- ✅ Promociones 2X1 o Descuento aplicadas al precio final
- ✅ **Hoteles:** Markup $10,000 COP por habitación (discriminado)
- ✅ **Autos:** Sin markup adicional (incluido en tarifa del proveedor)
- ✅ 1 sola transacción por reserva
- ✅ Emisión automática en CASH
- ❌ Sin escenarios complejos de pago/emisión
- ❌ Sin fee oculto
- ❌ Sin dispersión de fondos
- ❌ Sin TC Corporativa

---

## ⚙️ CONFIGURACIÓN TÉCNICA

### **Collection: allowedAirports**
- Base de datos interna de MongoDB
- Define manualmente aeropuertos habilitados para búsqueda y emisión
- Control total sobre rutas disponibles
- NO usa configuración externa de proveedores

### **Pasarela de Pago: PlacetoPay**
- Integración P2P (Place to Pay)
- Soporte para dispersión de fondos
- Moneda: COP (Pesos Colombianos)
- País: Colombia

---

## 🧮 REGLAS DE CÁLCULO: PROMOCIONES 2X1 Y DESCUENTO

### ⚠️ IMPORTANTE: DIFERENCIAS POR PRODUCTO

**VUELOS:**
- **Fee Transaccional:** $10,000 COP por pasajero
- **Fee Oculto:** Variable (según aerolínea)
- **Total para 2 PAX:** $20,000 COP (fee transaccional)

**HOTELES:**
- **Markup:** $10,000 COP por habitación (discriminado en el precio)
- **Fee Oculto:** ❌ NO existe
- **Total para 2 habitaciones:** $20,000 COP (markup)

**AUTOS:**
- **Markup:** Incluido en tarifa final del proveedor (NO discriminado)
- **Fee Oculto:** ❌ NO existe

---

### **COMPONENTES DEL PRECIO (VUELOS):**

**Valores por Pasajero:**
- `Base`: Tarifa base del tiquete sin impuestos
- `Total Taxes`: Suma de todos los impuestos
- `Fee Oculto (HF)`: Cargo adicional no visible al usuario (si aplica)
- `Fee Transaccional`: Cargo fijo = **$10,000 COP por pasajero**

---

### **REGLA DE NEGOCIO: PROMOCIÓN 2X1**

**Concepto:** Cliente paga 1 tiquete y obtiene 2.

**Fórmula de cálculo:**
```
Precio base de 1 pasajero = Base + Total Taxes
VALOR TOTAL = Precio base (1 pasajero) + (Fee Transaccional × 2 pasajeros)
```

**Características:**
- ✅ Cliente paga la tarifa de **1 solo pasajero**
- ✅ Fee transaccional se cobra por **2 pasajeros** ($20,000 COP)
- ✅ Fee oculto (si existe) es cubierto por Ultragroup o TC Corporativa
- ✅ NO se muestra como "descuento", simplemente se cobra 1 tiquete

**Ejemplo simplificado:**
```
Si 1 tiquete cuesta $441,830 COP:
- Cliente paga: $441,830 (1 tiquete) + $20,000 (fees de 2 PAX)
- Total a pagar: $461,830 COP
- Cliente recibe: 2 tiquetes
```

---

### **REGLA DE NEGOCIO: DESCUENTO**

**Concepto:** Cliente paga 2 tiquetes con descuento aplicado al total.

**Fórmula de cálculo:**
```
Precio base 2 pasajeros = (Base + Total Taxes) × 2
VALOR TOTAL = (Precio base 2 pasajeros - Descuento) + (Fee Transaccional × 2)
```

**Características:**
- ✅ Se calcula precio de **2 pasajeros completo**
- ✅ Descuento se aplica **DESPUÉS** de sumar los 2 pasajeros
- ✅ Fee transaccional se cobra por **2 pasajeros** ($20,000 COP)
- ✅ Fee oculto (si existe) se incluye en cálculo interno pero NO se muestra al usuario
- ✅ Descuento puede ser **fijo** (ej: $400,000) o **porcentaje** (ej: 30%)

**Ejemplo simplificado:**
```
Si 2 tiquetes cuestan $926,380 COP y descuento es $400,000:
- Precio base 2 PAX: $926,380
- Descuento aplicado: -$400,000
- Subtotal: $526,380
- Fee transaccional (2 PAX): +$20,000
- Total a pagar: $546,380 COP
```

---

### **DIFERENCIAS CLAVE ENTRE 2X1 Y DESCUENTO:**

| Aspecto | 2X1 | Descuento |
|---------|-----|-----------|
| **Base de cálculo** | 1 pasajero | 2 pasajeros |
| **Descuento visible** | NO (se cobra 1 tiquete directo) | SÍ (se muestra el descuento) |
| **Precio antes de fees** | Tarifa de 1 PAX | Tarifa de 2 PAX - Descuento |
| **Fee transaccional (Vuelos)** | $20,000 (2 PAX) | $20,000 (2 PAX) |
| **Markup (Hoteles)** | $20,000 (2 habitaciones) | $20,000 (2 habitaciones) |
| **Markup (Autos)** | Incluido en tarifa | Incluido en tarifa |
| **Cliente recibe** | 2 tiquetes pagando 1 | 2 tiquetes con descuento |

---

### **FEE TRANSACCIONAL (Constante):**

- **Valor fijo**: $10,000 COP por pasajero
- **Total para 2 PAX**: $20,000 COP
- **Se cobra SIEMPRE**: Independiente del tipo de promoción
- **Visible al usuario**: Sí, aparece desglosado en el precio final

---

### **FEE OCULTO (Variable):**

- **NO visible al usuario**: No aparece en el desglose de precios
- **Cubierto por**: Ultragroup o TC Corporativa (según escenario)
- **Solo en algunos casos**: Depende de la tarifa negociada con la aerolínea
- **Impacta en**: Método de pago y emisión (ver sección "Escenarios de Pago y Emisión")

---

### **🎯 VALIDACIONES DE CÁLCULO (QA):**

✅ **Para promoción 2X1:**
- Verificar que se cobre solo 1 tiquete (no 2)
- Confirmar fee transaccional = $20,000 COP (2 PAX)
- Validar que fee oculto NO aparezca al usuario
- Verificar que cliente reciba 2 tiquetes

✅ **Para promoción Descuento:**
- Verificar que descuento se aplique sobre precio de 2 PAX
- Confirmar fee transaccional = $20,000 COP (2 PAX)
- Validar que descuento se muestre claramente
- Verificar que precio final = (2 PAX - Descuento) + Fees

✅ **General:**
- Fee transaccional SIEMPRE $10,000 por pasajero
- Fee oculto NUNCA visible al usuario
- Precio final coherente con escenario de pago/emisión

---

## 📦 ESTRUCTURA DE PROVEEDORES

```
MASTERCARD PRICELESS 2X1 (Priceless)
├─ 🛫 VUELOS (7 Escenarios de pago/emisión)
│  ├─ SABRE EDIFACT (Dispersión condicional)
│  ├─ AGGREGATOR - NETATICA (Sin dispersión)
│  └─ AGGREGATOR - SABRE NDC (Sin dispersión)
│
├─ 🏨 HOTELES (Pago directo - Emisión CASH)
│  └─ SABRE (Sin dispersión)
│
└─ 🚗 AUTOS (Pago directo - Emisión CASH)
   ├─ Hertz (Sin dispersión)
   └─ Thermeon - México (Sin dispersión)
```

---

## ✅ VALIDACIONES GLOBALES

### VALIDACIONES DE PAGOS:
- ✅ Verificar integración correcta con PlacetoPay (P2P)
- ✅ Validar que se ejecute el escenario de pago correcto según:
  - Tipo de promoción (2X1 o Descuento)
  - Presencia de fee oculto (SÍ/NO)
  - Estado de dispersión de la aerolínea (ACTIVA/INACTIVA)
  - Tipo de proveedor (Edifact vs Aggregator)
- ✅ Confirmar cantidad de transacciones esperadas (1 o 2)
- ✅ Validar uso correcto de TC del cliente vs TC corporativa
- ✅ Verificar montos finales en COP

### VALIDACIONES DE PROMOCIONES:
- ✅ Identificar correctamente el tipo de promoción (2X1 o Descuento)
- ✅ Verificar elegibilidad del usuario para promociones Mastercard
- ✅ Validar disponibilidad de la promoción en la aerolínea seleccionada
- ✅ Confirmar que se aplica solo UNA promoción por reserva
- ✅ **Validar cálculo correcto de descuento o 2X1** (ver sección Fórmulas de Cálculo)
- ✅ **Verificar que fee transaccional sea $10,000 COP por pasajero**
- ✅ **Confirmar que fee oculto NO se muestre al usuario**
- ✅ Validar que el descuento o 2X1 se aplique correctamente al precio final
- ✅ Verificar términos y condiciones de Mastercard

### VALIDACIONES DE EMISIÓN:

**VUELOS:**
- ✅ Verificar método de emisión correcto según escenario (1-7):
  - TC del Cliente
  - TC Corporativa
  - CASH (pago manual posterior)
  - Combinado (Cash + TC Cliente)
- ✅ Validar emisión del 1er tiquete según escenario
- ✅ Validar emisión del 2do tiquete según escenario
- ✅ Confirmar que NO se requiere intervención manual (excepto CASH)

**HOTELES:**
- ✅ Verificar SIEMPRE emisión en CASH (automática)
- ✅ Confirmar 1 sola transacción TC Cliente
- ✅ Validar markup $10,000 COP por habitación (discriminado)
- ✅ Validar que NO se use TC Corporativa
- ✅ Verificar voucher/confirmación generado correctamente

**AUTOS:**
- ✅ Verificar SIEMPRE emisión en CASH (automática)
- ✅ Confirmar 1 sola transacción TC Cliente
- ✅ Validar que markup NO se discrimine (incluido en tarifa)
- ✅ Validar que NO se use TC Corporativa
- ✅ Verificar voucher/confirmación generado correctamente

### VALIDACIONES DE DISPERSIÓN (SOLO VUELOS):
- ✅ Confirmar estado de dispersión de la aerolínea (ACTIVA/INACTIVA)
- ✅ Validar que se ejecute dispersión SOLO si está activa
- ✅ Verificar distribución correcta de fondos:
  - Valor de PQ → Aerolínea
  - Fee transaccional → Ultragroup
- ✅ Confirmar trazabilidad completa de la transacción
- ✅ Validar que aggregators NO ejecuten dispersión (siempre CASH)
- ⚠️ **Hoteles y Autos NO tienen dispersión**

### VALIDACIONES DE FEE OCULTO (SOLO VUELOS):
- ✅ Identificar si existe fee oculto en la tarifa
- ✅ Validar que fee oculto active uso de TC corporativa
- ✅ Confirmar que fee oculto NO se muestre al usuario
- ✅ Verificar que el pago con TC corporativa cubra el fee
- ⚠️ **Hoteles y Autos NO manejan fee oculto**

### VALIDACIONES DE AEROPUERTOS:
- ✅ Verificar que aeropuerto de origen esté en collection `allowedAirports`
- ✅ Verificar que aeropuerto de destino esté en collection `allowedAirports`
- ✅ Validar que búsqueda solo muestre rutas habilitadas
- ✅ Confirmar que emisión solo proceda para aeropuertos permitidos

### VALIDACIONES DE CANCELACIÓN:
- ⚠️ **Reversos NO automáticos:** Los pagos con TC Cliente NO se reversan automáticamente
- ⚠️ **Proceso manual:** El equipo de operaciones ejecuta los reversos manualmente
- ✅ Validar estado cambio a CANCELADO en el sistema
- ✅ Verificar políticas de cancelación aplicables (producto y proveedor)
- ✅ Confirmar penalidades según políticas (si aplica)
- ⚠️ **Vuelos con TC Corporativa:** Reverso de TC Corporativa también es manual
- ⚠️ **Hoteles:** Reverso único de TC Cliente (proceso manual) + markup
- ⚠️ **Autos:** Reverso único de TC Cliente (proceso manual) - markup incluido en tarifa
- ✅ Reembolsos según políticas del proveedor
- ✅ Notificación al cliente sobre cancelación procesada

---

## 🔗 REFERENCIAS

- 📚 [SHARED_QA_RULES.md](../SHARED_QA_RULES.md) - Fundamentos ISTQB y Azure DevOps
- 📋 [Documentación Mastercard Priceless en Wiki Azure]
- 📋 [PlacetoPay Integration Documentation]

---

## 📊 DATOS AZURE DEVOPS

```yaml
project: "ultragroupla"
planId: [PENDIENTE CONFIGURAR]
suiteId: [PENDIENTE CONFIGURAR]
```

**⚠️ IMPORTANTE:** Estos valores deben ser configurados antes de crear casos de prueba.

---

## 🎯 PARTICULARIDADES DEL MODELO PRICELESS

### DIFERENCIAS CON OTROS MODELOS:

**vs. Modelos de Puntos/Millas (PM, BGR, CME):**
- ❌ NO usa puntos ni millas
- ❌ NO requiere login (acceso directo)
- ✅ Pago 100% en dinero (COP)
- ✅ Beneficio viene de promociones (2X1/Descuento), NO de millas
- ✅ Múltiples escenarios de emisión (TC Cliente, TC Corporativa, CASH)

**vs. Modelos Corporativos:**
- ✅ B2C (consumidor final)
- ❌ NO requiere centro de costos
- ❌ NO requiere aprobaciones empresariales
- ✅ Usa TC corporativa para casos específicos (fee oculto, segundo tiquete 2X1)

**vs. Otros B2C (especialmente MRS):**
- ❌ NO requiere autenticación SSO (MRS sí requiere)
- ✅ Acceso directo al portal sin login
- ✅ Promociones exclusivas Mastercard (2X1/Descuento)
- ✅ Dispersión de fondos condicional (según aerolínea)
- ✅ Pasarela específica (PlacetoPay - P2P)
- ✅ Emisión variable según 7 escenarios diferentes
- ✅ Control manual de aeropuertos permitidos (allowedAirports)

### COMPLEJIDAD QA:

**🔴 ALTA COMPLEJIDAD** debido a:
- 7 escenarios diferentes de pago y emisión
- Variables combinables: Promoción (2X1/Desc) + Fee Oculto (Sí/No) + Dispersión (Activa/Inactiva) + Proveedor (Edifact/Aggregator)
- Uso dual de tarjetas: TC Cliente + TC Corporativa
- Emisión mixta: TC Cliente, TC Corporativa, CASH, Combinaciones
- Configuración manual de aeropuertos (allowedAirports)

---

## ⚠️ CASOS EDGE CONOCIDOS

### PROMOCIONES:
- ⚠️ Validar comportamiento cuando promoción expira durante el proceso de reserva
- ⚠️ Confirmar manejo de cambio de tipo de promoción (2X1 → Descuento)
- ⚠️ Verificar límites de uso por usuario (si aplica)
- ⚠️ Validar que solo se aplique UNA promoción (no combinar 2X1 + Descuento)
- ⚠️ Confirmar mensaje claro al usuario sobre tipo de promoción aplicada

### DISPERSIÓN DE FONDOS:
- ⚠️ Validar rollback en caso de fallo de dispersión activa
- ⚠️ Confirmar trazabilidad completa de transacciones dispersadas
- ⚠️ **Verificar reembolsos con dispersión:** Reversión manual de fondos por operaciones
- ⚠️ Validar comportamiento si aerolínea cambia estado dispersión durante compra
- ⚠️ Confirmar que aggregators NUNCA ejecuten dispersión

### FEE OCULTO:
- ⚠️ Validar detección correcta de fee oculto en PQ
- ⚠️ Confirmar activación automática de TC corporativa cuando hay fee oculto
- ⚠️ Verificar que fee oculto NO se muestre al usuario en ningún momento
- ⚠️ Validar que el monto de TC corporativa cubra fee correctamente
- ⚠️ Confirmar manejo de fallo de TC corporativa (¿rollback?)

### EMISIÓN CON TC CORPORATIVA:
- ⚠️ Validar disponibilidad de TC corporativa antes de procesar
- ⚠️ Confirmar límite de crédito suficiente en TC corporativa
- ⚠️ Verificar manejo de rechazo de TC corporativa
- ⚠️ Validar que emisión CASH no proceda si dispersión está activa (excepto aggregators)

### PROVEEDORES:
- ⚠️ Validar que Edifact siempre evalúe dispersión y fee oculto
- ⚠️ Confirmar que aggregators (Sabre NDC, Netactica) siempre emitan en CASH
- ⚠️ Verificar que Thermeon solo opere para destinos en México
- ⚠️ Validar que Hertz opere globalmente
- ⚠️ Confirmar comportamiento cuando proveedor falla a mitad de transacción

### AEROPUERTOS RESTRINGIDOS:
- ⚠️ Validar que solo aeropuertos en `allowedAirports` aparezcan en búsqueda
- ⚠️ Confirmar bloqueo de emisión para aeropuertos NO permitidos
- ⚠️ Verificar mensaje de error claro si usuario intenta ruta no habilitada
- ⚠️ Validar actualización en tiempo real de collection `allowedAirports`

### COMBINACIONES COMPLEJAS:
- ⚠️ 2X1 + Fee Oculto + Dispersión Activa → 2 transacciones (TC Cliente + TC Corp)
- ⚠️ 2X1 + Fee Oculto + Dispersión Inactiva → 1 transacción (TC Cliente) + Emisión CASH
- ⚠️ Descuento + Sin Fee + Dispersión Activa → 1 transacción (TC Cliente) + Emisión Mixta
- ⚠️ Aggregator + Cualquier Promoción → Siempre 1 transacción + Emisión CASH

### CÁLCULOS DE PROMOCIONES:
- ⚠️ Validar que fee transaccional sea SIEMPRE $10,000 COP por pasajero
- ⚠️ Confirmar que en 2X1 el cliente pague solo 1 tiquete + fees de 2
- ⚠️ Verificar que descuento se aplique DESPUÉS de sumar 2 pasajeros
- ⚠️ Validar que fee oculto se incluya en cálculos internos pero NO se muestre al usuario
- ⚠️ Confirmar que fórmulas coincidan con Excel de referencia (4 escenarios)
- ⚠️ Verificar redondeos en montos finales (COP no tiene decimales)

---

## � REFERENCIAS

- 📚 [SHARED_QA_RULES.md](../SHARED_QA_RULES.md) - Fundamentos ISTQB y Azure DevOps
- 📋 [Mastercard - Priceless 2X1 (Wiki Azure)](https://dev.azure.com/ultragrouplaorg/ultragroupla/_wiki/wikis/Ultra%20Group%20Wiki/1141/Mastercard-Priceless-2X1)
- 📋 [PlacetoPay Integration Documentation]
- 📋 [Collection allowedAirports - MongoDB]- 📊 [Calcular 2x1 o descuento.xlsx (SharePoint)](https://smartlinksdev-my.sharepoint.com/:x:/r/personal/crubiog_ultragroupla_com/_layouts/15/Doc.aspx?sourcedoc=%7B64CBE898-E0F2-402B-88AB-1093813C7C49%7D&file=Calcular%202x1%20o%20descuento.xlsx) - Fórmulas de cálculo oficiales
---

## 📝 NOTAS TÉCNICAS

### IMPORTANTE:
- Portal en producción: **vuelaconoccidente.com**
- Ambientes separados para test, demo y producción
- Célula Skynet responsable del desarrollo y mantenimiento
- **ÚNICO modelo con 7 escenarios de pago/emisión diferentes**

### GLOSARIO DE TÉRMINOS PRICELESS:

- **PQ (Price Quote):** Cotización de precio de un tiquete
- **Base:** Tarifa base del tiquete (sin impuestos)
- **Total Taxes:** Suma de todos los impuestos del tiquete
- **equivalentAmount:** Suma de Base + Total Taxes (tarifa completa sin fees)
- **Fee Transaccional Fijo:** Cargo fijo por pasajero = $10,000 COP
- **Fee Oculto (Hidden Fee / HF):** Cargo adicional no visible al usuario
- **Taxes sin HF:** Total Taxes excluyendo Hidden Fee
- **TC Cliente:** Tarjeta de crédito del usuario final (vía PlacetoPay)
- **TC Corporativa:** Tarjeta de crédito empresarial de Ultragroup
- **Dispersión Activa:** Aerolínea acepta distribución automática de fondos
- **Edifact:** Proveedor directo de aerolíneas (Sabre)
- **Aggregator:** Proveedor intermediario (Sabre NDC, Netactica)
- **P2P (Peer to Peer):** Integración directa con pasarela PlacetoPay
- **allowedAirports:** Collection de MongoDB con aeropuertos habilitados
- **X2 Pax:** Cálculo del precio para 2 pasajeros
- **SUMA HF x2PAX:** Suma total incluyendo hidden fees de ambos pasajeros

### DECISIONES DE ARQUITECTURA:

**¿Por qué 7 escenarios diferentes?**
- Cada aerolínea tiene configuración propia de dispersión
- Fee oculto depende de tarifas negociadas con aerolíneas
- Promociones 2X1 vs Descuento requieren flujos diferentes
- Aggregators no soportan dispersión automática

**¿Por qué TC Corporativa?**
- Segundo tiquete en 2X1 con dispersión activa
- Cobertura de fees ocultos
- Pago posterior manual a aerolíneas (cuando no hay dispersión)

**¿Por qué allowedAirports manual?**
- Control total sobre rutas disponibles
- Evitar búsquedas en aeropuertos no negociados
- Prevenir emisiones en rutas sin cobertura

### PENDIENTE DOCUMENTAR:
- [x] Reglas de negocio detalladas de promociones Mastercard ✅
- [x] Escenarios de pago y emisión ✅
- [ ] Proceso de reembolsos por escenario
- [ ] Flujo de cancelaciones (¿qué pasa con TC Corporativa?)
- [ ] Límites de uso de promociones por usuario
- [ ] Criterios de elegibilidad Mastercard
- [ ] Proceso de actualización de allowedAirports

---

**Fecha de última actualización:** 3 de febrero de 2026  
**Responsable:** Célula Skynet  
**Estado:** ⚠️ En construcción
