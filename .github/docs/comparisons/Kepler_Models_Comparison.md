# 📊 Comparación Detallada: Modelos de Negocio Célula Kepler

> Documento de referencia para QA_LEAD_Assistant con análisis comparativo completo entre todos los modelos de la célula Kepler.

**Modelos activos:** PM, BGR, CME, CMP, PROM, CCOP (en configuración)

---

## 🎯 RESUMEN EJECUTIVO

| Aspecto         | PM                | BGR              | CME              | CMP              | PROM              | CCOP              |
| --------------- | ----------------- | ---------------- | ---------------- | ---------------- | ----------------- | ----------------- |
| **URL**         | pichinchamiles-ec | bgrmiles-ec      | clubmiles-ec     | [A definir]      | [A definir]       | [A definir]       |
| **País**        | Ecuador           | Ecuador          | Ecuador          | Perú             | [A definir]       | Colombia          |
| **Prefijo**     | [PM]              | [BGR]            | [CME]            | [CMP]            | [PROM]            | [CCOP]            |
| **Modelo**      | 100% Millas       | Slider           | Slider           | [A definir]      | [A definir]       | [A definir]       |
| **Fee Vuelos**  | Sí                | No               | No               | [A definir]      | [A definir]       | [A definir]       |
| **Emisión**     | Automática        | Mixta            | Mixta            | [A definir]      | [A definir]       | [A definir]       |
| **Complejidad** | Media             | Alta             | Alta             | [A definir]      | [A definir]       | [A definir]       |
| **Estado**      | ✅ Activo         | ✅ Activo        | ✅ Activo        | ✅ Activo        | ✅ Activo         | 🔄 Configurando   |
| **Agente**      | PM_QA_Assistant   | BGR_QA_Assistant | CME_QA_Assistant | CMP_QA_Assistant | PROM_QA_Assistant | CCOP_QA_Assistant |

---

## 💰 MODELO DE NEGOCIO COMPARADO

### **1. Pichincha Miles (PM) - Ecuador**

**VUELOS:**

```
Producto = 100% MILLAS
Fee de procesamiento = TARJETA DE CRÉDITO (lightbox)
Emisión = AUTOMÁTICA
```

**OTROS PRODUCTOS (Hoteles, Autos, Actividades, Disney):**

```
Producto = 100% MILLAS
Sin fee, sin tarjeta
Emisión = AUTOMÁTICA
```

**Características:**

- ✅ Modelo simple y predecible
- ✅ Emisión siempre automática
- ✅ Solo vuelos requieren tarjeta (fee)
- ✅ Sin proceso manual de emisión

---

### **2. BGR Miles (BGR) - Ecuador**

**TRES MODALIDADES DE PAGO:**

```
1. Solo Millas (100% millas)
   → Pago: 100% MILLAS
   → Emisión: AUTOMÁTICA
   → Tarjeta: NO requerida

2. Millas + Plata (Pago Mixto)
   → Pago: MILLAS (slider) + PLATA (tarjeta en checkout)
   → Emisión: SEMIAUTOMÁTICA (manual)
   → Tarjeta: REQUERIDA
   → Proceso admin: Debitar millas → Emitir en cash

3. Solo Plata (0% millas)
   → ❌ NO PERMITIDO (slider tiene mínimo obligatorio)
```

**Mínimos por Slider:**

- Vuelos: 2875 millas mínimo
- Otros: 20% del total de millas

**Características:**

- ⚠️ Modelo complejo con múltiples flujos
- ⚠️ Emisión mixta (automática + manual)
- ⚠️ Requiere validación continua del slider
- ⚠️ Proceso manual para pago mixto

---

## 🏗️ COMPARACIÓN DE ARQUITECTURA

### **Proveedores por Producto**

| Producto        | PM                                                        | BGR                                                       | Coinciden             |
| --------------- | --------------------------------------------------------- | --------------------------------------------------------- | --------------------- |
| **Vuelos**      | AGGREGATOR NETACTICA<br>AGGREGATOR SABRE<br>SABRE EDIFACT | AGGREGATOR NETACTICA<br>AGGREGATOR SABRE<br>SABRE EDIFACT | ✅ Mismos proveedores |
| **Autos**       | Sabre → Hertz, Dollar, Thrifty                            | Sabre → Hertz, Dollar, Thrifty                            | ✅ Mismos proveedores |
| **Hoteles**     | HotelBeds                                                 | HotelBeds                                                 | ✅ Mismo proveedor    |
| **Actividades** | HotelBeds                                                 | HotelBeds                                                 | ✅ Mismo proveedor    |
| **Disney**      | DerbySoft                                                 | OffLine                                                   | ❌ **DIFERENTES**     |

### **Tecnologías por Producto**

| Producto        | PM      | BGR               |
| --------------- | ------- | ----------------- |
| **Vuelos**      | Angular | (No especificado) |
| **Autos**       | Meteor  | (No especificado) |
| **Hoteles**     | Angular | (No especificado) |
| **Actividades** | Angular | (No especificado) |
| **Disney**      | React   | (No especificado) |

---

## 🔄 FLUJOS DE EMISIÓN COMPARADOS

### **Pichincha Miles (PM)**

**SIEMPRE AUTOMÁTICO:**

```
Usuario completa checkout
       ↓
Sistema procesa pago (100% millas)
       ↓
Si hay fee (vuelos): Lightbox tarjeta
       ↓
Estado final: EMITIDA
```

**Características:**

- ✅ Sin intervención manual
- ✅ Flujo lineal y predecible
- ✅ Menos estados de reserva

---

### **BGR Miles (BGR)**

**EMISIÓN AUTOMÁTICA (100% millas):**

```
Usuario completa checkout con slider al 100%
       ↓
Sistema procesa pago (100% millas)
       ↓
Estado final: EMITIDA
```

**EMISIÓN MANUAL (Millas + Plata):**

```
Usuario completa checkout con slider < 100%
       ↓
Usuario ingresa tarjeta en checkout
       ↓
Estado: PENDIENTE DÉBITO
       ↓
Admin: Ingresar a panel BGR
       ↓
Admin: Buscar y abrir reserva
       ↓
Admin: Debitar millas manualmente
       ↓
Estado: PENDIENTE PAGO CASH
       ↓
Admin: Emitir en cash (usar tarjeta ingresada)
       ↓
Estado final: EMITIDA
```

**Características:**

- ⚠️ Requiere intervención manual para pago mixto
- ⚠️ Más estados de reserva
- ⚠️ Mayor complejidad operativa
- ⚠️ Requiere acceso a admin BGR

---

### **3. Club Miles Ecuador (CME) - Ecuador**

**Estado:** ✅ Activo  
**Documentación:** [CME_COMMON_RULES.md](../../shared/Kepler/CME_COMMON_RULES.md)

**Características principales:**

- Modelo similar a BGR (Slider)
- [Detalles a completar según documentación CME]

---

### **4. Club Millas Perú (CMP) - Perú**

**Estado:** ✅ Activo  
**Documentación:** Pendiente crear CMP_COMMON_RULES.md

**Características principales:**

- [A definir según documentación CMP]

---

### **5. Promerica Rewards (PROM)**

**Estado:** ✅ Activo  
**Documentación:** [PROM_COMMON_RULES.md](../../shared/Reglas Marketplace/PROM_COMMON_RULES.md)

**Características principales:**

- [Detalles a completar según documentación PROM]

---

### **6. Consolidación COP (CCOP) - Colombia** 🆕

**Estado:** 🔄 EN CONFIGURACIÓN INICIAL  
**Documentación:** [CCOP_COMMON_RULES.md](../../shared/Kepler/CCOP_COMMON_RULES.md)  
**Guía de Setup:** [CCOP_SETUP_GUIDE.md](../CCOP_SETUP_GUIDE.md)

**Características principales:**

- ⏳ URL: [A definir]
- ⏳ Modelo de negocio: [A definir]
- ⏳ Tipo de emisión: [A definir]
- ⏳ Productos: [A definir]
- ⏳ Proveedores: [A definir]

**Pendientes de configuración:**

- [ ] Definir URL del portal
- [ ] Definir productos disponibles
- [ ] Definir modelo de negocio
- [ ] Definir tipo de emisión
- [ ] Definir proveedores
- [ ] Crear documentación específica por producto
- [ ] Configurar Azure DevOps

**Ver:** [CCOP_SETUP_GUIDE.md](../CCOP_SETUP_GUIDE.md) para checklist completo.

---

## ✅ VALIDACIONES COMPARADAS

### **Validaciones COMUNES (ambos portales)**

✅ Integridad de datos en todas las pantallas  
✅ Validación de campos obligatorios  
✅ Links funcionales (T&C, tratamiento de datos)  
✅ Estados de reserva correctos en admin  
✅ Confirmación del proveedor  
✅ Cálculo correcto de millas

### **Validaciones ESPECÍFICAS PM**

✅ Fee aplicado solo a vuelos  
✅ Lightbox de tarjeta funcional (vuelos)  
✅ Emisión automática inmediata  
✅ Sin validación de slider (no existe)

### **Validaciones ESPECÍFICAS BGR**

✅ Slider funcional y dentro de límites  
✅ Cálculo dinámico millas/plata según slider  
✅ Validación de mínimo por slider  
✅ Saldo de millas suficiente para slider  
✅ Proceso manual completo para pago mixto  
✅ Estado PENDIENTE vs EMITIDA según modalidad  
✅ Admin BGR accesible y funcional  
✅ Débito de millas correcto  
✅ Emisión en cash correcta

---

## 🎯 ESCENARIOS DE PRUEBA COMPARADOS

### **Pichincha Miles (PM)**

**Casos principales:**

1. Vuelos con fee (lightbox tarjeta)
2. Hoteles sin fee (solo millas)
3. Autos sin fee (solo millas)
4. Actividades sin fee (solo millas)
5. Disney sin fee (solo millas)

**Complejidad:** Media  
**Variantes típicas:** 5-8 casos por producto

---

### **BGR Miles (BGR)**

**Casos principales:**

1. Producto con 100% millas (automático)
2. Producto con millas + plata (manual)
3. Validación de mínimo slider
4. Validación de saldo insuficiente
5. Proceso manual completo en admin

**Complejidad:** Alta  
**Variantes típicas:** 10-15 casos por producto

---

## 📊 MÉTRICAS Y COBERTURA

### **Esfuerzo de Testing Estimado**

| Portal   | Casos por Producto | Total Productos | Total Casos Estimado | Estado    |
| -------- | ------------------ | --------------- | -------------------- | --------- |
| **PM**   | 5-8                | 5               | 25-40 casos          | ✅ Activo |
| **BGR**  | 10-15              | 5               | 50-75 casos          | ✅ Activo |
| **CME**  | 10-15              | [A definir]     | [A estimar]          | ✅ Activo |
| **CMP**  | [A definir]        | [A definir]     | [A estimar]          | ✅ Activo |
| **PROM** | [A definir]        | [A definir]     | [A estimar]          | ✅ Activo |
| **CCOP** | [A definir]        | [A definir]     | [A estimar]          | 🔄 Config |

### **Áreas de Mayor Riesgo**

**PM:**

- 🟡 Lightbox de tarjeta (vuelos)
- 🟡 Integración con proveedores
- 🟢 Emisión automática (baja complejidad)

**BGR:**

- 🔴 Slider y cálculo dinámico
- 🔴 Proceso manual de emisión
- 🔴 Estados de reserva complejos
- 🟡 Validación de saldos
- 🟡 Admin BGR funcional

---

## 🎓 GUÍA DE DECISIÓN PARA QA

### **¿Qué agente usar según el portal?**

**PM_QA_Assistant:**
✅ URL contiene `pichinchamiles-ec`  
✅ Modelo 100% millas fijo  
✅ Emisión siempre automática  
✅ Fee solo en vuelos  
✅ Sin proceso manual

**BGR_QA_Assistant:**
✅ URL contiene `bgrmiles-ec`  
✅ Modelo con slider millas/plata  
✅ Emisión mixta (automática + manual)  
✅ Sin fee  
✅ Requiere validación de proceso manual

**CME_QA_Assistant:**
✅ URL contiene `clubmiles-ec`  
✅ Ecuador  
✅ [Características específicas según CME_COMMON_RULES.md]

**CMP_QA_Assistant:**
✅ Club Millas Perú  
✅ Perú  
✅ [Características específicas a definir]

**PROM_QA_Assistant:**
✅ Promerica Rewards  
✅ [Características específicas según PROM_COMMON_RULES.md]

**CCOP_QA_Assistant:**
✅ Consolidación COP  
✅ Colombia  
✅ Prefijo [CCOP]  
⚠️ Estado: En configuración inicial

**QA_LEAD_Assistant:**
✅ Preguntas comparativas entre CUALQUIER modelo  
✅ Análisis de cobertura global  
✅ Decisiones estratégicas de testing  
✅ Reportes consolidados  
✅ Orquestación de creación de casos multi-portal

---

## 🔄 FLUJO DE DELEGACIÓN

### **Desde QA_LEAD_Assistant**

```
Usuario: "¿Cuál es la diferencia entre emisión PM y BGR?"
   ↓
QA_LEAD: Responde con tabla comparativa (este documento)
```

```
Usuario: "Genera 5 casos de vuelos para PM"
   ↓
QA_LEAD: "Para generar casos específicos de PM,
          debes usar el agente PM_QA_Assistant.
          ¿Quieres que te prepare el contexto?"
```

```
Usuario: "¿Cuántos proveedores de vuelos tenemos en total?"
   ↓
QA_LEAD: "Ambos portales comparten los mismos 3 proveedores:
          - AGGREGATOR NETACTICA
          - AGGREGATOR SABRE
          - SABRE EDIFACT"
```

---

## 📌 TÉRMINOS CLAVE

**Slider:** Control deslizante en BGR para ajustar proporción Millas/Plata  
**Fee:** Cargo por servicio (solo vuelos PM, procesado con tarjeta)  
**Emisión automática:** Sistema emite ticket sin intervención humana  
**Emisión manual:** Requiere débito manual de millas y emisión en cash  
**Débito de millas:** Acción manual en admin BGR para descontar millas  
**Emitir en cash:** Procesar pago con tarjeta en admin BGR  
**Lightbox:** Ventana modal para ingresar datos de tarjeta  
**Agregador:** Proveedor que consolida múltiples fuentes

---

## 📖 REFERENCIAS

**Reglas compartidas:**

- [SHARED_QA_RULES.md](../../shared/SHARED_QA_RULES.md) - Fundamentos comunes

**Reglas específicas por modelo:**

- [PM_COMMON_RULES.md](../../shared/Kepler/PM_COMMON_RULES.md) - Pichincha Miles
- [BGR_COMMON_RULES.md](../../shared/Kepler/BGR_COMMON_RULES.md) - BGR Miles
- [CME_COMMON_RULES.md](../../shared/Kepler/CME_COMMON_RULES.md) - Club Miles Ecuador
- CMP_COMMON_RULES.md - Club Millas Perú (pendiente crear)
- [PROM_COMMON_RULES.md](../../shared/Reglas Marketplace/PROM_COMMON_RULES.md) - Promerica Rewards
- [CCOP_COMMON_RULES.md](../../shared/Kepler/CCOP_COMMON_RULES.md) - Consolidación COP 🆕

**Guías y documentación adicional:**

- [GLOSSARY.md](../GLOSSARY.md) - Glosario completo
- [ARCHITECTURE.md](../ARCHITECTURE.md) - Decisiones arquitecturales
- [CCOP_SETUP_GUIDE.md](../CCOP_SETUP_GUIDE.md) - Guía configuración CCOP 🆕

---

**Última actualización:** 2026-01-22  
**Versión:** 2.0 (incluye CCOP)  
**Mantenido por:** Sistema de Agentes QA - Célula Kepler
