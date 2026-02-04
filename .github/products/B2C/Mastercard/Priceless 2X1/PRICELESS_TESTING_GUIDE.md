# 🧪 **GUÍA DE TESTING - MASTERCARD PRICELESS 2X1**

## 📋 **INFORMACIÓN GENERAL**

**Cliente:** Mastercard (Sub-proyecto Priceless 2X1)  
**País:** Colombia  
**Moneda:** COP (Pesos Colombianos)  
**Célula:** Skynet  
**Modelo:** B2C - 100% Dinero con promociones 2X1 o Descuento  
**Agente QA:** PRICELESS_QA_Assistant  

---

## 🎯 **ESTRATEGIA DE TESTING**

### **Pirámide de Testing:**

```
                    ▲
                   ╱ ╲
                  ╱ E2E╲           10% - Testing Manual (E2E crítico)
                 ╱ UI   ╲
                ╱────────╲
               ╱          ╲
              ╱ Integration╲      30% - Testing de Integración
             ╱              ╲
            ╱────────────────╲
           ╱                  ╲
          ╱   Unit Tests       ╲   60% - Unit Testing
         ╱                      ╲
        ╱────────────────────────╲
```

---

## 🔍 **NIVELES DE TESTING**

### **1️⃣ Unit Testing (Backend)**

**Responsable:** Equipo Backend (Angelo Nieto)  
**Cobertura esperada:** 80%+  
**Framework:** Jest  

**Áreas clave:**
- Cálculo de promociones (2X1 vs Descuento)
- Validación de fee transaccional (Vuelos: $10,000 COP/PAX)
- Validación de markup (Hoteles/Autos: $10,000 COP/unidad)
- Lógica de dispersión (7 escenarios Vuelos)
- Validación allowedAirports
- Cálculo de fee oculto

**Ejemplo:**
```javascript
describe('Promoción 2X1 - Vuelos', () => {
  test('Debe calcular correctamente precio con 2X1', () => {
    const base = 400000;  // COP
    const taxes = 0;
    const passengers = 2;
    const feeTransaccional = 10000;
    
    const total = calculatePromo2x1(base, taxes, passengers);
    
    expect(total).toBe(820000);  // (400k + 0) × 1 PAX + (10k × 2 PAX)
  });
});
```

---

### **2️⃣ Integration Testing**

**Responsable:** Equipo Backend + QA  
**Cobertura esperada:** 70%+  
**Framework:** Jest + Supertest  

**Áreas clave:**
- Integración con SABRE (Vuelos, Hoteles)
- Integración con Netatica (Vuelos)
- Integración con SABRE NDC (Vuelos)
- Integración con Hertz (Autos)
- Integración con Thermeon (Autos)
- Integración con PlacetoPay (P2P)
- Integración con MongoDB (allowedAirports, dispersion_config)

**Ejemplo:**
```javascript
describe('PlacetoPay Integration - 2X1', () => {
  test('Debe procesar pago con dispersión ACTIVA', async () => {
    const paymentData = {
      amount: 820000,
      reference: 'PRICELESS-2X1-TEST-001',
      dispersion: true,
      tcCliente: '5121220000000000',
      tcCorporativa: '[configurada]'
    };
    
    const response = await placetoPay.process(paymentData);
    
    expect(response.status).toBe('APPROVED');
    expect(response.dispersions).toHaveLength(1);
  });
});
```

---

### **3️⃣ E2E Testing (Manual + Automatizado)**

**Responsable:** Equipo QA (Carlos Alberto Rubio Gallego)  
**Herramienta manual:** Azure DevOps Test Plans  
**Herramienta automatizada:** Playwright / Cypress (recomendado)  

**Áreas clave:**
- Flujos completos por producto (Vuelos, Hoteles, Autos)
- 7 escenarios de Vuelos (combinaciones promoción/dispersión/fee)
- Modelo simplificado Hoteles/Autos
- Validación de cálculos visibles al usuario
- Proceso de pago PlacetoPay
- Cancelaciones y reversos manuales

---

## 🛫 **TESTING VUELOS (7 ESCENARIOS)**

### **Escenario 1: 2X1 SIN fee oculto + Dispersión ACTIVA**

**Precondiciones:**
- Aerolínea con dispersión ACTIVA (ej: Avianca)
- Aeropuertos en allowedAirports
- Promoción 2X1 habilitada

**Datos de prueba:**
```yaml
Origen: BOG
Destino: MDE
Tipo: Ida y vuelta
Pasajeros: 2 adultos
Base: $400,000 COP
Taxes: $0
Fee Transaccional: $10,000 × 2 = $20,000
Total esperado: $820,000 COP
```

**Validaciones críticas:**
- ✅ Precio visible: $820,000 (no $1,620,000)
- ✅ Fee transaccional: $20,000 (visible)
- ✅ Pago 1: TC Cliente $410,000 (1 PQ + Fee)
- ✅ Pago 2: TC Corporativa $400,000 (1 PQ sin fee)
- ✅ Emisión: 1er tiquete TC Cliente, 2do tiquete TC Corporativa
- ✅ Sin fee oculto

**Caso de prueba:** [Priceless] Vuelos - Ida y vuelta - 2X1 - SABRE - Dispersión Activa

---

### **Escenario 2: 2X1 SIN fee oculto + Dispersión INACTIVA**

**Precondiciones:**
- Aerolínea con dispersión INACTIVA (ej: LATAM)
- Aeropuertos en allowedAirports
- Promoción 2X1 habilitada

**Datos de prueba:**
```yaml
Origen: BOG
Destino: CTG
Tipo: Ida y vuelta
Pasajeros: 2 adultos
Base: $350,000 COP
Taxes: $0
Total esperado: $720,000 COP
```

**Validaciones críticas:**
- ✅ Precio visible: $720,000
- ✅ Fee transaccional: $20,000 (visible)
- ✅ Pago: TC Cliente $720,000 (total)
- ✅ Emisión: 2 tiquetes CASH
- ✅ Sin dispersión
- ✅ Sin fee oculto

**Caso de prueba:** [Priceless] Vuelos - Ida y vuelta - 2X1 - SABRE - Dispersión Inactiva

---

### **Escenario 3: 2X1/Desc CON fee oculto + Dispersión ACTIVA**

**Precondiciones:**
- Aerolínea con dispersión ACTIVA
- Fee oculto configurado
- Promoción 2X1 o Descuento habilitada

**Datos de prueba:**
```yaml
Origen: MDE
Destino: BOG
Tipo: Solo ida
Pasajeros: 2 adultos
Base (sin fee oculto): $400,000 COP
Fee oculto: $50,000 COP
Total visible: $820,000 COP
Total real (con fee oculto): $870,000 COP
```

**Validaciones críticas:**
- ✅ Precio visible: $820,000 (SIN fee oculto)
- ✅ Fee oculto: $50,000 (NO visible al usuario)
- ✅ Pago 1: TC Cliente $820,000 (total visible)
- ✅ Pago 2: TC Corporativa $800,000 (2 PQ sin fee transaccional - fee oculto cubierto por corporativa)
- ✅ Emisión: 2 tiquetes TC Corporativa
- ✅ Fee oculto NO mostrado en UI

**Caso de prueba:** [Priceless] Vuelos - Solo ida - 2X1 - SABRE - Fee Oculto + Dispersión

---

### **Escenario 4: 2X1/Desc CON fee oculto + Dispersión INACTIVA**

**Precondiciones:**
- Aerolínea con dispersión INACTIVA
- Fee oculto configurado
- Promoción habilitada

**Datos de prueba:**
```yaml
Origen: CLO
Destino: BOG
Tipo: Ida y vuelta
Pasajeros: 2 adultos
Total visible: $820,000 COP
Fee oculto: $50,000 COP
```

**Validaciones críticas:**
- ✅ Precio visible: $820,000 (sin fee oculto)
- ✅ Pago: TC Cliente $820,000 (total visible)
- ✅ Emisión: 2 tiquetes CASH
- ✅ Fee oculto cubierto internamente
- ✅ Sin dispersión

**Caso de prueba:** [Priceless] Vuelos - Ida y vuelta - 2X1 - Fee Oculto sin Dispersión

---

### **Escenario 5: Descuento SIN fee oculto + Dispersión ACTIVA**

**Precondiciones:**
- Aerolínea con dispersión ACTIVA
- Promoción Descuento habilitada (ej: 30%)
- Sin fee oculto

**Datos de prueba:**
```yaml
Origen: BOG
Destino: MDE
Tipo: Ida y vuelta
Pasajeros: 2 adultos
Base por PAX: $400,000 COP
Total sin descuento: $800,000 + $20,000 fee = $820,000
Descuento: 30% sobre base = $240,000
Total esperado: $580,000 + $20,000 = $600,000 COP
```

**Validaciones críticas:**
- ✅ Descuento visible: $240,000
- ✅ Total con descuento: $600,000
- ✅ Pago: TC Cliente $600,000 (con dispersión parcial)
- ✅ Emisión: Mixta (1er tiquete TC Cliente, 2do tiquete CASH + TC Cliente)
- ✅ Descuento claramente mostrado

**Caso de prueba:** [Priceless] Vuelos - Ida y vuelta - Descuento 30% - Dispersión Activa

---

### **Escenario 6: Descuento SIN fee oculto + Dispersión INACTIVA**

**Precondiciones:**
- Aerolínea con dispersión INACTIVA
- Promoción Descuento habilitada
- Sin fee oculto

**Datos de prueba:**
```yaml
Origen: CTG
Destino: CLO
Tipo: Solo ida
Pasajeros: 2 adultos
Total sin descuento: $820,000
Descuento: $300,000
Total esperado: $520,000 + $20,000 fee = $540,000
```

**Validaciones críticas:**
- ✅ Descuento visible: $300,000
- ✅ Total: $540,000
- ✅ Pago: TC Cliente $540,000
- ✅ Emisión: 2 tiquetes CASH
- ✅ Sin dispersión

**Caso de prueba:** [Priceless] Vuelos - Solo ida - Descuento $300k - Sin Dispersión

---

### **Escenario 7: Aggregator (Netatica o SABRE NDC)**

**Precondiciones:**
- Búsqueda retorna resultados de Aggregator
- Promoción aplicable (2X1 o Descuento)

**Datos de prueba:**
```yaml
Origen: BOG
Destino: MDE
Proveedor: AGGREGATOR NETATICA
Pasajeros: 2 adultos
Total: $820,000 (con promoción 2X1)
```

**Validaciones críticas:**
- ✅ Promoción aplicada correctamente
- ✅ Pago: TC Cliente $820,000 (total único)
- ✅ Emisión: 2 tiquetes CASH automático
- ✅ Sin dispersión (Aggregator no soporta)
- ✅ Sin fee oculto

**Caso de prueba:** [Priceless] Vuelos - Ida y vuelta - 2X1 - Netactica

---

## 🏨 **TESTING HOTELES (MODELO SIMPLIFICADO)**

### **Flujo Único:**

**Precondiciones:**
- Promoción 2X1 o Descuento habilitada
- Markup configurado: $10,000 COP/noche

**Datos de prueba:**
```yaml
Ciudad: Cartagena
Check-in: +7 días
Check-out: +9 días
Noches: 2
Habitaciones: 1
Huéspedes: 2 adultos
Precio base (SABRE): $200,000/noche × 2 = $400,000
Promoción: 2X1
Markup: $10,000 × 2 noches = $20,000
Total esperado: $200,000 + $20,000 = $220,000 (paga 1 noche + markup de 2)
```

**Validaciones críticas:**
- ✅ Precio visible: $220,000
- ✅ Markup: $20,000 (visible como "Costo de servicio")
- ✅ Promoción 2X1 aplicada (paga 1 noche, recibe 2)
- ✅ Pago: TC Cliente $220,000 (directo a Ultragroup)
- ✅ Emisión: CASH automática
- ✅ Sin dispersión
- ✅ Sin fee oculto

**Caso de prueba:** [Priceless] Hoteles - 2 noches - 2X1 - SABRE

---

### **Testing Descuento Hoteles:**

**Datos de prueba:**
```yaml
Ciudad: Bogotá
Noches: 3
Precio base: $150,000/noche × 3 = $450,000
Descuento: 20% = $90,000
Markup: $10,000 × 3 = $30,000
Total esperado: ($450,000 - $90,000) + $30,000 = $390,000
```

**Validaciones críticas:**
- ✅ Descuento visible: $90,000
- ✅ Markup visible: $30,000
- ✅ Total: $390,000
- ✅ Pago: TC Cliente $390,000
- ✅ Emisión: CASH automática

**Caso de prueba:** [Priceless] Hoteles - 3 noches - Descuento 20% - SABRE

---

## 🚗 **TESTING AUTOS (MODELO SIMPLIFICADO)**

### **Flujo Hertz (Colombia):**

**Precondiciones:**
- Promoción 2X1 o Descuento habilitada
- Markup configurado: $10,000 COP/día

**Datos de prueba:**
```yaml
Ciudad: Bogotá
Recogida: +7 días
Devolución: +12 días
Días: 5
Categoría: Compacto
Proveedor: Hertz
Precio base: $80,000/día × 5 = $400,000
Promoción: 2X1 (paga 3 días, recibe 5)
Markup: $10,000 × 5 días = $50,000
Total esperado: ($80,000 × 3) + $50,000 = $290,000
```

**Validaciones críticas:**
- ✅ Precio visible: $290,000
- ✅ Markup: $50,000 (visible)
- ✅ Promoción 2X1 aplicada correctamente
- ✅ Pago: TC Cliente $290,000 (directo a Ultragroup)
- ✅ Emisión: CASH automática
- ✅ Sin dispersión
- ✅ Sin fee oculto

**Caso de prueba:** [Priceless] Autos - 5 días - 2X1 - Hertz

---

### **Flujo Thermeon (México):**

**Datos de prueba:**
```yaml
Ciudad: Cancún (México)
Días: 7
Precio base: $100,000/día × 7 = $700,000 COP (convertido)
Descuento: $200,000
Markup: $10,000 × 7 = $70,000
Total esperado: ($700,000 - $200,000) + $70,000 = $570,000
```

**Validaciones críticas:**
- ✅ Descuento visible: $200,000
- ✅ Markup visible: $70,000
- ✅ Total: $570,000
- ✅ Pago: TC Cliente $570,000 (procesado en COP)
- ✅ Emisión: CASH automática

**Caso de prueba:** [Priceless] Autos - 7 días - Descuento $200k - Thermeon México

---

## 🚫 **TESTING CANCELACIONES**

### **Flujo de Cancelación:**

**Precondiciones:**
- Reserva confirmada con pago aprobado
- Estado inicial: CONFIRMED

**Pasos:**
1. Usuario solicita cancelación
2. Sistema cambia estado a CANCELLED automáticamente
3. Equipo de operaciones ejecuta reverso manual
4. Validar reverso procesado correctamente

**Validaciones críticas:**
- ✅ Estado cambia a CANCELLED inmediatamente
- ⚠️ Reverso NO automático (proceso manual)
- ✅ Reverso procesado en PlacetoPay (validar manualmente con operaciones)
- ✅ Vuelos: Reverso TC Cliente + TC Corporativa (si aplica)
- ✅ Hoteles/Autos: Reverso TC Cliente únicamente
- ✅ Notificación enviada al usuario

**Caso de prueba:** [Priceless] Vuelos - Cancelación con reverso manual (Escenario 1)

---

## 📊 **MATRIZ DE TESTING**

### **Vuelos:**

| Escenario | Promoción | Dispersión | Fee Oculto | Proveedor | Casos | Estado |
|-----------|-----------|------------|------------|-----------|-------|--------|
| 1 | 2X1 | ACTIVA | NO | SABRE | 2 | ✅ Crítico |
| 2 | 2X1 | INACTIVA | NO | SABRE | 2 | ✅ Crítico |
| 3 | 2X1/Desc | ACTIVA | SÍ | SABRE | 2 | ✅ Crítico |
| 4 | 2X1/Desc | INACTIVA | SÍ | SABRE | 1 | ⚠️ Alta |
| 5 | Descuento | ACTIVA | NO | SABRE | 2 | ✅ Crítico |
| 6 | Descuento | INACTIVA | NO | SABRE | 1 | ⚠️ Alta |
| 7 | 2X1/Desc | N/A | NO | Aggregator | 2 | ✅ Crítico |

**Total casos críticos Vuelos:** 12

---

### **Hoteles:**

| Flujo | Promoción | Proveedor | Casos | Estado |
|-------|-----------|-----------|-------|--------|
| Estándar | 2X1 | SABRE | 2 | ✅ Crítico |
| Estándar | Descuento | SABRE | 2 | ✅ Crítico |

**Total casos críticos Hoteles:** 4

---

### **Autos:**

| Flujo | Promoción | Proveedor | Casos | Estado |
|-------|-----------|-----------|-------|--------|
| Hertz | 2X1 | Hertz | 2 | ✅ Crítico |
| Hertz | Descuento | Hertz | 1 | ⚠️ Alta |
| Thermeon | 2X1 | Thermeon | 1 | ⚠️ Alta |
| Thermeon | Descuento | Thermeon | 2 | ✅ Crítico |

**Total casos críticos Autos:** 6

---

### **TOTAL CASOS CRÍTICOS E2E:** 22

---

## 🔄 **TESTING DE REGRESIÓN**

### **Checklist Pre-Release:**

**Vuelos:**
- [ ] Escenario 1 (2X1 + Dispersión ACTIVA)
- [ ] Escenario 2 (2X1 + Dispersión INACTIVA)
- [ ] Escenario 3 (Fee Oculto + Dispersión ACTIVA)
- [ ] Escenario 7 (Aggregator Netatica)
- [ ] Validar allowedAirports
- [ ] Validar cálculo fee transaccional
- [ ] Cancelación + reverso manual

**Hoteles:**
- [ ] Promoción 2X1
- [ ] Promoción Descuento
- [ ] Validar Markup visible
- [ ] Pago directo Ultragroup
- [ ] Emisión CASH automática
- [ ] Cancelación + reverso manual

**Autos:**
- [ ] Hertz - Promoción 2X1
- [ ] Thermeon - Descuento
- [ ] Validar Markup visible
- [ ] Pago directo Ultragroup
- [ ] Emisión CASH automática
- [ ] Cancelación + reverso manual

**PlacetoPay:**
- [ ] Pago único (TC Cliente)
- [ ] Pago dual (TC Cliente + TC Corporativa)
- [ ] Dispersión ACTIVA
- [ ] Reverso manual (coordinado con operaciones)

---

## 🛠️ **HERRAMIENTAS DE TESTING**

### **Manuales:**
- Azure DevOps Test Plans
- Postman (API testing)
- PlacetoPay Sandbox (tarjetas de prueba)

### **Automatizadas (Recomendadas):**
- Playwright (E2E)
- Cypress (E2E)
- Jest (Unit + Integration)
- Supertest (API)

---

## 📞 **CONTACTOS**

| Rol | Nombre | Email | Responsabilidad |
|-----|--------|-------|-----------------|
| **QA Lead** | Carlos Alberto Rubio Gallego | crubiog@ultragroupla.com | Testing E2E, Test Plans |
| **Backend Lead** | Angelo Nieto | anieto@ultragroupla.com | Unit Tests, Integration Tests |
| **Frontend Lead** | Sergio Mauricio Pimiento Niño | spimiento@ultragroupla.com | UI Tests |
| **PO** | Juan Bernardo Arias Hurtado | jhurtado@ultragroupla.com | Criterios de aceptación |

---

## 📚 **REFERENCIAS**

- 📋 [PRICELESS_COMMON_RULES.md](../../../shared/Reglas Marketplace/PRICELESS_COMMON_RULES.md) - Reglas de negocio
- 📋 [README.MD](README.MD) - Documentación principal
- 🛫 [PRICELESS_VUELOS.md](PRICELESS_VUELOS.md) - Casos de prueba Vuelos
- 🏨 [PRICELESS_HOTELES.md](PRICELESS_HOTELES.md) - Casos de prueba Hoteles
- 🚗 [PRICELESS_AUTOS.md](PRICELESS_AUTOS.md) - Casos de prueba Autos
- 📋 [PRICELESS_ENVIRONMENTS.md](PRICELESS_ENVIRONMENTS.md) - Entornos y datos de prueba
- 📋 [PRICELESS_INTEGRATIONS.md](PRICELESS_INTEGRATIONS.md) - Integraciones técnicas

---

**Última actualización:** Enero 2025  
**Responsable:** Carlos Alberto Rubio Gallego (QA Mastercard)  
**Agente QA:** PRICELESS_QA_Assistant  
