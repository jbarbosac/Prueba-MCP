# 📋 REGLAS COMUNES CME (Correos Millas Ecuador)

Documento de referencia con reglas, validaciones y estructura compartida para todos los productos de Correos Millas Ecuador.

---

## 🎯 IDENTIFICACIÓN Y ALCANCE

**Portal:** https://correosmillas-ec.preprodppm.com/  
**País:** Ecuador  
**Prefijo obligatorio:** [CME]  

**Productos disponibles:**
- ✅ Vuelos
- ✅ Hoteles
- ✅ Autos
- ✅ Actividades
- ✅ Tickets Disney

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
CORREOS MILLAS ECUADOR (CME)
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

## � FORMATO DE TÍTULO ESPECÍFICO CME

```
[CME] [Producto] - [Escenario] - [Variante] - [Proveedor si aplica]
```

**Ejemplos:**
- ✅ `[CME] Vuelos - Ida y vuelta - Sabre - Fee con lightbox`
- ✅ `[CME] Hoteles - 2 noches - HotelBeds - Cancelación gratuita`
- ✅ `[CME] Autos - Dropoff diferente - Hertz - 5 días`

**URL de login:**
```
https://correosmillas-ec.preprodppm.com/
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

---

## ⚠️ DIFERENCIAS CLAVE CON OTROS PORTALES

**CME vs PM:**
- Marca diferente (Correos del Ecuador vs Banco Pichincha)
- Mismo modelo de negocio (100% Millas)
- Mismos proveedores
- Usuario final diferente (clientes de Correos)

**CME vs BGR:**
- CME: 100% Millas (pago único)
- BGR: Slider Millas + Plata (pago mixto)
- CME: Emisión automática siempre
- BGR: Emisión automática (100% millas) o manual (mixto)

---

## 🔧 TECNOLOGÍAS POR PRODUCTO

| Producto | Tecnología | Framework | Notas |
|----------|-----------|-----------|-------|
| Vuelos | Angular | TypeScript | Mismo módulo que PM |
| Hoteles | Angular | TypeScript | Mismo módulo que PM |
| Autos | Meteor | JavaScript | Mismo módulo que PM |
| Actividades | Angular | TypeScript | Mismo módulo que PM |
| Disney | React | JavaScript/TypeScript | Mismo módulo que PM |

---

## 📸 IMÁGENES DE REFERENCIA

**Estructura de imágenes en .github/images/CME/:**

```
CME/
├── Vuelos/
│   ├── Home-vuelos-CME.png
│   ├── Disponibilidad-vuelos-CME.png
│   ├── Checkout-vuelos-CME.png
│   ├── Lightbox-fee-CME.png
│   ├── Confirmacion-vuelos-CME.png
│   └── Admin.png
│
├── Hoteles/
│   ├── Home-hoteles-CME.png
│   ├── Disponibilidad-hoteles-CME.png
│   ├── Detalle-hotel-CME.png
│   ├── Checkout-hoteles-CME.png
│   ├── Confirmacion-hoteles-CME.png
│   └── Admin.png
│
├── Autos/
│   ├── Home-autos-CME.png
│   ├── Disponibilidad-autos-CME.png
│   ├── Checkout-autos-CME.png
│   ├── Confirmacion-autos-CME.png
│   └── Admin.png
│
├── Actividades/
│   ├── Home-actividades-CME.png
│   ├── Disponibilidad-actividades-CME.png
│   ├── Detalle-actividad-CME.png
│   ├── Checkout-actividades-CME.png
│   ├── Confirmacion-actividades-CME.png
│   └── Admin.png
│
└── Disney/
    ├── Home-disney-CME.png
    ├── Disponibilidad-disney-CME.png
    ├── Checkout-disney-CME.png
    ├── Confirmacion-disney-CME.png
    └── Admin.png
```

---

## 🧪 ESCENARIOS DE PRUEBA RECOMENDADOS

**VUELOS:**
- Ida y vuelta, solo ida, multidestino
- Nacional, internacional
- 1 pasajero, múltiples pasajeros
- Con equipaje, sin equipaje
- Fee en lightbox con tarjeta de crédito

**HOTELES:**
- 1 habitación, múltiples habitaciones
- Solo adultos, adultos + menores
- Cancelación gratuita, con cargo, no reembolsable
- Nacional, internacional

**AUTOS:**
- Pickup y dropoff mismo lugar
- Dropoff diferente
- 1 día, múltiples días
- Diferentes empresas (Hertz, Dollar, Thrifty)

**ACTIVIDADES:**
- Tours, excursiones, traslados
- 1 persona, múltiples personas
- Nacional, internacional

**DISNEY:**
- 1 día, múltiples días
- Magic Kingdom, Epcot, Hollywood Studios, Animal Kingdom
- 1 persona, múltiples personas

---

## 🚨 REGLAS CRÍTICAS ESPECÍFICAS CME

1. **Inicio obligatorio desde login** en todos los flujos
2. **Prefijo [CME]** obligatorio en todos los títulos de casos de prueba
3. **URL correcta:** https://correosmillas-ec.preprodppm.com/
4. **Modelo de pago:** 100% Millas (sin slider, sin pago mixto)
5. **Fee solo en Vuelos:** Tarjeta de crédito en lightbox para fee
6. **Emisión automática:** Siempre, sin intervención manual
7. **Validación en admin:** Siempre incluir pasos de validación en admin CME
8. **Proveedor correcto:** Validar respuesta del proveedor correspondiente

---

## 📚 ARCHIVOS RELACIONADOS

**Reglas compartidas:**
- [SHARED_QA_RULES.md](../SHARED_QA_RULES.md) - Fundamentos ISTQB y Azure DevOps

**Flujos por producto:**
- [CME_VUELOS.md](../../products/Kepler/CME/CME_VUELOS.md)
- [CME_HOTELES.md](../../products/Kepler/CME/CME_HOTELES.md)
- [CME_AUTOS.md](../../products/Kepler/CME/CME_AUTOS.md)
- [CME_ACTIVIDADES.md](../../products/Kepler/CME/CME_ACTIVIDADES.md)
- [CME_DISNEY.md](../../products/Kepler/CME/CME_DISNEY.md)

---

**Última actualización:** 2026-01-06  
**Versión:** 1.0.0  
**Mantenido por:** QA Team Ultragroup
