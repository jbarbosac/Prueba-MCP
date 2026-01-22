# 🚀 GUÍA DE CONFIGURACIÓN: Consolidación COP (CCOP)

Este documento guía la configuración inicial completa del modelo de negocio **Consolidación COP**.

---

## 📋 CHECKLIST DE CONFIGURACIÓN

### ✅ FASE 1: INFORMACIÓN BÁSICA

- [ ] **URL del portal**
  - Definir: `https://[dominio-a-definir]`
  - Ambiente: Preproducción / Producción
  - País: Colombia
  - Moneda: COP (Pesos Colombianos)

- [ ] **Identificación del modelo**
  - Nombre completo: Consolidación COP
  - Prefijo: [CCOP]
  - Célula: [Kepler / Otra célula]
  - Equipo responsable: [A definir]

---

### ✅ FASE 2: MODELO DE NEGOCIO

- [ ] **Sistema de pago**
  - [ ] ¿Usa millas/puntos?
  - [ ] ¿Usa dinero en efectivo?
  - [ ] ¿Usa sistema mixto (millas + efectivo)?
  - [ ] ¿Tiene slider como BGR?
  - [ ] ¿Tiene fee de procesamiento?
  - [ ] ¿Requiere tarjeta de crédito?

- [ ] **Tipo de emisión**
  - [ ] ¿Automática? (Emitida inmediato)
  - [ ] ¿Manual? (Requiere intervención humana)
  - [ ] ¿Semiautomática? (Débito → Pago → Emisión)
  - [ ] Definir estados de reserva

---

### ✅ FASE 3: PRODUCTOS Y PROVEEDORES

**Definir qué productos estará disponibles:**

- [ ] **Vuelos**
  - Framework: [Angular / React / Meteor / Otro]
  - Proveedores:
    - [ ] AGGREGATOR NETACTICA
    - [ ] AGGREGATOR SABRE
    - [ ] SABRE EDIFACT
    - [ ] Otro: ____________

- [ ] **Hoteles**
  - Framework: [Angular / React / Meteor / Otro]
  - Proveedores:
    - [ ] HotelBeds
    - [ ] DerbySoft
    - [ ] Otro: ____________

- [ ] **Autos**
  - Framework: [Angular / React / Meteor / Otro]
  - Proveedores:
    - [ ] Sabre (Hertz, Dollar, Thrifty)
    - [ ] Otro: ____________

- [ ] **Actividades**
  - Framework: [Angular / React / Meteor / Otro]
  - Proveedores:
    - [ ] HotelBeds
    - [ ] Otro: ____________

- [ ] **Disney/Parques**
  - Framework: [Angular / React / Meteor / Otro]
  - Proveedores:
    - [ ] DerbySoft
    - [ ] OffLine
    - [ ] Otro: ____________

- [ ] **Otros productos**
  - Producto: ____________
  - Framework: ____________
  - Proveedor: ____________

---

### ✅ FASE 4: VALIDACIONES CRÍTICAS

- [ ] **Validación de saldo**
  - ¿Cuándo se valida? [Antes de búsqueda / Antes de checkout / Ambos]
  - ¿Qué mensaje muestra si es insuficiente?
  - ¿Se puede continuar con saldo parcial?

- [ ] **Validación de checkout**
  - ¿Qué datos se validan?
  - ¿Qué campos son obligatorios?
  - ¿Tiene validaciones especiales por producto?

- [ ] **Validación de emisión**
  - ¿Qué valida antes de emitir?
  - ¿Tiene timeout de emisión?
  - ¿Qué pasa si falla la emisión?

---

### ✅ FASE 5: ESTADOS Y FLUJOS

- [ ] **Definir estados de reserva**
  - Estado 1: [Nombre] - [Descripción]
  - Estado 2: [Nombre] - [Descripción]
  - Estado 3: [Nombre] - [Descripción]
  - Estado 4: [Nombre] - [Descripción]
  - Estado 5: [Nombre] - [Descripción]

- [ ] **Diagramar flujo de compra**
  - Búsqueda → Resultados
  - Selección → Checkout
  - Checkout → Emisión
  - Emisión → Estado final

---

### ✅ FASE 6: DOCUMENTACIÓN TÉCNICA

- [ ] **Crear documentos por producto:**
  - [ ] CCOP_VUELOS.md (si aplica)
  - [ ] CCOP_HOTELES.md (si aplica)
  - [ ] CCOP_AUTOS.md (si aplica)
  - [ ] CCOP_ACTIVIDADES.md (si aplica)
  - [ ] CCOP_DISNEY.md (si aplica)
  - [ ] CCOP_[OTRO].md (si aplica)

- [ ] **Actualizar CCOP_COMMON_RULES.md:**
  - [ ] URL del portal
  - [ ] Productos disponibles
  - [ ] Modelo de negocio
  - [ ] Tipo de emisión
  - [ ] Proveedores
  - [ ] Frameworks
  - [ ] Estados de reserva
  - [ ] Validaciones críticas

---

### ✅ FASE 7: AZURE DEVOPS

- [ ] **Configurar Test Plan:**
  - projectName: [A definir]
  - planId: [A definir]
  - planName: [A definir]

- [ ] **Crear Test Suites por producto:**
  - [ ] Suite Vuelos: suiteId = [A definir]
  - [ ] Suite Hoteles: suiteId = [A definir]
  - [ ] Suite Autos: suiteId = [A definir]
  - [ ] Suite Actividades: suiteId = [A definir]
  - [ ] Suite Disney: suiteId = [A definir]
  - [ ] Suite Otros: suiteId = [A definir]

- [ ] **Configurar trazabilidad:**
  - [ ] Vincular HU con Test Cases
  - [ ] Configurar área path
  - [ ] Configurar iteration path

---

### ✅ FASE 8: EQUIPO Y RESPONSABILIDADES

- [ ] **Asignar roles:**
  - Tech Manager (TM): [Nombre]
  - Tech Lead (TL): [Nombre]
  - Product Owner (PO): [Nombre]
  - QA Lead: [Nombre]
  - QA Testers: [Nombres]
  - Frontend Devs: [Nombres]
  - Backend Devs: [Nombres]

- [ ] **Definir célula:**
  - [ ] Kepler
  - [ ] Pixel
  - [ ] Rocket
  - [ ] Skynet
  - [ ] Transversales
  - [ ] Nueva célula: ____________

---

## 📚 TEMPLATES DE DOCUMENTACIÓN

### TEMPLATE: CCOP_[PRODUCTO].md

Copiar estructura de:
- [PM_VUELOS.md](../products/B2C/AVASA/VIVA%20AEROBUS/PM_VUELOS.md) (si existe)
- [BGR_VUELOS.md](../products/[ruta]/BGR_VUELOS.md) (si existe)

Adaptar según el producto y proveedor.

---

## 🔗 ARCHIVOS CREADOS

✅ Ya creados en esta configuración inicial:

1. **CCOP_COMMON_RULES.md**
   - Ubicación: `.github/shared/Kepler/CCOP_COMMON_RULES.md`
   - Estado: 🔄 Pendiente completar datos

2. **CCOP_QA_Assistant.agent.md**
   - Ubicación: `.github/agents/CCOP_QA_Assistant.agent.md`
   - Estado: ✅ Listo (pendiente ajustes según configuración)

3. **CCOP_SETUP_GUIDE.md** (este archivo)
   - Ubicación: `.github/docs/CCOP_SETUP_GUIDE.md`
   - Estado: ✅ Listo

---

## 🚀 PRÓXIMOS PASOS

1. **Reunión de Kickoff:**
   - Revisar este checklist con el equipo
   - Asignar responsables por cada fase
   - Definir timeline de configuración

2. **Completar información básica:**
   - URL del portal
   - Modelo de negocio
   - Productos disponibles
   - Proveedores por producto

3. **Crear documentación técnica:**
   - Documentos específicos por producto
   - Actualizar CCOP_COMMON_RULES.md con datos reales

4. **Configurar Azure DevOps:**
   - Crear Test Plan
   - Crear Test Suites
   - Definir estructura de trazabilidad

5. **Activar agente CCOP_QA_Assistant:**
   - Validar que toda la documentación esté completa
   - Hacer pruebas de creación de casos
   - Ajustar formato según necesidades

---

## 📞 CONTACTOS Y SOPORTE

**Para consultas sobre:**

- **Arquitectura del modelo:** QA_LEAD_Assistant
- **Comparaciones con otros modelos:** QA_LEAD_Assistant
- **Creación de casos CCOP:** CCOP_QA_Assistant
- **Documentación técnica:** [Líder QA a definir]
- **Azure DevOps:** [Administrador ADO a definir]

---

## 📝 HISTORIAL DE CAMBIOS

| Fecha | Versión | Cambios | Autor |
|-------|---------|---------|-------|
| 2026-01-22 | 1.0 | Configuración inicial | GitHub Copilot |
| [Fecha] | [Ver] | [Cambios] | [Autor] |

---

**Última actualización:** 2026-01-22  
**Estado del modelo:** 🔄 EN CONFIGURACIÓN INICIAL  
**Próxima revisión:** [A definir]
