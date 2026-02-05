# 📋 REGLAS COMUNES PICHINCHA MILES (PM)

Documento de referencia con reglas, validaciones y estructura compartida para todos los productos de Pichincha Miles.

**Tipo de negocio:** Marketplace B2B2C (Business to Business to Consumer)

---

## 🎯 IDENTIFICACIÓN Y ALCANCE

**Portales:**

- 🧪 **TEST:** https://pichinchamiles-ec.developppm.com/
- 🎯 **DEMO:** https://pichinchamiles-ec.preprodppm.com/

**País:** Ecuador

**Prefijo obligatorio:** [PM]

### Configuración de entornos

#### 🧪 TEST

- **URL:** https://pichinchamiles-ec.developppm.com/
- **Id agencia:** 5699cdf3-89a5-4622-8a1a-b92b1e6b891f
- **Usuario:** ULTRA11111
- **Contraseña:** Ultra1111.

#### 🎯 DEMO

- **URL:** https://pichinchamiles-ec.preprodppm.com/
- **Id agencia:** 63cc18a9-d922-4093-8c2d-5fdbebd0e5ca
- **Usuario:** ULTRA1111
- **Contraseña:** Colombia2024*

#### 📧 VERIFICACIÓN OTP

- Después de ingresar usuario y contraseña, el sistema envía un código OTP al correo
- **Correo OTP:** pruebasotp@ultragroupla.com
- **Contraseña correo:** Smartlinks91
- El código OTP debe ingresarse para completar el login

### Productos disponibles

- ✅ **Vuelos** (Angular)
- ✅ **Hoteles** (Angular)
- ✅ **Autos** (Meteor)
- ✅ **Actividades** (Angular)
- ✅ **Tickets Disney** (React)

---

## 💰 MODELO DE NEGOCIO

### Ecuación de pago

#### VUELOS

```plaintext
Producto = 100% MILLAS
Fee de procesamiento = TARJETA DE CRÉDITO (lightbox)
```

#### OTROS PRODUCTOS (Hoteles, Autos, Actividades, Disney)

```plaintext
Producto = 100% MILLAS (sin fee, sin tarjeta)
```

**NOTA IMPORTANTE:** PM es un modelo de **SOLO MILLAS**. No maneja opción de "Millas + Plata".

### Emisión

- **Automática** (estado EMITIDA inmediato)
- No requiere intervención manual
- Sin proceso semiautomático

---

## 📦 ESTRUCTURA DE PROVEEDORES

```plaintext
PICHINCHA MILES (PM)
├─ 🛫 VUELOS [Angular]
│  ├─ AGGREGATOR - NETACTICA (sin dispersión)
│  ├─ AGGREGATOR - SABRE (sin dispersión)
│  └─ SABRE EDIFACT (con dispersión de fondos)
│
├─ 🚗 AUTOS [Meteor]
│  ├─ Proveedor: Sabre
│  └─ Empresas: Hertz, Dollar, Thrifty
│
├─ 🏨 HOTELES [Angular]
│  └─ HotelBeds
│
├─ 🎢 ACTIVIDADES [Angular]
│  └─ HotelBeds
│
└─ 🎡 DISNEY [React]
   └─ DerbySoft
```

---

## 🏷️ FORMATO DE TÍTULO ESPECÍFICO PM

```plaintext
[PM] [Producto] - [Escenario] - [Variante] - [Proveedor si aplica]
```

**Ejemplos:**

- ✅ `[PM] Vuelos - Ida y vuelta - Sabre - Fee con lightbox`
- ✅ `[PM] Hoteles - 2 noches - HotelBeds - Cancelación gratuita`
- ✅ `[PM] Autos - Dropoff diferente - Hertz - 5 días`

---

## 🎟️ PROMOCODE (CÓDIGO PROMOCIONAL)

### Disponibilidad por producto

- ✅ **VUELOS:** Sí maneja Promocode
- ✅ **HOTELES:** Sí maneja Promocode
- ❌ **AUTOS:** NO maneja Promocode
- ✅ **ACTIVIDADES:** Sí maneja Promocode
- ✅ **DISNEY:** Sí maneja Promocode

### Regla general

```plaintext
Todos los productos de PM manejan Promocode EXCEPTO Autos
```

### Tipos de descuento Promocode

#### 1️⃣ Descuento Porcentual (%)

- El descuento se calcula como un porcentaje sobre el valor base
- **Ejemplo:** 10%, 15%, 20%
- **Cálculo:** Base × (% descuento)

#### 2️⃣ Descuento Fijo

- El descuento es una cantidad fija de millas
- **Ejemplo:** 5,000 millas, 10,000 millas
- Se resta directamente del valor base

### Validaciones Promocode
- ✅ Campo opcional en búsqueda (productos aplicables)
- ✅ Validar código válido/inválido
- ✅ Identificar tipo de descuento (% o fijo)
- ✅ Aplicar descuento según tipo
- ✅ Mostrar descuento aplicado en resumen
- ❌ En Autos: Campo NO existe en el flujo

---

## 💰 MARKUP (IMPUESTO/RECARGO)

### Disponibilidad por producto

- ❌ **VUELOS:** NO maneja Markup
- ✅ **HOTELES:** SÍ maneja Markup
- ❌ **AUTOS:** NO maneja Markup
- ✅ **ACTIVIDADES:** SÍ maneja Markup
- ❌ **DISNEY:** NO maneja Markup

### Regla general

```plaintext
SOLO Hoteles y Actividades manejan Markup
```

### ¿Qué es el Markup?

**Markup** es un impuesto o recargo que se cobra **por debajo** en el servicio. Es un costo adicional que se incluye en el precio final pero no es visible directamente para el usuario en el desglose.

### Tipos de Markup

#### 1️⃣ Markup Porcentual (%)

- Se calcula como un porcentaje sobre el precio base del servicio
- **Ejemplo:** 5%, 8%, 10%
- **Cálculo:** Precio base × (% markup)

#### 2️⃣ Markup Fijo

- Es una cantidad fija en millas que se suma al precio
- **Ejemplo:** 2,000 millas, 3,500 millas
- Se suma directamente al precio base

### Características del Markup

- ✅ **Se cobra por debajo:** No es visible como línea separada para el usuario
- ✅ **Incluido en precio final:** Ya está incorporado en el precio mostrado
- ✅ **Aplica en Hoteles y Actividades:** Únicos productos con Markup
- ✅ **Puede ser % o fijo:** Según configuración del servicio
- ❌ **NO es un fee visible:** Diferente al fee de vuelos

### Ejemplo Markup

#### Hotel con Markup 8%
```plaintext
Precio base hotel: 30,000 millas
Markup 8%: 30,000 × 0.08 = 2,400 millas
Precio final mostrado: 32,400 millas
```

#### Actividad con Markup fijo

```plaintext
Precio base actividad: 15,000 millas
Markup fijo: 1,500 millas
Precio final mostrado: 16,500 millas
```

### Validaciones Markup

- ✅ **Solo en Hoteles y Actividades:** Validar que NO aparece en otros productos
- ✅ **Incluido en precio:** El precio mostrado ya incluye el markup
- ✅ **Cálculo correcto:** Verificar que el markup esté aplicado correctamente
- ✅ **Tipo identificado:** Confirmar si es % o fijo según configuración  

---

## 📍 DROP OFF (CARGO POR DEVOLUCIÓN EN PUNTO DIFERENTE)

### Disponibilidad por producto

- ❌ **VUELOS:** NO aplica Drop off
- ❌ **HOTELES:** NO aplica Drop off
- ✅ **AUTOS:** SÍ aplica Drop off
- ❌ **ACTIVIDADES:** NO aplica Drop off
- ❌ **DISNEY:** NO aplica Drop off

### Regla general

```plaintext
SOLO Autos maneja Drop off
```

### ¿Qué es el Drop off?

**Drop off** es un **impuesto o cargo adicional** que se cobra cuando el vehículo se **recoge en un punto** y se **entrega en un punto diferente**.

### Características del Drop off

- ✅ **Cargo condicional:** Solo aplica cuando recogida ≠ devolución
- ✅ **Cobrado en millas:** Se suma al costo base de la renta
- ✅ **Pago en punto de entrega:** El Drop off se paga en el punto de devolución del vehículo
- ✅ **Visible y desglosado:** Aparece como línea separada en checkout
- ✅ **Campo opcional:** Check "Devolución en otro destino"
- ✅ **Incluido en total:** Parte de las millas totales canjeadas
- ❌ **No aplica mismo destino:** Si recogida = devolución, Drop off = 0

### Flujos

#### Sin Drop off (mismo destino)

```plaintext
Recogida: Madrid Aeropuerto
Devolución: Madrid Aeropuerto
Drop off: NO
Total: Solo costo base
```

#### Con Drop off (destino diferente)

```plaintext
Recogida: Madrid Aeropuerto
Devolución: Barcelona Aeropuerto
Drop off: SÍ (cargo adicional)
Total: Costo base + Drop off
```

### Ejemplo

#### Renta 5 días con Drop off

```plaintext
Costo base: 25,000 millas
Drop off (Madrid → Barcelona): 8,000 millas
Total: 33,000 millas
```

#### Renta 5 días sin Drop off

```plaintext
Costo base: 25,000 millas
Drop off: 0 millas (mismo destino)
Total: 25,000 millas
```

### Validaciones Drop off

- ✅ Campo funcional y cargo visible en todas las pantallas
- ✅ Pago en punto de devolución del vehículo
- ✅ Cálculo correcto: Total = Base + Drop off (cuando aplica)
- ✅ Drop off = 0 cuando recogida = devolución

---

## ✅ VALIDACIONES COMUNES A TODOS LOS PRODUCTOS

- ✅ **Integridad de datos** entre todas las pantallas del flujo
- ✅ **Campos obligatorios** validados antes de habilitar botón Canjear
- ✅ **Links funcionales** (términos, condiciones, tratamiento de datos)
- ✅ **Reserva en estado EMITIDA** sin intervención manual (emisión automática)
- ✅ **Proveedor correcto** confirmado en admin
- ✅ **Cálculo correcto de millas** según producto
- ✅ **Promocode** validar según producto (NO aplica en Autos)
