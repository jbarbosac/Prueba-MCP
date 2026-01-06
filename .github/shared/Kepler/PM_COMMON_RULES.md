# 📋 REGLAS COMUNES PICHINCHA MILES (PM)

Documento de referencia con reglas, validaciones y estructura compartida para todos los productos de Pichincha Miles.

---

## 🎯 IDENTIFICACIÓN Y ALCANCE

**Portal:** https://pichinchamiles-ec.preprodppm.com/  
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

## ✅ VALIDACIONES COMUNES A TODOS LOS PRODUCTOS

✅ **Integridad de datos:** Consistencia entre todas las pantallas del flujo  
✅ **Campos obligatorios:** Validación completa antes de habilitar botón Canjear  
✅ **Links funcionales:** Términos y condiciones, tratamiento de datos abren correctamente  
✅ **Estados de reserva:** Confirmada en admin con todos los datos completos  
✅ **Emisión automática:** Reserva en estado EMITIDA sin intervención manual  
✅ **Proveedor:** Confirmación correcta del proveedor correspondiente  
✅ **Cálculo correcto:** Millas canjeadas calculadas correctamente según producto
