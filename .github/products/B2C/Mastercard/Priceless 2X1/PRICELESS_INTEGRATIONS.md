# 🔌 **INTEGRACIONES - MASTERCARD PRICELESS 2X1**

## 📋 **INFORMACIÓN GENERAL**

**Cliente:** Mastercard (Sub-proyecto Priceless 2X1)  
**País:** Colombia  
**Moneda:** COP (Pesos Colombianos)  
**Célula:** Skynet  
**Modelo:** B2C - 100% Dinero con promociones 2X1 o Descuento  

---

## 🌐 **ARQUITECTURA DE INTEGRACIONES**

```
┌─────────────────────────────────────────────────────────────┐
│                   FRONTEND (React + Angular)                │
│                                                             │
│  Home (React)  │  Vuelos (Angular)  │  Hoteles  │  Autos   │
└────────────┬────────────────────────┴───────────┴──────────┘
             │
             │ REST API
             ▼
┌─────────────────────────────────────────────────────────────┐
│                      BACKEND (Node.js)                      │
│                                                             │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐   │
│  │ Vuelos   │  │ Hoteles  │  │  Autos   │  │ Payment  │   │
│  │ Service  │  │ Service  │  │ Service  │  │ Service  │   │
│  └────┬─────┘  └────┬─────┘  └────┬─────┘  └────┬─────┘   │
└───────┼─────────────┼─────────────┼─────────────┼──────────┘
        │             │             │             │
        │             │             │             │
   ┌────┴───┐    ┌────┴───┐    ┌────┴───┐    ┌────┴────┐
   │ SABRE  │    │ SABRE  │    │ Hertz  │    │PlacetoPay│
   │Netactica│   │        │    │Thermeon│    │         │
   │SABRE NDC│   │        │    │        │    │         │
   └────────┘    └────────┘    └────────┘    └─────┬───┘
                                                    │
                                              ┌─────┴─────┐
                                              │ Dispersión│
                                              │(Vuelos)   │
                                              │TC Corporat│
                                              └───────────┘
        ┌──────────────────────────────────────────┐
        │           MongoDB (allowedAirports)      │
        └──────────────────────────────────────────┘
```

---

## 🛫 **INTEGRACIÓN VUELOS**

### **Proveedores Disponibles:**

#### **1️⃣ SABRE (Edifact)**
```yaml
Tipo: GDS (Global Distribution System)
Proveedor: SABRE
Protocolo: Edifact (XML/SOAP)
Productos: Vuelos
Modelo: Dispersión condicional
```

**Endpoints:**
```
Búsqueda: https://api.sabre.com/v1/shop/flights
Reserva: https://api.sabre.com/v1/air/book
Emisión: https://api.sabre.com/v1/air/ticket
```

**Autenticación:**
```yaml
Tipo: OAuth 2.0
Client ID: [Configurado en backend]
Client Secret: [Configurado en backend]
Token URL: https://api.sabre.com/v2/auth/token
```

**Características:**
- ✅ Dispersión ACTIVA (aerolíneas configuradas)
- ✅ Fee oculto (cuando aplica)
- ✅ Emisión dual: TC Cliente + TC Corporativa
- ✅ allowedAirports validation

**Escenarios aplicables:** 1, 2, 3, 4, 5, 6

---

#### **2️⃣ AGGREGATOR NETATICA**
```yaml
Tipo: Aggregator
Proveedor: Netatica
Protocolo: REST API (JSON)
Productos: Vuelos
Modelo: CASH automático
```

**Endpoints:**
```
Búsqueda: https://api.netatica.com/v1/flights/search
Reserva: https://api.netatica.com/v1/flights/book
Confirmación: https://api.netatica.com/v1/flights/confirm
```

**Autenticación:**
```yaml
Tipo: API Key
Header: X-API-Key
Value: [Configurado en backend]
```

**Características:**
- ❌ Dispersión NO aplicable (Aggregator)
- ❌ Fee oculto NO aplica
- ✅ Emisión CASH automática
- ✅ Pago único TC Cliente

**Escenario aplicable:** 7

---

#### **3️⃣ AGGREGATOR SABRE NDC**
```yaml
Tipo: Aggregator (NDC)
Proveedor: SABRE NDC
Protocolo: REST API (JSON)
Productos: Vuelos
Modelo: CASH automático
```

**Endpoints:**
```
Búsqueda: https://api.sabre.com/v1/offers/shop
Reserva: https://api.sabre.com/v1/orders/create
Confirmación: https://api.sabre.com/v1/orders/confirm
```

**Autenticación:**
```yaml
Tipo: OAuth 2.0 + NDC
Client ID: [Configurado en backend]
Client Secret: [Configurado en backend]
Token URL: https://api.sabre.com/v2/auth/token
```

**Características:**
- ❌ Dispersión NO aplicable (Aggregator)
- ❌ Fee oculto NO aplica
- ✅ Emisión CASH automática
- ✅ Pago único TC Cliente

**Escenario aplicable:** 7

---

### **Validación allowedAirports:**

**Fuente:** MongoDB Collection `allowedAirports`

**Estructura:**
```json
{
  "_id": "aeropuertos_colombia",
  "country": "CO",
  "airports": [
    {
      "code": "BOG",
      "name": "Aeropuerto Internacional El Dorado",
      "city": "Bogotá",
      "enabled": true
    },
    {
      "code": "MDE",
      "name": "Aeropuerto Internacional José María Córdova",
      "city": "Medellín",
      "enabled": true
    },
    {
      "code": "CLO",
      "name": "Aeropuerto Internacional Alfonso Bonilla Aragón",
      "city": "Cali",
      "enabled": true
    }
    // ... más aeropuertos
  ]
}
```

**Validación en búsqueda:**
```javascript
if (!allowedAirports.includes(origen) || !allowedAirports.includes(destino)) {
  throw new Error("Aeropuerto no permitido para promociones Priceless");
}
```

---

## 🏨 **INTEGRACIÓN HOTELES**

### **Proveedor: SABRE**

```yaml
Tipo: GDS
Proveedor: SABRE
Protocolo: REST API (JSON)
Productos: Hoteles
Modelo: Pago directo Ultragroup + CASH
```

**Endpoints:**
```
Búsqueda: https://api.sabre.com/v1/shop/hotels
Disponibilidad: https://api.sabre.com/v1/shop/hotels/availability
Reserva: https://api.sabre.com/v1/hotel/book
```

**Autenticación:**
```yaml
Tipo: OAuth 2.0
Client ID: [Mismo que Vuelos]
Client Secret: [Mismo que Vuelos]
Token URL: https://api.sabre.com/v2/auth/token
```

**Características:**
- ❌ Dispersión NO aplica (pago directo)
- ❌ Fee oculto NO aplica
- ✅ Markup $10,000 COP/noche
- ✅ Emisión CASH automática
- ✅ Pago único TC Cliente → Ultragroup

**Flujo de Integración:**
```
1. Búsqueda → SABRE API
2. Selección → Frontend
3. Aplicar Markup → Backend
4. Pago → PlacetoPay (TC Cliente)
5. Reserva → SABRE API
6. Emisión → CASH automático
```

---

## 🚗 **INTEGRACIÓN AUTOS**

### **Proveedor 1: Hertz (Colombia)**

```yaml
Tipo: API Directa
Proveedor: Hertz
Protocolo: REST API (JSON)
Países: Colombia
Modelo: Pago directo Ultragroup + CASH
```

**Endpoints:**
```
Búsqueda: https://api.hertz.com/v1/cars/search
Disponibilidad: https://api.hertz.com/v1/cars/availability
Reserva: https://api.hertz.com/v1/cars/book
```

**Autenticación:**
```yaml
Tipo: API Key
Header: Authorization
Value: Bearer [Configurado en backend]
```

**Características:**
- ❌ Dispersión NO aplica
- ❌ Fee oculto NO aplica
- ✅ Markup $10,000 COP/día
- ✅ Emisión CASH automática
- ✅ Pago único TC Cliente → Ultragroup

---

### **Proveedor 2: Thermeon (México)**

```yaml
Tipo: Aggregator
Proveedor: Thermeon
Protocolo: REST API (JSON)
Países: México
Modelo: Pago directo Ultragroup + CASH
```

**Endpoints:**
```
Búsqueda: https://api.thermeon.com/v1/vehicles/search
Reserva: https://api.thermeon.com/v1/vehicles/book
Confirmación: https://api.thermeon.com/v1/vehicles/confirm
```

**Autenticación:**
```yaml
Tipo: API Key + Secret
Header: X-API-Key
Value: [Configurado en backend]
```

**Características:**
- ❌ Dispersión NO aplica
- ❌ Fee oculto NO aplica
- ✅ Markup $10,000 COP/día (convertido a MXN si aplica)
- ✅ Emisión CASH automática
- ✅ Pago único TC Cliente → Ultragroup

**Nota:** Aunque Thermeon opera en México, el pago se procesa en COP (Colombia).

---

## 💳 **INTEGRACIÓN PLACETOPAY (P2P)**

### **Pasarela de Pago Principal**

```yaml
Proveedor: PlacetoPay
Tipo: Payment Gateway
País: Colombia
Moneda: COP
Protocolo: REST API (JSON)
```

**Endpoints:**

**Test (Sandbox):**
```
URL Base: https://checkout-test.placetopay.com
Process: /api/session
Query: /api/session/{requestId}
Redirect: /session/{requestId}
```

**Producción:**
```
URL Base: https://checkout.placetopay.com
Process: /api/session
Query: /api/session/{requestId}
Redirect: /session/{requestId}
```

**Autenticación:**
```yaml
Tipo: Custom (Nonce + SHA256)
Login: [Configurado en backend]
TranKey: [Configurado en backend]
Algoritmo: SHA256(nonce + seed + tranKey)
```

---

### **Flujo de Pago Estándar:**

#### **1️⃣ Crear Sesión:**
```json
POST /api/session
{
  "auth": {
    "login": "xxxxxxxxxx",
    "tranKey": "xxxxxxxxxx",
    "nonce": "xxxxxxxxxx",
    "seed": "2025-01-15T12:00:00-05:00"
  },
  "payment": {
    "reference": "PRICELESS-2X1-12345",
    "description": "Vuelo BOG-MDE 2X1",
    "amount": {
      "currency": "COP",
      "total": 820000
    }
  },
  "returnUrl": "https://vuelaconoccidente.com/payment/return",
  "cancelUrl": "https://vuelaconoccidente.com/payment/cancel",
  "ipAddress": "190.25.231.234",
  "userAgent": "Mozilla/5.0..."
}
```

#### **2️⃣ Redirigir Usuario:**
```javascript
// Response de PlacetoPay
{
  "status": {
    "status": "OK",
    "message": "Session created"
  },
  "requestId": 123456,
  "processUrl": "https://checkout.placetopay.com/session/123456"
}

// Frontend redirige a processUrl
window.location.href = response.processUrl;
```

#### **3️⃣ Consultar Estado:**
```json
POST /api/session/123456
{
  "auth": {
    "login": "xxxxxxxxxx",
    "tranKey": "xxxxxxxxxx",
    "nonce": "xxxxxxxxxx",
    "seed": "2025-01-15T12:05:00-05:00"
  }
}
```

**Response:**
```json
{
  "status": {
    "status": "APPROVED",
    "reason": "00",
    "message": "La petición ha sido aprobada exitosamente"
  },
  "payment": [
    {
      "status": {
        "status": "APPROVED"
      },
      "internalReference": 1,
      "paymentMethod": "CR_VS",
      "amount": {
        "from": {
          "currency": "COP",
          "total": 820000
        }
      },
      "authorization": "000000",
      "receipt": "241560000001",
      "franchise": "CR_VS"
    }
  ]
}
```

---

### **Dispersión de Fondos (SOLO VUELOS):**

**Escenarios con Dispersión:**

#### **Escenario 1: 2X1 sin fee oculto + Dispersión ACTIVA**
```json
// Pago 1: TC Cliente
{
  "amount": {
    "currency": "COP",
    "total": 410000  // 1 PQ + Fee Transaccional
  },
  "dispersions": []  // Pago directo
}

// Pago 2: TC Corporativa
{
  "amount": {
    "currency": "COP",
    "total": 400000  // 1 PQ sin fee
  },
  "dispersions": [
    {
      "amount": 400000,
      "account": "[Cuenta aerolínea]"
    }
  ]
}
```

#### **Escenario 3: 2X1/Desc con fee oculto + Dispersión ACTIVA**
```json
// Pago 1: TC Cliente
{
  "amount": {
    "currency": "COP",
    "total": 820000  // Total visible al usuario
  },
  "dispersions": []
}

// Pago 2: TC Corporativa (fee oculto)
{
  "amount": {
    "currency": "COP",
    "total": 800000  // 2 PQ sin fee (oculto al usuario)
  },
  "dispersions": [
    {
      "amount": 800000,
      "account": "[Cuenta aerolínea]"
    }
  ]
}
```

**⚠️ IMPORTANTE:**
- Dispersión SOLO en Vuelos con proveedor Edifact (SABRE)
- Hoteles y Autos: Pago directo a Ultragroup (sin dispersión)
- Aggregators (Netatica, SABRE NDC): Sin dispersión

---

## 🗄️ **INTEGRACIÓN MONGODB**

### **Collections Principales:**

#### **1️⃣ allowedAirports**
```json
{
  "_id": "aeropuertos_colombia",
  "country": "CO",
  "airports": [
    { "code": "BOG", "name": "...", "enabled": true },
    { "code": "MDE", "name": "...", "enabled": true }
  ],
  "updatedAt": "2025-01-15T10:00:00Z"
}
```

**Uso:** Validar aeropuertos permitidos en búsqueda de vuelos

---

#### **2️⃣ promociones**
```json
{
  "_id": "promo_2x1_colombia",
  "type": "2X1",
  "country": "CO",
  "product": "flights",
  "enabled": true,
  "startDate": "2025-01-01T00:00:00Z",
  "endDate": "2025-12-31T23:59:59Z",
  "conditions": {
    "minPassengers": 2,
    "maxPassengers": 2,
    "allowedAirports": ["BOG", "MDE", "CLO", "CTG"]
  }
}
```

**Uso:** Configurar promociones activas por producto

---

#### **3️⃣ dispersion_config**
```json
{
  "_id": "dispersion_airlines",
  "airlines": [
    {
      "code": "AV",
      "name": "Avianca",
      "dispersionEnabled": true,
      "account": "xxxx-xxxx-xxxx-xxxx"
    },
    {
      "code": "LA",
      "name": "LATAM",
      "dispersionEnabled": false
    }
  ]
}
```

**Uso:** Determinar si aerolínea tiene dispersión activa

---

#### **4️⃣ markup_config**
```json
{
  "_id": "markup_hoteles",
  "product": "hotels",
  "markup": {
    "type": "fixed",
    "amount": 10000,
    "currency": "COP",
    "unit": "noche"
  }
},
{
  "_id": "markup_autos",
  "product": "cars",
  "markup": {
    "type": "fixed",
    "amount": 10000,
    "currency": "COP",
    "unit": "dia"
  }
}
```

**Uso:** Aplicar markup en Hoteles y Autos

---

## 🔒 **SEGURIDAD**

### **Autenticación Frontend → Backend:**
```yaml
Tipo: Session-based
Cookie: priceless_session
HttpOnly: true
Secure: true
SameSite: Strict
```

### **Autenticación Backend → Proveedores:**

| Proveedor | Tipo | Almacenamiento |
|-----------|------|----------------|
| SABRE | OAuth 2.0 | Variables de entorno |
| Netatica | API Key | Variables de entorno |
| Hertz | API Key | Variables de entorno |
| Thermeon | API Key | Variables de entorno |
| PlacetoPay | Custom (SHA256) | Variables de entorno |

### **Cifrado:**
```yaml
Datos sensibles: AES-256
Tarjetas: Tokenización PlacetoPay
Logs: Sin datos de tarjetas
```

---

## 📊 **MONITOREO**

### **Endpoints de Health Check:**
```
GET /health/sabre
GET /health/netatica
GET /health/hertz
GET /health/thermeon
GET /health/placetopay
GET /health/mongodb
```

**Response:**
```json
{
  "status": "healthy",
  "provider": "SABRE",
  "responseTime": 250,
  "lastCheck": "2025-01-15T12:00:00Z"
}
```

### **Logs Centralizados:**
- Request/Response de proveedores
- Errores de integración
- Tiempos de respuesta
- Transacciones PlacetoPay

---

## 📞 **CONTACTOS SOPORTE PROVEEDORES**

| Proveedor | Soporte Técnico | Email |
|-----------|-----------------|-------|
| SABRE | https://developer.sabre.com/support | support@sabre.com |
| Netatica | [Backend Team - solicitar] | - |
| Hertz | [Backend Team - solicitar] | - |
| Thermeon | [Backend Team - solicitar] | - |
| PlacetoPay | https://docs.placetopay.com | soporte@placetopay.com |

---

## 📚 **REFERENCIAS**

- 📋 [PRICELESS_COMMON_RULES.md](../../../shared/Reglas Marketplace/PRICELESS_COMMON_RULES.md) - Reglas de negocio
- 📋 [PRICELESS_ENVIRONMENTS.md](PRICELESS_ENVIRONMENTS.md) - Configuración de entornos
- 📋 [README.MD](README.MD) - Documentación principal
- 📋 [Wiki Azure DevOps](https://dev.azure.com/ultragrouplaorg/ultragroupla/_wiki/wikis/Ultra%20Group%20Wiki/1141/Mastercard-Priceless-2X1) - Documentación técnica

---

**Última actualización:** Enero 2025  
**Responsable:** Angelo Nieto (Backend Mastercard)  
**QA:** Carlos Alberto Rubio Gallego  
**Agente QA:** PRICELESS_QA_Assistant  
