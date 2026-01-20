# 📋 REGLAS COMUNES CME (ClubMiles Ecuador)

Documento de referencia con reglas, validaciones y estructura compartida para todos los productos de ClubMiles Ecuador.

---

## 🎯 IDENTIFICACIÓN Y ALCANCE

**Nombre completo:** ClubMiles Ecuador (CME)  
**Portal Test:** https://clubmiles-ec.developppm.com/  
**Portal Demo:** https://clubmiles-ec.preprodppm.com/  
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
❌ Mostrar CheckOut con pop-up sobrepuesto indicando:
"Debe comprar más Millas para poder reservar este producto"
- CheckOut se muestra de fondo con gris transparente
- Pop-up sobrepuesto impide interactuar con el CheckOut
- No se puede hacer clic en el fondo para continuar
```

**ESCENARIO 3:** Millas suficientes (≥ 100% del producto)
```
✅ Mostrar Slider en CheckOut
- Permitir ajuste manual desde el mínimo (20%) hasta el 100% del producto
- Socio decide cuántas Millas usar y cuánto pagar en USD
```

**ESCENARIO 4:** Pago 100% con Solo Millas (sin USD)
```
✅ Socio tiene Millas suficientes y elige pagar 100% en Millas
- Ajustar slider al 100% del valor del producto
- No se cobra nada en USD (excepto fee de vuelos si aplica)
- No se usa Tarjeta de Crédito para el producto (solo para fee de vuelos si aplica)
- Reserva y emisión automática sin Copago
```

### ECUACIÓN DE PAGO POR PRODUCTO:

**VUELOS:**
```
Producto = Millas o Millas+Plata (Slider en CheckOut)
Fee de procesamiento = TARJETA DE CRÉDITO (obligatorio)
  - Formulario de TC dentro del CheckOut (NO lightbox)
  - Al reservar: Conexión bash a PlacetoPay (sin interfaz visual)
Pasarela: PlacetoPay (bash, sin mostrar interfaz)
```

**OTROS PRODUCTOS (Hoteles, Autos, Actividades, Disney):**
```
Producto = Millas o Millas+Plata (Slider en CheckOut)
Sin fee
Pasarela: PlacetoPay (bash, solo si hay Copago, sin mostrar interfaz)
  - Conexión bash al reservar
  - No se muestra interfaz de pasarela de pago
```

---

## 🔐 AUTENTICACIÓN Y NAVEGACIÓN

### PORTAL DE AUTENTICACIÓN:
- Inicia desde el **portal del Cliente PPM** (fuera de control de UltraGroup)
- **URL Test:** https://clubmiles-ec.developppm.com/
- **URL Demo:** https://clubmiles-ec.preprodppm.com/

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

**PANTALLAS ESPECÍFICAS POR PRODUCTO:**
Consultar archivos detallados de cada producto para pantallas exclusivas (Resumen, Modales, etc.)

**NOTAS:**
- **Home:** Controlada por el Cliente PPM (fuera de UltraGroup)
- **Resto de pantallas:** Desarrolladas y mantenidas por UltraGroup

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
2. Cobro en Tarjeta de Crédito (USD) vía PlacetoPay (bash, sin interfaz)
3. Emisión automática tipo "Cash"

### EMISIÓN:
- **Automática** (estado EMITIDA inmediato)
- No requiere intervención manual
- Sin proceso semiautomático

### CONSULTA EN ADMINISTRADOR:
- **Todas las reservas emitidas** se pueden consultar en el **Administrador del modelo CME**
- Se visualiza el detalle completo de la reserva emitida
- Estado: EMITIDA

### VOUCHERS EN ADMIN:
- **Vuelos:** Disponible (excepto vuelos+seguro)
- **Autos:** Solo para Hertz
- **Disney:** Bilingüe (Español/Inglés)
- **Hoteles y Actividades:** No disponible

**Detalle específico por producto:** Ver archivo correspondiente (CME_VUELOS.md, CME_AUTOS.md, etc.)

---

## 📦 ESTRUCTURA DE PROVEEDORES

```
CLUB MILES ECUADOR (CME)
├─ 🛫 VUELOS [Angular]
│  ├─ Sabre Edifact
│  ├─ Aggregator - Sabre NDC
│  └─ Aggregator - Netactica
│
├─ 🚗 AUTOS [Meteor]
│  └─ Sabre Edifact → Hertz, Dollar, Thrifty
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
- ✅ `[CME] Vuelos - Ida y vuelta - Sabre Edifact - Fee con formulario CheckOut`
- ✅ `[CME] Hoteles - 2 noches - HotelBeds - Cancelación gratuita`
- ✅ `[CME] Autos - Dropoff diferente - Hertz - 5 días - Voucher disponible`

**URLs de login:**
```
Test: https://clubmiles-ec.developppm.com/
Demo: https://clubmiles-ec.preprodppm.com/
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
✅ **Formulario TC en CheckOut:** Para fee de vuelos, validar formulario dentro del CheckOut (NO lightbox)  
✅ **PlacetoPay bash:** Validar conexión bash sin interfaz visual en vuelos (fee) y copago (todos)  
✅ **Copago:** Si aplica, validar descuento en PlacetoPay bash y emisión correcta  
✅ **OTP:** Si aplica, validar Modal OTP y flujo completo  
✅ **Navegación sin login:** Búsqueda y Disponibilidad accesibles sin autenticación  
✅ **Bloqueo post-Disponibilidad:** Solicitar login antes de continuar al Checkout  
✅ **Vouchers en Admin:** Validar disponibilidad según producto (Vuelos, Autos Hertz, Disney bilingüe)

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

## 🧪 ESCENARIOS DE PRUEBA COMUNES

**VALIDACIONES GENERALES (Aplican a todos los productos):**
- ✅ Solo Millas (100%) vs Millas+Plata (Copago con slider)
- ✅ Slider en CheckOut: Mínimo 20%, máximo 100% o Millas disponibles
- ✅ Cálculo dinámico en tiempo real al mover slider
- ✅ PlacetoPay bash (si hay Copago, sin interfaz visual)
- ✅ Modal OTP (si tarjeta requiere OTP en Copago)
- ✅ Escenarios 1-4 de redención según Millas disponibles
- ✅ Navegación sin login (hasta Disponibilidad)
- ✅ Emisión automática tipo "Cash"
- ✅ Consulta en Admin con estado EMITIDA

**ESCENARIOS ESPECÍFICOS POR PRODUCTO:**
Ver archivos detallados:
- 🛫 [CME_VUELOS.md](../../products/B2B2C/PPM/CME/CME_VUELOS.md) - Incluye fee, seguro, vouchers, 3 proveedores
- 🏨 [CME_HOTELES.md](../../products/B2B2C/PPM/CME/CME_HOTELES.md) - Habitaciones, cancelaciones, sin voucher
- 🚗 [CME_AUTOS.md](../../products/B2B2C/PPM/CME/CME_AUTOS.md) - Dropoff, rentadoras, voucher Hertz
- 🎢 [CME_ACTIVIDADES.md](../../products/B2B2C/PPM/CME/CME_ACTIVIDADES.md) - Tours, excursiones, sin voucher
- 🎡 [CME_DISNEY.md](../../products/B2B2C/PPM/CME/CME_DISNEY.md) - Parques, voucher bilingüe

---

## 🚨 REGLAS CRÍTICAS ESPECÍFICAS CME

1. **Inicio obligatorio desde login** en todos los flujos
2. **Prefijo [CME]** obligatorio en todos los títulos de casos de prueba
3. **URLs correctas:** Test: https://clubmiles-ec.developppm.com/ | Demo: https://clubmiles-ec.preprodppm.com/
4. **Métodos de pago:** "Solo Millas" (100%) o "Millas+Plata" (Copago con Slider)
5. **Slider en CheckOut:** Visible solo en CheckOut, mínimo 20% para todos los productos
6. **Mínimo de Millas:** Siempre validar lógica del 20% del valor del producto (slider)
7. **Ajuste manual:** El socio ajusta el porcentaje de Millas mediante slider
8. **Pasarela de pago:** PlacetoPay bash (sin interfaz visual) para fee de vuelos y copago
9. **Fee solo en Vuelos:** Formulario TC en CheckOut (NO lightbox) + PlacetoPay bash
10. **Emisión automática:** Siempre, sin intervención manual, tipo "Cash"
11. **Validación en admin:** Siempre incluir pasos de validación en admin CME
12. **Vouchers en Admin:** Validar según producto (Vuelos, Autos Hertz, Disney bilingüe)
13. **Proveedor correcto:** Validar respuesta del proveedor correspondiente
14. **Modal OTP:** Solo aparece si hay Copago y la tarjeta requiere OTP
15. **Navegación sin login:** Permitido hasta Disponibilidad, bloqueado después

---

## 📚 ARCHIVOS RELACIONADOS

**Reglas compartidas:**
- [SHARED_QA_RULES.md](../SHARED_QA_RULES.md) - Fundamentos ISTQB y Azure DevOps

**Flujos por producto:**
- [CME_VUELOS.md](../../products/B2B2C/PPM/CME/CME_VUELOS.md)
- [CME_HOTELES.md](../../products/B2B2C/PPM/CME/CME_HOTELES.md)
- [CME_AUTOS.md](../../products/B2B2C/PPM/CME/CME_AUTOS.md)
- [CME_ACTIVIDADES.md](../../products/B2B2C/PPM/CME/CME_ACTIVIDADES.md)
- [CME_DISNEY.md](../../products/B2B2C/PPM/CME/CME_DISNEY.md)

---

**Última actualización:** 2026-01-08  
**Versión:** 2.3.0  
**Mantenido por:** QA Team Ultragroup  
**Actualización:** Optimización del archivo - Información genérica común mantenida aquí, detalles específicos de productos movidos a archivos individuales. Eliminada dispersión de fondos. Estructura modular para evitar duplicación.
