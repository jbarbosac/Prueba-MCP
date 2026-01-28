# 📋 REGLAS COMUNES MRS (Mastercard Rewards System)

Documento de referencia con reglas, validaciones y estructura compartida para todos los productos de MRS.

---

## 🎯 IDENTIFICACIÓN Y ALCANCE

**Portales MRS (Mastercard):**
- 🇪🇨 Ecuador (Austro): https://austec.smartlinks.dev/es-ec
- 🇭🇳 Honduras (Ficohsa): https://ficsahonduras.smartlinks.dev/es-hn
- 🇬🇹 Guatemala (Ficohsa): https://ficsaguatemala.smartlinks.dev/es-gt
- 🇵🇦 Panamá (Ficohsa): https://ficsapanama.smartlinks.dev/es-pa
- 🇳🇮 Nicaragua (Ficohsa): https://ficsanicaragua.smartlinks.dev/es-ni
- 🇨🇷 Costa Rica (Coopenae): https://cpn-mrs.smartlinks.dev/es-cr
- 🧪 Testing: https://skynet-mc-test.smartlinks.dev
- 🎯 Demo: https://demo-skynet-mc.smartlinks.dev

**Clientes:** Austro, Ficohsa (multi-país), Coopenae  
**Prefijo obligatorio:** [MRS]  

**Productos disponibles:**
- ✅ Vuelos
- ✅ Hoteles
- ✅ Autos
- ✅ Actividades
- ✅ Tickets Disney

---

## 🔐 AUTENTICACIÓN SSO (Single Sign-On)

### PROCESO DE LOGIN SSO

**Objetivo:** Generar el **token SSO** (vigencia 24h) via `security/api/saml/acs` y usarlo para iniciar sesión en la Agencia MRS.

### FLUJO DE AUTENTICACIÓN:

1. **Construir SAMLResponse** con atributos mínimos requeridos
2. **Codificar SAML en Base64** (sin saltos de línea)
3. **POST a `security/api/saml/acs`** con `SAMLResponse=<base64>`
4. **Recibir token** (vigencia 24h, TTL 12h)
5. **Armar URL de login** con el token
6. **Validar inicio de sesión** en la Agencia

### TIPOS DE USUARIO MRS:

| Código | Estado | Uso en Testing |
|--------|--------|----------------|
| 000 | Redeem Only | ❌ |
| 001 | Good Standing | ✅ **Recomendado** |
| 002 | New | ⚠️ Opcional |
| 003 | Cancelled | ❌ |
| 004 | On Hold | ❌ |
| 005 | Inactive | ❌ |

**Para testing:** Usar usuarios **001 – Good Standing** (activos)

### ATRIBUTOS SAML REQUERIDOS:

```xml
<saml2:AttributeStatement>
  <saml2:Attribute Name="RANAC">
    <saml2:AttributeValue>542185022028257854764409320205</saml2:AttributeValue>
  </saml2:Attribute>
  <saml2:Attribute Name="Email_Address">
    <saml2:AttributeValue>usuario@ejemplo.com</saml2:AttributeValue>
  </saml2:Attribute>
  <saml2:Attribute Name="First_Name">
    <saml2:AttributeValue>Nombre</saml2:AttributeValue>
  </saml2:Attribute>
  <saml2:Attribute Name="Last_Name">
    <saml2:AttributeValue>Apellido</saml2:AttributeValue>
  </saml2:Attribute>
</saml2:AttributeStatement>
```

### URLs DE LOGIN POR ENTORNO:

```
TEST: https://skynet-mc-test.smartlinks.dev/es-ec/auth?token={TOKEN}
DEMO: https://demo-skynet-mc.smartlinks.dev/es-ec/auth?token={TOKEN}
```

### VALIDACIÓN DE LOGIN EXITOSO:

✅ No hay redirecciones a sitios externos  
✅ Se mantiene dentro del dominio de la Agencia  
✅ Endpoint de users responde con status 200  
✅ Sesión queda activa en Network/DevTools  

### CONSIDERACIONES IMPORTANTES:

⚠️ **NotBefore** y **NotOnOrAfter** deben estar dentro del rango actual  
⚠️ **RANAC** debe ser de un usuario activo (consultar documentación de usuarios MRS)  
⚠️ Token SSO tiene vigencia de **24 horas**  
⚠️ TTL del token: **12 horas**  

**Documentación complementaria:**
- 📋 [Wiki: Login SSO Mastercard MRS - Generación Token](https://dev.azure.com/ultragrouplaorg/ultragroupla/_wiki/wikis/Ultra%20Group%20Wiki/1342/Login-SSO-Mastercard-MRS-Generación-Token)
- 📄 Colección Postman: MasterCard - MRS.postman_collection.json
- 📊 Documentación usuarios MRS (RANAC activos)

---

## 💰 MODELO DE NEGOCIO

### ECUACIÓN DE PAGO:

**TRES OPCIONES DE PAGO:**

```
1. Solo Millas (100% millas)
   → Pago: 100% MILLAS
   → Emisión: AUTOMÁTICA
   → Tarjeta: NO requerida

2. Millas + Plata (Pago Mixto)
   → Pago: MILLAS (slider) + PLATA (tarjeta en checkout)
   → Emisión: AUTOMÁTICA
   → Tarjeta: REQUERIDA
   → Estado: EMITIDA inmediatamente tras la compra

3. Solo Plata (0% millas)
   → ❌ NO PERMITIDO (slider tiene mínimo obligatorio)
```

### MÍNIMOS POR SLIDER:

**IMPORTANTE:** Los mínimos son **configurables desde el Admin MRS** por cada cliente.

**Valores de referencia comunes:**
```
• Vuelos: Configurable (ejemplo común: 2000 millas)
• Hoteles: Configurable (ejemplo común: 2000 millas)
• Autos: Configurable (ejemplo común: 2000 millas)
• Actividades: Configurable (ejemplo común: 2000 millas)
• Disney: Configurable (ejemplo común: 2000 millas)
```

⚠️ **Nota:** Validar el mínimo configurado en el Admin MRS del cliente correspondiente antes de ejecutar casos de prueba.

### EMISIÓN:

**Solo Millas (100%):**
- **Automática** (estado EMITIDA inmediato)
- Sin intervención manual

**Millas + Plata (mixto):**
- **Automática** (estado EMITIDA inmediato)
- Sin intervención manual
- Débito de millas y cobro en tarjeta procesados automáticamente

---

## 📦 ESTRUCTURA DE PROVEEDORES

```
MASTERCARD REDEMPTION SYSTEM (MRS)
├─ 🛫 VUELOS
│  ├─ AGGREGATOR - NETACTICA (sin dispersión)
│  ├─ AGGREGATOR - SABRE (sin dispersión)
│  └─ SABRE EDIFACT (sin dispersión de fondos)
│
├─ 🚗 AUTOS
│  ├─ Proveedor: Sabre
│  └─ Empresas: Hertz, Dollar, Thrifty
│
├─ 🏨 HOTELES
│  └─ Hotel Sabre
│
├─ 🎢 ACTIVIDADES
│  └─ HotelBeds
│
└─ 🎠 DISNEY
   └─ OffLine
```

---

## 📝 FORMATO DE TÍTULO ESPECÍFICO MRS

```
[MRS] [Producto] - [Escenario] - [Variante] - [Modelo de pago] - [Proveedor si aplica] - [Cliente]
```

**Ejemplos:**
```
✅ [MRS] Vuelos - Solo ida - AGGREGATOR NETACTICA - Solo Millas automático - Austro
✅ [MRS] Vuelos - Ida y vuelta - SABRE EDIFACT - Millas + Plata manual - Ficsa Honduras
✅ [MRS] Hoteles - 3 noches - HotelBeds - Solo Millas automático - Coopenae
✅ [MRS] Autos - 5 días - Hertz - Millas + Plata manual - Ficsa Guatemala
```

**URLs de login por cliente:**
```
Austro (Ecuador):    https://austec.smartlinks.dev/es-ec
Ficsa (Honduras):    https://ficsahonduras.smartlinks.dev/es-hn
Ficsa (Guatemala):   https://ficsaguatemala.smartlinks.dev/es-gt
Ficsa (Panamá):      https://ficsapanama.smartlinks.dev/es-pa
Ficsa (Nicaragua):   https://ficsanicaragua.smartlinks.dev/es-ni
Coopenae (C. Rica):  https://cpn-mrs.smartlinks.dev/es-cr
Testing:             https://skynet-mc-test.smartlinks.dev
Demo:                https://demo-skynet-mc.smartlinks.dev
```

**Campos adicionales MRS:**
- Payment Model: [Millas | Millas + Plata]
- Proveedor: [Según producto]
- Cliente: [Austro | Ficohsa | Coopenae]

---

## ✅ VALIDACIONES COMUNES A TODOS LOS PRODUCTOS

### SLIDER DE PAGO (crítico):
✅ Validar que el slider esté visible en disponibilidad  
✅ Validar mínimo configurado en el Admin MRS del cliente  
✅ Validar que NO permita bajar del mínimo configurado  
✅ Validar que se pueda mover el slider para seleccionar millas  
✅ Validar cálculo: Total = Millas + Plata  
✅ Validar que el slider funcione correctamente  
⚠️ Consultar configuración actual antes de validar límites  

### CHECKOUT:
✅ Campos obligatorios completos  
✅ Tarjeta solo si es Millas + Plata  
✅ Términos y condiciones aceptados  
✅ Botón de compra habilitado solo con campos completos  
✅ Cálculo visible: débito de millas seleccionadas en slider  

### CONFIRMACIÓN:
✅ Código de reserva visible  
✅ Resumen de pagos (millas y/o plata)  
✅ Valores consistentes con checkout  

### ADMIN:
✅ Reserva localizable por código  
✅ Valores coinciden con confirmación  
✅ Solo Millas: Estado EMITIDA automáticamente  
✅ Millas + Plata: Estado EMITIDA automáticamente  
✅ Validar débito de millas y cobro en tarjeta procesados correctamente  

### CANCELACIÓN (Reservas ya emitidas):
✅ Reserva en estado EMITIDA  
✅ Opción de cancelación visible en admin (según políticas del producto)  
✅ Confirmar cancelación  
✅ Validar devolución automática de millas (según políticas)  
✅ Validar reverso de cobro en tarjeta si aplica (según políticas)  
✅ Validar estado CANCELADO  

### INTEGRIDAD DE DATOS:
✅ Consistencia entre todas las pantallas  
✅ Millas y plata calculadas correctamente  
✅ Fechas correctas en todo el flujo  
✅ Proveedor correcto según producto  
✅ Cliente correcto (Austro, Ficohsa, Coopenae)  

### IMPORTANTE:
⚠️ En MRS NO se valida ni calcula fees de procesamiento  
⚠️ Todos los cálculos se basan en: Millas y/o Plata  
⚠️ Cada cliente tiene su propio portal con URL específica  

---

## 🔍 PROCESO DE CANCELACIÓN DETALLADO

### Escenario: Cancelación de reserva EMITIDA (Solo Millas o Millas + Plata)

**Pasos del proceso:**

1. **Estado inicial:** Reserva en EMITIDA tras compra (emisión automática)
2. **Ingreso admin:** Acceder al administrador MRS del cliente correspondiente
3. **Búsqueda:** Localizar reserva por código
4. **Cancelación:** Click en opción "Cancelar" desde admin (según políticas del producto)
5. **Confirmación:** Confirmar la acción de cancelación
6. **Validación automática:** Sistema devuelve millas a la cuenta del usuario (según políticas)
7. **Reverso de pago:** Si fue Millas + Plata, reversar cobro en tarjeta (según políticas)
8. **Estado final:** Reserva queda en estado CANCELADO

**Validaciones críticas:**
✅ Reserva estaba en estado EMITIDA  
✅ Millas devueltas automáticamente al saldo (según políticas de cancelación)  
✅ Cobro en tarjeta reversado si aplica (según políticas)  
✅ Reserva queda en estado CANCELADO  
✅ Usuario puede usar las millas nuevamente (si se devolvieron)  

---

## 📊 MATRIZ DE MODELOS DE PAGO

| Producto | Mínimo Slider | Solo Millas | Millas + Plata | Emisión Solo Millas | Emisión Mixta |
|----------|---------------|-------------|----------------|---------------------|---------------|
| Vuelos | Config Admin (2000 por lo general) | ✅ | ✅ | Automática | Automática |
| Hoteles | Config Admin (2000 por lo general) | ✅ | ✅ | Automática | Automática |
| Autos | Config Admin (2000 por lo general) | ✅ | ✅ | Automática | Automática |
| Actividades | Config Admin (2000 por lo general) | ✅ | ✅ | Automática | Automática |
| Disney | Config Admin (2000 por lo general) | ✅ | ✅ | Automática | Automática |

---

**NOTA FINAL:**  
Este documento establece las reglas base para MRS (Mastercard Redemption System). Para flujos detallados por producto, consultar los archivos individuales:
- MRS_VUELOS.md
- MRS_HOTELES.md
- MRS_AUTOS.md
- MRS_ACTIVIDADES.md
- MRS_DISNEY.md

**CLIENTES Y PORTALES MRS:**
- 🏦 **Austro** (Ecuador): Portal dedicado para Banco Austro
- 🏦 **Ficsa** (Multi-país): Honduras, Guatemala, Panamá, Nicaragua
- 🏦 **Coopenae** (Costa Rica): Portal dedicado para cooperativa Coopenae
- 🧪 **Testing/Demo**: Ambientes de pruebas y demostración
