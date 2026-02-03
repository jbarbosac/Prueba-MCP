# 🌍 **ENTORNOS - MASTERCARD PRICELESS 2X1**

## 📋 **INFORMACIÓN GENERAL**

**Cliente:** Mastercard (Sub-proyecto Priceless 2X1)  
**País:** Colombia  
**Moneda:** COP (Pesos Colombianos)  
**Célula:** Skynet  
**Modelo:** B2C - 100% Dinero con promociones 2X1 o Descuento  
**Productos:** Vuelos, Hoteles, Autos  

---

## 🏗️ **ENTORNOS DISPONIBLES**

### **1️⃣ ENTORNO TEST**

#### **URLs:**
- **Home (React):** https://test-skynet-pmc.smartlinks.dev/es-co
- **Vuelos (Angular):** https://test-skynet-pmc.smartlinks.dev/es-co/flights
- **Hoteles (Angular):** https://test-skynet-pmc.smartlinks.dev/es-co/hotels
- **Autos (React):** https://test-skynet-pmc.smartlinks.dev/es-co/cars

#### **Características:**
- ✅ Acceso directo (sin login)
- ✅ Integración con proveedores en modo test
- ✅ PlacetoPay en modo sandbox
- ✅ Promociones configurables (2X1/Descuento)
- ✅ Dispersión configurable (Vuelos)
- ✅ Fee oculto configurable (Vuelos)

#### **Configuración PlacetoPay:**
```yaml
Modo: Sandbox
Login: [Configurado en backend]
TranKey: [Configurado en backend]
URL: https://checkout-test.placetopay.com
```

#### **Proveedores en Test:**
| Producto | Proveedor(es) | Estado |
|----------|---------------|--------|
| Vuelos | SABRE, AGGREGATOR NETATICA, AGGREGATOR SABRE NDC | ✅ Activo |
| Hoteles | SABRE | ✅ Activo |
| Autos | Hertz (Colombia), Thermeon (México) | ✅ Activo |

#### **Tarjetas de Prueba (PlacetoPay Sandbox):**
```yaml
# TC Cliente (aprobación)
Número: 5121220000000000
CVV: 123
Vencimiento: 12/28
Nombre: Test User

# TC Cliente (rechazo)
Número: 5121220000000001
CVV: 123
Vencimiento: 12/28
Nombre: Test User Declined

# TC Corporativa (dispersión)
Número: [Solicitar a equipo de backend]
CVV: 123
Vencimiento: 12/28
Nombre: Mastercard Corporate
```

#### **Aeropuertos Permitidos (Vuelos):**
Collection MongoDB: `allowedAirports`
- Lista configurable por equipo de backend
- Ejemplo: BOG, MDE, CLO, CTG, BAQ, SMR, ADZ, PEI, BGA, etc.

#### **Accesos:**
- **Azure DevOps:** https://dev.azure.com/ultragrouplaorg/ultragroupla
- **Repositorio:** [Solicitar acceso a equipo Skynet]
- **Postman Collection:** [Solicitar a equipo de backend]

---

### **2️⃣ ENTORNO DEMO**

#### **URLs:**
- **Home (React):** https://demo-skynet-pmc.smartlinks.dev/es-co
- **Vuelos (Angular):** https://demo-skynet-pmc.smartlinks.dev/es-co/flights
- **Hoteles (Angular):** https://demo-skynet-pmc.smartlinks.dev/es-co/hotels
- **Autos (React):** https://demo-skynet-pmc.smartlinks.dev/es-co/cars

#### **Características:**
- ✅ Datos cercanos a producción
- ✅ Integración con proveedores en modo UAT
- ✅ PlacetoPay en modo producción
- ✅ Promociones pre-configuradas
- ⚠️ Tarjetas reales requeridas (pago real)

#### **Propósito:**
- Validaciones finales antes de producción
- Demos a cliente
- UAT (User Acceptance Testing)

#### **Configuración PlacetoPay:**
```yaml
Modo: Production
Login: [Configurado en backend]
TranKey: [Configurado en backend]
URL: https://checkout.placetopay.com
```

#### **Proveedores en Demo:**
| Producto | Proveedor(es) | Estado |
|----------|---------------|--------|
| Vuelos | SABRE, AGGREGATOR NETATICA, AGGREGATOR SABRE NDC | ✅ Activo |
| Hoteles | SABRE | ✅ Activo |
| Autos | Hertz (Colombia), Thermeon (México) | ✅ Activo |

#### **⚠️ IMPORTANTE:**
- Los pagos en DEMO son REALES
- Se requiere coordinación con equipo de operaciones para reversos
- Validar con Carlos Alberto Rubio Gallego antes de ejecutar pruebas

---

### **3️⃣ ENTORNO PRODUCCIÓN**

#### **URLs:**
- **Home (React):** https://vuelaconoccidente.com/es-co
- **Vuelos (Angular):** https://vuelaconoccidente.com/es-co/flights
- **Hoteles (Angular):** https://vuelaconoccidente.com/es-co/hotels
- **Autos (React):** https://vuelaconoccidente.com/es-co/cars

#### **Características:**
- ✅ Entorno productivo
- ✅ Usuarios reales
- ✅ PlacetoPay en producción
- ✅ Promociones oficiales (configuradas por Mastercard)
- 🚫 NO ejecutar pruebas sin autorización

#### **Configuración PlacetoPay:**
```yaml
Modo: Production
Login: [Configurado en backend - PROD]
TranKey: [Configurado en backend - PROD]
URL: https://checkout.placetopay.com
```

#### **Proveedores en Producción:**
| Producto | Proveedor(es) | Estado |
|----------|---------------|--------|
| Vuelos | SABRE, AGGREGATOR NETATICA, AGGREGATOR SABRE NDC | ✅ Activo |
| Hoteles | SABRE | ✅ Activo |
| Autos | Hertz (Colombia), Thermeon (México) | ✅ Activo |

#### **Monitoreo:**
- ⚠️ Logs centralizados en [herramienta de monitoreo - solicitar acceso]
- ⚠️ Alertas configuradas para errores críticos
- ⚠️ Coordinación con equipo de operaciones para soporte 24/7

#### **⚠️ RESTRICCIONES:**
- 🚫 NO realizar pruebas manuales sin aprobación
- 🚫 NO usar tarjetas de prueba
- 🚫 NO modificar configuraciones sin change management
- ✅ Solo smoke tests post-deployment autorizados

---

## 🔑 **ACCESOS Y CREDENCIALES**

### **Equipo QA:**
| Recurso | Responsable | Contacto |
|---------|-------------|----------|
| Azure DevOps | Carlos Alberto Rubio Gallego | crubiog@ultragroupla.com |
| PlacetoPay Sandbox | Backend Team | [Solicitar en Slack] |
| MongoDB Test | Backend Team | [Solicitar en Slack] |
| Postman Collections | Carlos Alberto Rubio Gallego | Azure DevOps Repos |

### **Equipo Backend:**
| Recurso | Responsable | Contacto |
|---------|-------------|----------|
| PlacetoPay Production | Angelo Nieto | anieto@ultragroupla.com |
| MongoDB Production | Angelo Nieto | anieto@ultragroupla.com |
| SABRE API Keys | Backend Team | [Solicitar en Slack] |
| Hertz/Thermeon API | Backend Team | [Solicitar en Slack] |

### **Equipo Frontend:**
| Recurso | Responsable | Contacto |
|---------|-------------|----------|
| Angular (Vuelos/Hoteles) | Sergio Mauricio Pimiento Niño | spimiento@ultragroupla.com |
| React (Home/Autos) | Sergio Mauricio Pimiento Niño | spimiento@ultragroupla.com |

---

## 🔧 **CONFIGURACIONES CLAVE**

### **Variables de Entorno (Backend):**

**TEST:**
```env
ENVIRONMENT=test
PLACETOPAY_MODE=sandbox
PLACETOPAY_URL=https://checkout-test.placetopay.com
SABRE_ENV=test
MONGODB_URI=mongodb://[test-server]/priceless-test
DISPERSION_ENABLED=true
FEE_OCULTO_ENABLED=true
PROMOCION_2X1_ENABLED=true
PROMOCION_DESCUENTO_ENABLED=true
```

**DEMO:**
```env
ENVIRONMENT=demo
PLACETOPAY_MODE=production
PLACETOPAY_URL=https://checkout.placetopay.com
SABRE_ENV=uat
MONGODB_URI=mongodb://[demo-server]/priceless-demo
DISPERSION_ENABLED=true
FEE_OCULTO_ENABLED=true
PROMOCION_2X1_ENABLED=true
PROMOCION_DESCUENTO_ENABLED=true
```

**PRODUCCIÓN:**
```env
ENVIRONMENT=production
PLACETOPAY_MODE=production
PLACETOPAY_URL=https://checkout.placetopay.com
SABRE_ENV=production
MONGODB_URI=mongodb://[prod-server]/priceless-prod
DISPERSION_ENABLED=true
FEE_OCULTO_ENABLED=true
PROMOCION_2X1_ENABLED=true
PROMOCION_DESCUENTO_ENABLED=true
```

---

## 🧪 **DATOS DE PRUEBA**

### **Vuelos - Escenario 1 (2X1 sin fee oculto + Dispersión ACTIVA):**
```yaml
Origen: BOG (Bogotá)
Destino: MDE (Medellín)
Tipo: Ida y vuelta
Fecha ida: +7 días desde hoy
Fecha vuelta: +10 días desde hoy
Pasajeros: 2 adultos
Promoción: 2X1
Aerolínea: Avianca (dispersión ACTIVA)
TC Cliente: 5121220000000000
TC Corporativa: [Backend configura]
```

### **Hoteles - Modelo Simplificado:**
```yaml
Ciudad: Cartagena
Check-in: +7 días desde hoy
Check-out: +9 días desde hoy
Habitaciones: 1
Huéspedes: 2 adultos
Promoción: Descuento 30%
TC Cliente: 5121220000000000
```

### **Autos - Modelo Simplificado:**
```yaml
Ciudad: Bogotá
Recogida: +7 días desde hoy
Devolución: +12 días desde hoy
Categoría: Compacto
Proveedor: Hertz
Promoción: 2X1
TC Cliente: 5121220000000000
```

---

## 📞 **CONTACTOS DE SOPORTE**

### **Célula Skynet:**
| Rol | Nombre | Email |
|-----|--------|-------|
| **Líder Célula** | Juan Camilo Estrada | jestrada@ultragroupla.com |
| **QA Mastercard** | Carlos Alberto Rubio Gallego | crubiog@ultragroupla.com |
| **Frontend Mastercard** | Sergio Mauricio Pimiento Niño | spimiento@ultragroupla.com |
| **Backend Mastercard** | Angelo Nieto | anieto@ultragroupla.com |
| **PO Mastercard** | Juan Bernardo Arias Hurtado | jhurtado@ultragroupla.com |

### **Soporte PlacetoPay:**
- **Email:** soporte@placetopay.com
- **Documentación:** https://docs.placetopay.com

### **Soporte Proveedores:**
| Proveedor | Contacto | Producto |
|-----------|----------|----------|
| SABRE | [Backend Team] | Vuelos, Hoteles |
| Netactica | [Backend Team] | Vuelos (Aggregator) |
| Hertz | [Backend Team] | Autos (Colombia) |
| Thermeon | [Backend Team] | Autos (México) |

---

## 🎯 **VALIDACIONES POR ENTORNO**

### **Test:**
- ✅ Validar 7 escenarios de Vuelos
- ✅ Validar modelo simplificado Hoteles/Autos
- ✅ Validar cálculo de promociones (2X1 y Descuento)
- ✅ Validar fee transaccional ($10,000 COP/PAX en Vuelos)
- ✅ Validar markup ($10,000 COP/unidad en Hoteles/Autos)
- ✅ Validar dispersión (ACTIVA/INACTIVA en Vuelos)
- ✅ Validar emisión (TC Cliente, TC Corp, CASH, Mixta en Vuelos)
- ✅ Validar emisión CASH automática (Hoteles/Autos)
- ✅ Validar allowedAirports (Vuelos)
- ✅ Validar proceso de cancelación manual

### **Demo:**
- ✅ Smoke tests de flujos críticos
- ✅ Validar integración PlacetoPay en producción
- ✅ Validar promociones configuradas por cliente
- ⚠️ Coordinar con operaciones para reversos

### **Producción:**
- ✅ Solo smoke tests post-deployment
- ✅ Monitoreo de errores en tiempo real
- 🚫 NO pruebas manuales sin autorización

---

## 📚 **REFERENCIAS**

- 📋 [PRICELESS_COMMON_RULES.md](../../../shared/Reglas Marketplace/PRICELESS_COMMON_RULES.md) - Reglas de negocio
- 📋 [README.MD](README.MD) - Documentación principal
- 🛫 [PRICELESS_VUELOS.md](PRICELESS_VUELOS.md) - Flujo E2E Vuelos
- 🏨 [PRICELESS_HOTELES.md](PRICELESS_HOTELES.md) - Flujo E2E Hoteles
- 🚗 [PRICELESS_AUTOS.md](PRICELESS_AUTOS.md) - Flujo E2E Autos
- 📊 [Calcular 2x1 o descuento.xlsx](https://smartlinksdev-my.sharepoint.com/:x:/r/personal/crubiog_ultragroupla_com/_layouts/15/Doc.aspx?sourcedoc=%7B64CBE898-E0F2-402B-88AB-1093813C7C49%7D&file=Calcular%202x1%20o%20descuento.xlsx) - Fórmulas oficiales
- 📋 [Wiki Azure DevOps](https://dev.azure.com/ultragrouplaorg/ultragroupla/_wiki/wikis/Ultra%20Group%20Wiki/1141/Mastercard-Priceless-2X1) - Documentación técnica

---

## 🚀 **PROCESO DE DESPLIEGUE**

### **Pipelines Azure DevOps:**

**Frontend Angular (Vuelos + Hoteles):**
- Pipeline: `smartlinks-web-testing-pmc-aks`
- URL: https://dev.azure.com/ultragrouplaorg/ultragroupla/_build?definitionId=213
- Infraestructura: AKS (Azure Kubernetes Service)

**Frontend React (Home + Autos):**
- Pipeline: `smartlinks-web-travel-testing-pmc-aks`
- URL: https://dev.azure.com/ultragrouplaorg/ultragroupla/_build?definitionId=210
- Infraestructura: AKS (Azure Kubernetes Service)

**Widgets:**
- Pipeline: `smartlinks-widgets-pmc-test`
- URL: https://dev.azure.com/ultragrouplaorg/ultragroupla/_build?definitionId=216
- Trigger: Manual (debe ejecutarse manualmente)
- Infraestructura: Azure App Service

**Meteor (Admin):**
- Pipeline: `smartlinks-meteor`
- Trigger: Automático al subir cambios a rama del PR
- Stage TEST: `Test` (Priceless no tiene stage propio)
- Infraestructura: Azure App Service

**Backend (API Core):**
- Pipeline: `smartlinks-api-core-test`
- Trigger: Automático al subir cambios a rama del PR
- Stage TEST Priceless 2X1: `PMC`
- Infraestructura: Azure App Service

---

### **Despliegue de Pull Requests (PRs):**

#### **Frontend (Angular/React):**

**Requisitos previos:**
- ✅ Aprobación de un dev frontend par (peer review)
- ✅ Aprobación de TM o TL de frontend

**Pasos para desplegar:**

1. Ir al pipeline correspondiente:
   - **Angular (Vuelos/Hoteles):** `smartlinks-web-testing-pmc-aks`
   - **React (Home/Autos):** `smartlinks-web-travel-testing-pmc-aks`

2. Clic en **"Run pipeline"** (botón azul superior derecho)

3. Seleccionar la rama del PR en el dropdown (ej: `feature/PRICELESS-123-nueva-funcionalidad`)

4. Confirmar ejecución manual

El pipeline ejecutará: Build → Tests → Deploy to AKS (TEST) → Smoke Tests

---

#### **Backend (api-core):**

**Proceso automático:**
- ✅ Pipeline `smartlinks-api-core-test` se ejecuta **automáticamente** al hacer push a la rama del PR
- ✅ Para desplegar en ambiente TEST Priceless 2X1, ejecutar el **Stage "PMC"**
- ✅ No requiere ejecución manual del pipeline completo

**Pasos:**
1. Hacer push de cambios a la rama del PR
2. Pipeline se ejecuta automáticamente
3. Ir al Stage **"PMC"** en el pipeline
4. Ejecutar/Aprobar el stage para desplegar en TEST Priceless 2X1

---

### **Despliegue en TEST (Automático):**
- Trigger: Automático al merge a rama `develop`
- Aprobación: No requerida

### **Despliegue en DEMO (Manual):**
- Trigger: Manual desde rama `release/*`
- Aprobación: Requerida (PO o Tech Lead)
