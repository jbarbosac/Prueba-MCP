# 📋 REGLAS COMUNES PICHINCHA MILES (PM)

Documento de referencia con reglas, validaciones y estructura compartida para todos los productos de Pichincha Miles.

---

## 🎯 IDENTIFICACIÓN Y ALCANCE

**Portal:DEMO** https://pichinchamiles-ec.preprodppm.com/  
**País:** Ecuador  
**Prefijo obligatorio:** [PM]  

**Productos disponibles:**
- ✅ Vuelos (Angular)
- ✅ Hoteles (Angular)
- ✅ Autos (Meteor)
- ✅ Actividades (Angular)
- ✅ Tickets Disney (React)

---

## 💰 MODELO DE NEGOCIO

### ECUACIÓN DE PAGO:

**VUELOS:**
```
Producto = 100% MILLAS
Fee de procesamiento = TARJETA DE CRÉDITO (lightbox)
```

**OTROS PRODUCTOS (Hoteles, Autos, Actividades, Disney):**
```
Producto = 100% MILLAS (Único pago, sin fee, sin tarjeta)
```

### EMISIÓN:
- **Automática** (estado EMITIDA inmediato)
- No requiere intervención manual
- Sin proceso semiautomático

---

## 📦 ESTRUCTURA DE PROVEEDORES

```
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

## � FORMATO DE TÍTULO ESPECÍFICO PM

```
[PM] [Producto] - [Escenario] - [Variante] - [Proveedor si aplica]
```

**Ejemplos:**
- ✅ `[PM] Vuelos - Ida y vuelta - Sabre - Fee con lightbox`
- ✅ `[PM] Hoteles - 2 noches - HotelBeds - Cancelación gratuita`
- ✅ `[PM] Autos - Dropoff diferente - Hertz - 5 días`

**URL de login:**
```
https://pichinchamiles-ec.preprodppm.com/
```

---

## 🎟️ PROMOCODE (CÓDIGO PROMOCIONAL)

### DISPONIBILIDAD POR PRODUCTO:

✅ **VUELOS:** Sí maneja Promocode  
✅ **HOTELES:** Sí maneja Promocode  
❌ **AUTOS:** NO maneja Promocode  
✅ **ACTIVIDADES:** Sí maneja Promocode  
✅ **DISNEY:** Sí maneja Promocode  

### REGLA GENERAL:
```
Todos los productos de PM manejan Promocode EXCEPTO Autos
```

### TIPOS DE DESCUENTO PROMOCODE:

**1️⃣ Descuento Porcentual (%):**
- El descuento se calcula como un porcentaje sobre el valor base
- Ejemplo: 10%, 15%, 20%
- Cálculo: Base × (% descuento)

**2️⃣ Descuento Fijo:**
- El descuento es una cantidad fija de millas
- Ejemplo: 5,000 millas, 10,000 millas
- Se resta directamente del valor base

### VALIDACIONES PROMOCODE:
- ✅ Campo opcional en búsqueda (productos aplicables)
- ✅ Validar código válido/inválido
- ✅ Identificar tipo de descuento (% o fijo)
- ✅ Aplicar descuento según tipo
- ✅ Mostrar descuento aplicado en resumen
- ❌ En Autos: Campo NO existe en el flujo

---

## 💰 MARKUP (IMPUESTO/RECARGO)

### DISPONIBILIDAD POR PRODUCTO:

❌ **VUELOS:** NO maneja Markup  
✅ **HOTELES:** SÍ maneja Markup  
❌ **AUTOS:** NO maneja Markup  
✅ **ACTIVIDADES:** SÍ maneja Markup  
❌ **DISNEY:** NO maneja Markup  

### REGLA GENERAL:
```
SOLO Hoteles y Actividades manejan Markup
```

### ¿QUÉ ES EL MARKUP?

**Markup** es un impuesto o recargo que se cobra **por debajo** en el servicio. Es un costo adicional que se incluye en el precio final pero no es visible directamente para el usuario en el desglose.

### TIPOS DE MARKUP:

**1️⃣ Markup Porcentual (%):**
- Se calcula como un porcentaje sobre el precio base del servicio
- Ejemplo: 5%, 8%, 10%
- Cálculo: Precio base × (% markup)

**2️⃣ Markup Fijo:**
- Es una cantidad fija en millas que se suma al precio
- Ejemplo: 2,000 millas, 3,500 millas
- Se suma directamente al precio base

### CARACTERÍSTICAS DEL MARKUP:

✅ **Se cobra por debajo:** No es visible como línea separada para el usuario  
✅ **Incluido en precio final:** Ya está incorporado en el precio mostrado  
✅ **Aplica en Hoteles y Actividades:** Únicos productos con Markup  
✅ **Puede ser % o fijo:** Según configuración del servicio  
❌ **NO es un fee visible:** Diferente al fee de vuelos  

### EJEMPLO MARKUP:

**Hotel con Markup 8%:**
```
Precio base hotel: 30,000 millas
Markup 8%: 30,000 × 0.08 = 2,400 millas
Precio final mostrado: 32,400 millas
```

**Actividad con Markup fijo:**
```
Precio base actividad: 15,000 millas
Markup fijo: 1,500 millas
Precio final mostrado: 16,500 millas
```

### VALIDACIONES MARKUP:

✅ **Solo en Hoteles y Actividades:** Validar que NO aparece en otros productos  
✅ **Incluido en precio:** El precio mostrado ya incluye el markup  
✅ **Cálculo correcto:** Verificar que el markup esté aplicado correctamente  
✅ **Tipo identificado:** Confirmar si es % o fijo según configuración  

---

## 📍 DROP OFF (CARGO POR DEVOLUCIÓN EN PUNTO DIFERENTE)

### DISPONIBILIDAD POR PRODUCTO:

❌ **VUELOS:** NO aplica Drop off  
❌ **HOTELES:** NO aplica Drop off  
✅ **AUTOS:** SÍ aplica Drop off  
❌ **ACTIVIDADES:** NO aplica Drop off  
❌ **DISNEY:** NO aplica Drop off  

### REGLA GENERAL:
```
SOLO Autos maneja Drop off
```

### ¿QUÉ ES EL DROP OFF?

**Drop off** es un **impuesto o cargo adicional** que se cobra cuando el vehículo se **recoge en un punto** y se **entrega en un punto diferente**.

### CARACTERÍSTICAS DEL DROP OFF:

✅ **Cargo condicional:** Solo aplica cuando recogida ≠ devolución  
✅ **Cobrado en millas:** Se suma al costo base de la renta  
✅ **Pago en punto de entrega:** El Drop off se paga en el punto de devolución del vehículo  
✅ **Visible y desglosado:** Aparece como línea separada en checkout  
✅ **Campo opcional:** Check "Devolución en otro destino"  
✅ **Incluido en total:** Parte de las millas totales canjeadas  
❌ **No aplica mismo destino:** Si recogida = devolución, Drop off = 0  

### FLUJOS:

**Sin Drop off (mismo destino):**
```
Recogida: Madrid Aeropuerto
Devolución: Madrid Aeropuerto
Drop off: NO
Total: Solo costo base
```

**Con Drop off (destino diferente):**
```
Recogida: Madrid Aeropuerto
Devolución: Barcelona Aeropuerto
Drop off: SÍ (cargo adicional)
Total: Costo base + Drop off
```

### EJEMPLO:

**Renta 5 días con Drop off:**
```
Costo base: 25,000 millas
Drop off (Madrid → Barcelona): 8,000 millas
Total: 33,000 millas
```

**Renta 5 días sin Drop off:**
```
Costo base: 25,000 millas
Drop off: 0 millas (mismo destino)
Total: 25,000 millas
```

### VALIDACIONES DROP OFF:

✅ **Campo funcional:** Check "Devolución en otro destino" debe funcionar  
✅ **Cargo visible:** Drop off mostrado en disponibilidad, checkout y confirmación  
✅ **Pago en entrega:** Drop off se paga en el punto de devolución del vehículo  
✅ **Cálculo correcto:** Total = Base + Drop off (cuando aplica)  
✅ **Consistencia:** Drop off igual en todas las pantallas  
✅ **No cobro indebido:** Drop off = 0 cuando recogida = devolución  

### LÓGICA DE CÁLCULO EN VUELOS:

**El Promocode aplica sobre:**
- ✅ Valor del boleto (en millas)
- ✅ Fee oculto (en millas)
- ❌ **NO aplica sobre TA (Tasas Aeroportuarias)**

**Proceso de cálculo:**
```
1. Obtener precio total del vuelo en millas
2. Restar las TA equivalentes (convertidas a puntos/millas)
3. Sobre el valor resultante (Boleto + Fee oculto) aplicar el descuento del Promocode
4. Sumar nuevamente las TA (sin descuento)
5. Resultado final = (Boleto + Fee oculto - descuento Promocode) + TA
```

**Ejemplo 1 - Descuento Porcentual (10%):**
```
Precio total vuelo: 50,000 millas
TA equivalentes: 5,000 millas
Promocode: 10% descuento

1. Base de cálculo = 50,000 - 5,000 = 45,000 millas
2. Descuento = 45,000 × 10% = 4,500 millas
3. Subtotal con descuento = 45,000 - 4,500 = 40,500 millas
4. Total final = 40,500 + 5,000 (TA) = 45,500 millas
```

**Ejemplo 2 - Descuento Fijo (3,000 millas):**
```
Precio total vuelo: 50,000 millas
TA equivalentes: 5,000 millas
Promocode: 3,000 millas descuento fijo

1. Base de cálculo = 50,000 - 5,000 = 45,000 millas
2. Descuento = 3,000 millas (fijo)
3. Subtotal con descuento = 45,000 - 3,000 = 42,000 millas
4. Total final = 42,000 + 5,000 (TA) = 47,000 millas
```

---

## ✅ VALIDACIONES COMUNES A TODOS LOS PRODUCTOS

✅ **Integridad de datos:** Consistencia entre todas las pantallas del flujo  
✅ **Campos obligatorios:** Validación completa antes de habilitar botón Canjear  
✅ **Links funcionales:** Términos y condiciones, tratamiento de datos abren correctamente  
✅ **Estados de reserva:** Confirmada en admin con todos los datos completos  
✅ **Emisión automática:** Reserva en estado EMITIDA sin intervención manual  
✅ **Proveedor:** Confirmación correcta del proveedor correspondiente  
✅ **Cálculo correcto:** Millas canjeadas calculadas correctamente según producto  
✅ **Promocode:** Validar campo según producto (NO aplica en Autos)
