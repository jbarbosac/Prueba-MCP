# 🚀 SANTANDER - MODELO B2B2C (CÉLULA ROCKET)

**Estado:** ⚠️ EN CONSTRUCCIÓN  
**Aliado:** Fidelity  
**Célula:** Rocket  
**Líder:** Cristian Garzon Sanchez  
**Fecha de creación:** 2026-01-23  

---

## 📋 INFORMACIÓN GENERAL

**Santander** es un modelo B2B2C (Business to Business to Consumer) donde:
- **B2B:** Santander (banco) es el cliente corporativo de PPM/Fidelity
- **2C:** Los usuarios finales son clientes del banco Santander que acceden al marketplace

Este modelo permite a los clientes del banco Santander canjear puntos de su programa de fidelización por productos de viajes.

---

## 🎯 PRODUCTOS DISPONIBLES

1. ✈️ **Vuelos**
2. 🚗 **Autos**
3. 🏨 **Hoteles**
4. 🎢 **Actividades**
5. 🎡 **Tickets Disney**

---

## 📁 ESTRUCTURA DE ARCHIVOS

```
.github/
├── shared/
│   └── Reglas Marketplace/
│       └── SANTANDER_COMMON_RULES.md      ← Reglas comunes y modelo de negocio
│
├── products/
│   └── B2B2C/
│       └── Fidelity/
│           └── Santander/
│               ├── SANT_VUELOS.md         ← Flujo E2E de Vuelos
│               ├── SANT_AUTOS.md          ← Flujo E2E de Autos
│               ├── SANT_HOTELES.md        ← Flujo E2E de Hoteles
│               ├── SANT_ACTIVIDADES.md    ← Flujo E2E de Actividades
│               └── SANT_DISNEY.md         ← Flujo E2E de Tickets Disney
│
└── agents/
    └── SANTANDER_QA_Assistant.agent.md    ← Agente QA especializado
```

---

## 🤖 AGENTE QA

**Nombre:** `SANTANDER_QA_Assistant`  
**Archivo:** `.github/agents/SANTANDER_QA_Assistant.agent.md`  
**Prefijo:** [SANT]  

### Capacidades del agente:

- ✅ Generar casos de prueba E2E para todos los productos
- ✅ Crear test cases en Azure DevOps automáticamente
- ✅ Validar criterios ISTQB
- ✅ Flujos desde login hasta validación en admin
- ✅ Soporte para modelo B2B2C

### Alcance:

- ✅ Solo Santander
- ❌ NO puede responder sobre otros modelos (PM, BGR, CME, etc.)
- ❌ NO hace comparaciones (eso es del QA_LEAD_Assistant)

---

## ⚠️ INFORMACIÓN PENDIENTE DE DEFINIR

Este modelo está **EN CONSTRUCCIÓN**. La siguiente información técnica debe ser completada antes de comenzar pruebas:

### 🔴 CRÍTICO - Definir antes de crear casos de prueba:

1. **Modelo de Pago:**
   - ¿100% Puntos Santander?
   - ¿Slider (Puntos + Tarjeta)?
   - ¿Mixto con proporciones fijas?

2. **Proceso de Emisión:**
   - ¿Automática (inmediata)?
   - ¿Manual (débito → pago → emisión)?
   - ¿Semiautomática?

3. **Proveedores por Producto:**
   - Vuelos: ¿AGGREGATOR NETACTICA / SABRE / SABRE EDIFACT?
   - Autos: ¿Sabre? ¿Qué empresas (Hertz, Dollar, Thrifty)?
   - Hoteles: ¿HotelBeds / Expedia / Otro?
   - Actividades: ¿HotelBeds / Viator / Otro?
   - Disney: ¿DerbySoft / OffLine / Otro?

4. **Pasarela de Pago (si aplica tarjeta):**
   - ¿Lightbox / PlacetoPay / Otra?

### 🟡 IMPORTANTE - Definir para pruebas efectivas:

5. **URLs de ambientes:**
   - URL de desarrollo
   - URL de testing/QA
   - URL de preprod
   - URL de producción

6. **Credenciales de Prueba:**
   - Usuario con saldo alto de puntos
   - Usuario con saldo bajo de puntos
   - Usuario sin puntos
   - Usuario VIP (si aplica)

7. **Azure DevOps:**
   - Organization
   - Project
   - Plan ID
   - Suite ID base

### 🟢 RECOMENDADO - Para completar documentación:

8. **Capturas de Pantalla:**
   - Capturas de cada paso del flujo por producto
   - Almacenar en `.github/imagenes/SANT/[producto]/`

9. **País y Moneda:**
   - ¿Qué país opera?
   - ¿Qué moneda usa?

---

## 📖 CÓMO USAR ESTA ARQUITECTURA

### Para crear casos de prueba:

1. **Selecciona el agente correcto:**
   - Activa: `SANTANDER_QA_Assistant`

2. **Define la información técnica necesaria:**
   - Revisa SANTANDER_COMMON_RULES.md
   - Identifica qué información falta
   - Complétala con el equipo de negocio/producto

3. **Solicita al agente:**
   ```
   "Crea un caso de vuelos para Santander"
   ```

4. **Proporciona contexto Azure DevOps:**
   - planId
   - suiteId
   - HU (opcional)

5. **El agente generará:**
   - Casos completos desde login
   - Validaciones B2B2C
   - Campos HTML (Descriptions, Considerations)
   - Creación automática en Azure DevOps

### Para consultas sobre Santander:

1. **Activa:** `SANTANDER_QA_Assistant`
2. **Pregunta:** "¿Cómo funciona el flujo de hoteles en Santander?"
3. **Respuesta:** El agente consultará SANT_HOTELES.md y te explicará

### Para comparaciones entre modelos:

1. **Activa:** `QA_LEAD_Assistant`
2. **Pregunta:** "¿Qué diferencia a Santander de Pichincha Miles?"
3. **Respuesta:** El QA_LEAD tiene visión global y puede comparar

---

## ✅ CHECKLIST DE ARQUITECTURA COMPLETA

### Documentación Base:
- ✅ SANTANDER_COMMON_RULES.md creado
- ✅ Estructura de carpetas creada
- ✅ 5 archivos de flujos E2E creados (Vuelos, Autos, Hoteles, Actividades, Disney)

### Agente QA:
- ✅ SANTANDER_QA_Assistant.agent.md creado
- ✅ Referencia a documentación configurada
- ✅ Validaciones de contexto implementadas
- ✅ Prefijo [SANT] configurado

### Integración Global:
- ✅ QA_LEAD_Assistant actualizado con info Santander
- ✅ Célula Rocket actualizada en organización
- ✅ Tabla comparativa incluye Santander
- ✅ Resumen de células actualizado

### Pendiente:
- ⚠️ Definir información técnica (modelo de pago, emisión, proveedores)
- ⚠️ Obtener URLs de ambientes
- ⚠️ Configurar credenciales de prueba
- ⚠️ Configurar Azure DevOps (planId, suiteId)
- ⚠️ Capturar pantallas de flujos
- ⚠️ Completar país y moneda

---

## 🔗 REFERENCIAS

### Documentación:
- 📋 [SANTANDER_COMMON_RULES.md](../shared/Reglas Marketplace/SANTANDER_COMMON_RULES.md)
- 🛫 [SANT_VUELOS.md](../products/B2B2C/Fidelity/Santander/SANT_VUELOS.md)
- 🚗 [SANT_AUTOS.md](../products/B2B2C/Fidelity/Santander/SANT_AUTOS.md)
- 🏨 [SANT_HOTELES.md](../products/B2B2C/Fidelity/Santander/SANT_HOTELES.md)
- 🎢 [SANT_ACTIVIDADES.md](../products/B2B2C/Fidelity/Santander/SANT_ACTIVIDADES.md)
- 🎡 [SANT_DISNEY.md](../products/B2B2C/Fidelity/Santander/SANT_DISNEY.md)

### Agente:
- 🤖 [SANTANDER_QA_Assistant.agent.md](../agents/SANTANDER_QA_Assistant.agent.md)

### Compartido:
- 📋 [SHARED_QA_RULES.md](../shared/SHARED_QA_RULES.md)
- 📋 [AGENT_CONTEXT_VALIDATION.md](../shared/AGENT_CONTEXT_VALIDATION.md)

---

## 👥 EQUIPO

**Célula Rocket:**
- **Líder:** Cristian Garzon Sanchez
- **QA Team:**
  - Diego Fernando Castellanos Vargas
  - Juan David Ceballos Cogollo
  - Emma Del Carmen Gonzalez Sanchez

---

## 📞 CONTACTO

Para preguntas sobre Santander:
- Líder de Célula: Cristian Garzon Sanchez
- Equipo QA: Célula Rocket

Para arquitectura global/comparaciones:
- Usar agente: QA_LEAD_Assistant

---

**Versión:** 1.0.0  
**Última actualización:** 2026-01-23  
**Próxima revisión:** Después de completar información técnica pendiente  
