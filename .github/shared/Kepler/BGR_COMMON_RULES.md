# 📋 REGLAS COMUNES BGR (BGR Miles)

Documento de referencia con reglas, validaciones y estructura compartida para todos los productos de BGR.

---

## 🎯 IDENTIFICACIÓN Y ALCANCE

**Portal:** https://bgrmiles-ec.preprodppm.com/  
**País:** Ecuador  
**Prefijo obligatorio:** [BGR]  

**Productos disponibles:**
- ✅ Vuelos
- ✅ Hoteles
- ✅ Autos
- ✅ Actividades
- ✅ Tickets Disney

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
   → Emisión: SEMIAUTOMÁTICA (manual)
   → Tarjeta: REQUERIDA
   → Proceso admin: Debitar millas → Emitir en cash

3. Solo Plata (0% millas)
   → ❌ NO PERMITIDO (slider tiene mínimo obligatorio)
```

### MÍNIMOS POR SLIDER:

```
• Vuelos: 2875 millas mínimo
• Hoteles: 20% del total de millas
• Autos: 20% del total de millas
• Actividades: 20% del total de millas
• Disney: 20% del total de millas
```

### EMISIÓN:

**Solo Millas (100%):**
- **Automática** (estado EMITIDA inmediato)
- Sin intervención manual

**Millas + Plata (mixto):**
- **Semiautomática** (requiere proceso manual)
- Pasos:
  1. Reserva queda en estado PENDIENTE
  2. Ingresar al admin BGR
  3. Buscar y abrir reserva
  4. Debitar millas manualmente
  5. Emitir en cash
  6. Estado final: EMITIDA

---

## 📦 ESTRUCTURA DE PROVEEDORES

```
BGR MILES (BGR)
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
│  └─ HotelBeds
│
├─ 🎢 ACTIVIDADES
│  └─ HotelBeds
│
└─ 🎠 DISNEY
   └─ OffLine
```

---

## � FORMATO DE TÍTULO ESPECÍFICO BGR

```
[BGR] [Producto] - [Escenario] - [Variante] - [Modelo de pago] - [Proveedor si aplica]
```

**Ejemplos:**
```
✅ [BGR] Vuelos - Solo ida - AGGREGATOR NETACTICA - Solo Millas automático
✅ [BGR] Vuelos - Ida y vuelta - SABRE EDIFACT - Millas + Plata manual
✅ [BGR] Hoteles - 3 noches - HotelBeds - Solo Millas automático
✅ [BGR] Autos - 5 días - Hertz - Millas + Plata manual
```

**URL de login:**
```
https://bgrmiles-ec.preprodppm.com/
```

**Campos adicionales BGR:**
- Payment Model: [Millas | Millas + Plata]
- Proveedor: [Según producto]

---

## ✅ VALIDACIONES COMUNES A TODOS LOS PRODUCTOS

### SLIDER DE PAGO (crítico):
✅ Validar que el slider esté visible en disponibilidad  
✅ Validar mínimo por producto (vuelos 2875 millas, otros 20%)  
✅ Validar que NO permita bajar del mínimo  
✅ Validar que se pueda mover el slider para seleccionar millas  
✅ Validar cálculo: Total = Millas + Plata  
✅ Validar que el slider funcione correctamente  

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
✅ Millas + Plata: Estado PENDIENTE → proceso manual  

### PROCESO MANUAL (Millas + Plata):
✅ Ingresar al admin BGR  
✅ Buscar reserva por código  
✅ Abrir reserva  
✅ Debitar millas manualmente  
✅ Emitir en cash  
✅ Validar estado EMITIDA  

### CANCELACIÓN (Millas + Plata sin emitir):
✅ Reserva en estado PENDIENTE  
✅ Opción de cancelación visible en admin  
✅ Confirmar cancelación  
✅ Validar devolución automática de millas  
✅ Validar saldo actualizado del usuario  
✅ Validar estado CANCELADO  

### INTEGRIDAD DE DATOS:
✅ Consistencia entre todas las pantallas  
✅ Millas y plata calculadas correctamente  
✅ Fechas correctas en todo el flujo  
✅ Proveedor correcto según producto  

### IMPORTANTE:
⚠️ En BGR NO se valida ni calcula fees de procesamiento  
⚠️ Todos los cálculos se basan en: Millas y/o Plata  

---

## 🔍 PROCESO DE CANCELACIÓN DETALLADO

### Escenario: Cancelación de reserva Millas + Plata SIN emisión

**Pasos del proceso:**

1. **Estado inicial:** Reserva en PENDIENTE tras compra con Millas + Plata
2. **Ingreso admin:** Acceder al administrador BGR
3. **Búsqueda:** Localizar reserva por código
4. **Cancelación:** Click en opción "Cancelar" desde admin
5. **Confirmación:** Confirmar la acción de cancelación
6. **Validación automática:** Sistema devuelve millas a la cuenta del usuario
7. **Estado final:** Reserva queda en estado CANCELADO

**Validaciones críticas:**
✅ No se debitan millas (nunca se ejecutó el débito)  
✅ No se emite en cash (nunca se realizó emisión)  
✅ Millas devueltas automáticamente al saldo original  
✅ Reserva queda en estado CANCELADO  
✅ Usuario puede usar las millas nuevamente  

---

## 📊 MATRIZ DE MODELOS DE PAGO

| Producto | Mínimo Slider | Solo Millas | Millas + Plata | Emisión Solo Millas | Emisión Mixta |
|----------|---------------|-------------|----------------|---------------------|---------------|
| Vuelos | 2875 millas | ✅ | ✅ | Automática | Manual |
| Hoteles | 20% | ✅ | ✅ | Automática | Manual |
| Autos | 20% | ✅ | ✅ | Automática | Manual |
| Actividades | 20% | ✅ | ✅ | Automática | Manual |
| Disney | 20% | ✅ | ✅ | Automática | Manual |

---

**NOTA FINAL:**  
Este documento establece las reglas base para BGR. Para flujos detallados por producto, consultar los archivos individuales:
- BGR_VUELOS.md
- BGR_HOTELES.md
- BGR_AUTOS.md
- BGR_ACTIVIDADES.md
- BGR_DISNEY.md
