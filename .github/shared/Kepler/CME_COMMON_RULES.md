# 📋 REGLAS COMUNES CME (ClubMiles Ecuador)

Documento de referencia con reglas, validaciones y estructura compartida para todos los productos de ClubMiles Ecuador.

---

## 🎯 IDENTIFICACIÓN Y ALCANCE

**Nombre completo:** ClubMiles Ecuador (CME)  
**Portal:** https://correosmillas-ec.preprodppm.com/  
**País:** Ecuador  
**Prefijo obligatorio:** [CME]  
**Cliente:** PPM (Diners Club a través de PPM)  
**Tipo de negocio:** B2B-B2C (Modelo de lealtad)

**Productos disponibles:**
- ✅ Vuelos (Tickets de vuelos en aerolíneas)
- ✅ Hoteles (Hospedaje en hoteles)
- ✅ Autos (Renta de Autos)
- ✅ Actividades (Diversos planes o actividades para hacer)
- ✅ Tickets Disney (Entradas a Disney)

---

## 🏢 MODELO DE NEGOCIO CME

### CONTEXTO GENERAL:

CME es un **modelo de lealtad** (también llamado marketplace o aplicación de turismo) creado por **UltraGroup** para **PPM**.  

**Cadena de valor:**
1. **UltraGroup** desarrolla y vende CME a → **PPM**
2. **PPM** ofrece CME a → **Diners Club**  
3. **Diners Club** ofrece CME como programa de fidelización a → **Socios/Usuarios finales**

El usuario final es el **Socio** (cliente de Diners Club) que usa "Millas" como moneda de redención para productos de turismo.

---

## 💰 MÉTODOS DE PAGO

### TERMINOLOGÍA:
- **"Puntos"** → En CME se llaman **"Millas"**
- **"Solo Puntos"** → **"Solo Millas"** (100% Millas)
- **"Puntos+Plata"** → **"Millas+Plata"** o **"Copago"**

### REGLA CRÍTICA:
❌ **NO se puede pagar solo con dinero (USD)**

### MÉTODOS DE PAGO DISPONIBLES:

**1. Solo Millas (100% Millas):**
- El socio paga el 100% del producto con Millas
- No se usa tarjeta de crédito (excepto fee en vuelos)

**2. Millas+Plata (Copago):**
- El socio ajusta manualmente la cantidad de Millas mediante **Slider en CheckOut**
- El restante se paga con Tarjeta de Crédito en Dólares (USD)
- Pasarela de pago: **PlacetoPay**

### 🎚️ SLIDER AJUSTABLE EN CHECKOUT:

**Ubicación:** Solo visible en la pantalla **CheckOut** (para todos los productos)

**Configuración:**
- **Mínimo del slider:** 20% del valor del producto (en Millas)
- **Máximo del slider:** 100% del valor del producto (en Millas) o total de Millas disponibles del socio
- **Ajuste:** Manual por parte del socio mediante slider interactivo

**Comportamiento:**
- El socio puede ajustar el porcentaje de Millas entre el mínimo (20%) y el máximo (100% o sus Millas disponibles)
- El sistema calcula automáticamente el valor restante en USD
- Si el socio tiene Millas suficientes, puede elegir pagar 100% en Millas
- Si el socio tiene Millas insuficientes pero ≥ 20%, puede usar el slider para ajustar el Copago

### LÓGICA DE REDENCIÓN:

**Mínimo de Millas configurado:** 20% del valor del producto

**ESCENARIO 1:** Millas insuficientes PERO ≥ 20% del producto
```
✅ Mostrar Slider en CheckOut
- Permitir ajuste manual desde el mínimo (20%) hasta las Millas disponibles del socio
- Cobrar restante en USD con Tarjeta de Crédito vía PlacetoPay
```

**ESCENARIO 2:** Millas insuficientes Y < 20% del producto
```
❌ Mostrar pop-up indicando:
"Debe comprar más Millas para poder reservar este producto"
(No se muestra el CheckOut ni el Slider)
```

**ESCENARIO 3:** Millas suficientes (≥ 100% del producto)
```
✅ Mostrar Slider en CheckOut
- Permitir ajuste manual desde el mínimo (20%) hasta el 100% del producto
- Socio decide cuántas Millas usar y cuánto pagar en USD
```

### ECUACIÓN DE PAGO POR PRODUCTO:

**VUELOS:**
```
Producto = Millas o Millas+Plata
Fee de procesamiento = TARJETA DE CRÉDITO (obligatorio en lightbox)
Pasarela: PlacetoPay
```

**OTROS PRODUCTOS (Hoteles, Autos, Actividades, Disney):**
```
Producto = Millas o Millas+Plata
Sin fee
Pasarela: PlacetoPay (solo si hay Copago)
```

---

## 🔐 AUTENTICACIÓN Y NAVEGACIÓN

### PORTAL DE AUTENTICACIÓN:
- Inicia desde el **portal del Cliente PPM** (fuera de control de UltraGroup)
- URL: https://correosmillas-ec.preprodppm.com/

### PROCESO DE LOGIN:
1. Ingresar número de identificación (ya creado en la agencia)
2. Ingresar contraseña
3. Ingresar código **OTP** enviado al correo del socio

### NAVEGACIÓN SIN LOGIN:
✅ **Permitido:**
- Buscar en pantalla **Home**
- Ver resultados en pantalla **Disponibilidad**
- Consultar precios y recomendaciones

❌ **Bloqueado:**
- Continuar después de Disponibilidad requiere autenticación

---

## 📱 PANTALLAS DEL FLUJO E2E

### PANTALLAS COMUNES (Todos los productos):
1. **Home** (Portal del Cliente PPM) - Búsqueda inicial
2. **Disponibilidad** - Resultados de búsqueda
3. **Checkout** - Información del socio, **Slider Ajustable de Millas** y datos de pago
4. **Modal OTP** (Solo si aplica Copago con tarjeta que requiere OTP)
5. **Confirmación** - Confirmación de reserva

### PANTALLAS EXCLUSIVAS DE VUELOS:
- **Resumen** (Después de Disponibilidad)
- **Modal Seguro de Cancelación** (Si está activo)
- **Modal Previo a Confirmación**
- **Confirmación Vuelos+Seguro** (Si se aceptó el seguro)

### PANTALLAS EXCLUSIVAS DE AUTOS:
- **Modal Previo a Confirmación**

### NOTAS IMPORTANTES:
- **Home:** Controlada por el Cliente PPM (fuera de UltraGroup)
- **Resto de pantallas:** Desarrolladas y mantenidas por UltraGroup

---

## ✈️ SEGURO DE CANCELACIÓN (Solo Vuelos)

**Disponibilidad:** Solo para producto **Vuelos**  
**Momento:** Después de la pantalla **Resumen**

**Flujo:**
1. Se muestra **Modal de Seguro de Cancelación**
2. El socio puede **Aceptar** o **Denegar**
3. Si acepta:
   - Confirmación muestra pantalla especial: **Confirmación Vuelos+Seguro**
   - Incluye información del seguro de cancelación

---

## 🎫 EMISIÓN AUTOMÁTICA

### PROCESO DE EMISIÓN:

**Para TODOS los productos:**
- **Tipo de emisión:** Automática
- **Tipo de pago en backend:** "Cash"
- **Descuento de Millas:** Inmediato al confirmar reserva
- **Estado final:** EMITIDA

**Para Copago (Millas+Plata):**
1. Descuento de Millas
2. Cobro en Tarjeta de Crédito (USD) vía PlacetoPay
3. Emisión automática tipo "Cash"

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
✅ **Emisión automática:** Reserva en estado EMITIDA sin intervención manual, tipo "Cash"  
✅ **Proveedor:** Confirmación correcta del proveedor correspondiente  
✅ **Cálculo correcto:** Millas canjeadas calculadas correctamente según producto  
✅ **Slider en CheckOut:** Visible solo en CheckOut, mínimo 20%, ajuste manual funcional  
✅ **Validación de mínimo:** Lógica del 20% de Millas funcionando correctamente (slider)  
✅ **Cálculo dinámico:** Al mover el slider, actualización automática de Millas y USD  
✅ **Copago:** Si aplica, validar descuento en PlacetoPay y emisión correcta  
✅ **OTP:** Si aplica, validar Modal OTP y flujo completo  
✅ **Navegación sin login:** Búsqueda y Disponibilidad accesibles sin autenticación  
✅ **Bloqueo post-Disponibilidad:** Solicitar login antes de continuar al Checkout

---

## ⚠️ DIFERENCIAS CLAVE CON OTROS PORTALES

**CME vs PM:**
- Marca diferente (Diners Club/Correos Ecuador vs Banco Pichincha)
- Usuario final diferente (clientes de Diners Club vs clientes de Banco Pichincha)
- **CME:** Slider ajustable en CheckOut (mínimo 20%)
- **PM:** Lógica automática (mínimo 20%, sin slider)
- **MISMOS proveedores y tecnologías**
- **MISMA pasarela:** PlacetoPay

**CME vs BGR:**
- **CME:** Slider en CheckOut (mínimo 20% para todos los productos)
- **BGR:** Slider en CheckOut (vuelos: 2875 millas, otros: 20%)
- **CME:** Emisión automática siempre
- **BGR:** Emisión automática (100% millas) o manual (mixto)
- **CME:** Pasarela PlacetoPay
- **BGR:** Pasarela diferente (según configuración)

**Similitud CME = BGR en Slider:**
- Ambos tienen slider ajustable en CheckOut
- Ambos permiten ajuste manual de Millas vs USD
- Diferencia: CME siempre 20% mínimo, BGR varía según producto

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
- Solo Millas vs Millas+Plata (Copago)
- Con Seguro de Cancelación vs Sin Seguro
- Modal OTP (tarjeta que requiere OTP)

**HOTELES:**
- 1 habitación, múltiples habitaciones
- Solo adultos, adultos + menores
- Cancelación gratuita, con cargo, no reembolsable
- Nacional, internacional
- Solo Millas vs Millas+Plata (Copago)

**AUTOS:**
- Pickup y dropoff mismo lugar
- Dropoff diferente
- 1 día, múltiples días
- Diferentes empresas (Hertz, Dollar, Thrifty)
- Solo Millas vs Millas+Plata (Copago)
- Modal Previo a Confirmación

**ACTIVIDADES:**
- Tours, excursiones, traslados
- 1 persona, múltiples personas
- Nacional, internacional
- Solo Millas vs Millas+Plata (Copago)

**DISNEY:**
- 1 día, múltiples días
- Magic Kingdom, Epcot, Hollywood Studios, Animal Kingdom
- 1 persona, múltiples personas
- Solo Millas vs Millas+Plata (Copago)

**VALIDACIONES DE SLIDER Y MÍNIMO DE MILLAS:**
- Slider visible en CheckOut (todos los productos)
- Mínimo del slider: 20% del valor del producto
- Máximo del slider: 100% o Millas disponibles del socio
- Ajuste manual: Mover slider actualiza cálculo Millas/USD en tiempo real
- Socio con ≥ 20% del producto → Mostrar slider en CheckOut, permitir Copago
- Socio con < 20% del producto → Mostrar pop-up, NO mostrar CheckOut
- Validar cálculo correcto al mover slider
- Validar límites del slider (no permitir menos del 20%)

---

## 🚨 REGLAS CRÍTICAS ESPECÍFICAS CME

1. **Inicio obligatorio desde login** en todos los flujos
2. **Prefijo [CME]** obligatorio en todos los títulos de casos de prueba
3. **URL correcta:** https://correosmillas-ec.preprodppm.com/
4. **Métodos de pago:** "Solo Millas" o "Millas+Plata" (Copago con Slider)
5. **Slider en CheckOut:** Visible solo en CheckOut, mínimo 20% para todos los productos
6. **Mínimo de Millas:** Siempre validar lógica del 20% del valor del producto (slider)
7. **Ajuste manual:** El socio ajusta el porcentaje de Millas mediante slider
8. **Pasarela de pago:** PlacetoPay para todos los cobros en USD
9. **Fee solo en Vuelos:** Tarjeta de crédito en lightbox para fee (obligatorio)
10. **Emisión automática:** Siempre, sin intervención manual, tipo "Cash"
11. **Validación en admin:** Siempre incluir pasos de validación en admin CME
12. **Proveedor correcto:** Validar respuesta del proveedor correspondiente
13. **Modal OTP:** Solo aparece si hay Copago y la tarjeta requiere OTP
14. **Navegación sin login:** Permitido hasta Disponibilidad, bloqueado después

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

**Última actualización:** 2026-01-08  
**Versión:** 2.1.0  
**Mantenido por:** QA Team Ultragroup  
**Actualización:** Agregado Slider Ajustable en CheckOut con mínimo del 20% para todos los productos. El socio puede ajustar manualmente la cantidad de Millas a usar mediante slider interactivo.
