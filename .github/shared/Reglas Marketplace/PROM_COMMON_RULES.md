# 📋 REGLAS COMUNES PROMERICA REWARDS (PROM)

Documento de referencia con reglas, validaciones y estructura compartida para todos los productos de Promerica Rewards.

---

## 🎯 IDENTIFICACIÓN Y ALCANCE

**Portal (Test CR):** https://traveltest-club-promerica.preprodppm.com/es-cr  
**URL Base (Test):** https://traveltest-club-promerica.preprodppm.com  
**País activo (Test):** Costa Rica (CR)  
**Prefijo obligatorio:** [PROM]

**Moneda del programa:** **Puntos** (no “Millas”)  
**Copago:** **Plata** (tarjeta) cuando aplique

**Productos disponibles:**

- ✅ Vuelos
- ✅ Hoteles
- ✅ Autos
- ✅ Actividades
- ✅ Tickets Disney

---

## 💰 MODELO DE NEGOCIO

**✅ Modelo confirmado (PROM): Puntos + Plata (Slider)**

### Ecuación de pago (conceptual)

```
Total = Puntos + Plata
```

### Reglas confirmadas

- El usuario ajusta la combinación **Puntos/Plata** mediante **slider**.
- Si hay **copago en Plata**, se requiere **método de pago (tarjeta)**.
- El sistema debe validar **saldo de Puntos** antes de permitir continuar.

### Reglas pendientes (NO asumir)

- **Porcentaje mínimo de Puntos** permitido por producto.
- **Fórmula exacta** de conversión Puntos↔Plata (por proveedor/producto).
- **Emisión** (automática vs manual/condicional) según combinación de pago.
- **Fees** por producto (si existen).

**Política anti-suposición (crítica):** si algo está marcado como _pendiente/por confirmar_, el agente QA debe **preguntar** o **dejarlo como TBD**; no “completar con defaults” ni extrapolar desde PM/BGR/CME.

---

## 📦 ESTRUCTURA DE PROVEEDORES

> Los proveedores son por producto y pueden variar por país. Si no está confirmado, mantenerlo como _pendiente_.

```
PROMERICA REWARDS (PROM)
├─ 🛫 VUELOS
│  └─ Proveedores: ⚠️ Pendiente confirmar (posibles: AGGREGATOR NETACTICA, AGGREGATOR SABRE, SABRE EDIFACT)
│
├─ 🚗 AUTOS
│  └─ Proveedores: ✅ Sabre (Hertz, Dollar, Thrifty)
│
├─ 🏨 HOTELES
│  └─ Proveedores: ✅ HotelBeds
│
├─ 🎢 ACTIVIDADES
│  └─ Proveedores: ✅ HotelBeds
│
└─ 🎡 DISNEY
   └─ Proveedores: ⚠️ Pendiente confirmar (referencias: DerbySoft u OffLine)
```

---

## 🏷️ FORMATO DE TÍTULO ESPECÍFICO PROM

```
[PROM] [Producto] - [Escenario] - [Variante] - [Proveedor si aplica]
```

**Ejemplos:**

```
✅ [PROM] Vuelos - Ida y vuelta - SABRE - 1 adulto clase económica
✅ [PROM] Hoteles - 3 noches - HotelBeds - 2 habitaciones
✅ [PROM] Autos - 5 días - Hertz - Dropoff diferente
✅ [PROM] Actividades - Tour - HotelBeds - 4 personas
✅ [PROM] Disney - Parques - DerbySoft - 2 adultos 1 niño
```

**URL de login (Test CR):** https://traveltest-club-promerica.preprodppm.com/es-cr

---

## ✅ VALIDACIONES COMUNES A TODOS LOS PRODUCTOS

### VALIDACIONES BÁSICAS

✅ **Integridad de datos:** Consistencia entre todas las pantallas del flujo  
✅ **Campos obligatorios:** Validación completa antes de habilitar botón de compra  
✅ **Links funcionales:** Términos y condiciones, tratamiento de datos abren correctamente  
✅ **Estados de reserva:** Confirmada en admin con todos los datos completos  
✅ **Proveedor:** Confirmación correcta del proveedor correspondiente  
✅ **Cálculo correcto:** Puntos/Plata calculados correctamente

### VALIDACIONES ESPECÍFICAS (Modelo Slider Puntos + Plata)

✅ Validar visibilidad y funcionalidad del slider  
✅ Validar mínimo por producto (**pendiente**: solicitar valor)  
✅ Validar cálculo dinámico: Puntos + Plata = Total  
✅ Validar solicitud de tarjeta cuando hay copago  
✅ Validar emisión automática vs manual (**pendiente**: confirmar regla)

---

## 🔄 PROCESO DE EMISIÓN

⚠️ **Pendiente confirmar para PROM** (no asumir):

- Estados posibles (ej: EMITIDA / PENDIENTE / EN PROCESO)
- Reglas de emisión según combinación Puntos/Plata
- SLAs y validación en Admin

---

## 🎯 CRITERIOS DE ACEPTACIÓN GENERALES

Mientras se completa la documentación específica, aplicar estos criterios base:

### FLUJO COMPLETO E2E:

✅ Login exitoso  
✅ Navegación correcta al producto  
✅ Búsqueda funcional con validación de campos  
✅ Disponibilidad muestra resultados correctos  
✅ Detalle con información completa  
✅ Checkout con campos obligatorios validados  
✅ Confirmación con código de reserva  
✅ Reserva visible en admin con datos correctos

### CÁLCULOS:

✅ Puntos/Plata calculados correctamente  
✅ Valores consistentes en todas las pantallas  
✅ Resumen final coincide con selección

### USABILIDAD:

✅ Botones habilitados solo con campos completos  
✅ Mensajes de error claros y específicos  
✅ Navegación intuitiva entre pantallas

---

## 🧾 GLOSARIO (PROM)

- **Puntos:** moneda de redención PROM.
- **Plata:** monto en moneda local/currency cobrado a tarjeta cuando hay copago.
- **Slider:** control para ajustar Puntos/Plata.

Regla: en títulos/pasos para PROM usar **Puntos** (no “Millas”).

---

## 📊 MATRIZ DE PRODUCTOS (Template)

| Producto    | Proveedor                          | Tecnología | Mínimo Puntos | Emisión      | Fee          |
| ----------- | ---------------------------------- | ---------- | ------------- | ------------ | ------------ |
| Vuelos      | ⚠️ Pendiente confirmar             | [DEFINIR]  | ⚠️ Pendiente  | ⚠️ Pendiente | ⚠️ Pendiente |
| Hoteles     | ✅ HotelBeds                       | [DEFINIR]  | ⚠️ Pendiente  | ⚠️ Pendiente | No           |
| Autos       | ✅ Sabre (Hertz/Dollar/Thrifty)    | [DEFINIR]  | ⚠️ Pendiente  | ⚠️ Pendiente | No           |
| Actividades | ✅ HotelBeds                       | [DEFINIR]  | ⚠️ Pendiente  | ⚠️ Pendiente | No           |
| Disney      | ⚠️ Pendiente (DerbySoft u OffLine) | [DEFINIR]  | ⚠️ Pendiente  | ⚠️ Pendiente | No           |

---

## 📝 CAMPOS ESPECÍFICOS AZURE DEVOPS

**Campos adicionales para casos de Promerica:**

```yaml
Area Path: ultragroupla\Kepler
Iteration Path: ultragroupla\[DEFINIR SPRINT] # No hardcodear; solicitar al usuario si no se provee
Tags: PROM, Promerica, [PRODUCTO], [PROVEEDOR]
```

---

## 🚀 PRÓXIMOS PASOS PARA COMPLETAR

1. ✅ **Definir URL del portal**
2. ✅ **Definir país(es) de operación**
3. ✅ **Confirmar y documentar reglas del slider:** mínimo, fórmula, emisión
4. ✅ **Documentar proveedores por producto**
5. ✅ **Definir tipo de emisión** (automática/manual/condicional)
6. ✅ **Validar si maneja fees** (solo vuelos o ninguno)
7. ✅ **Completar flujos E2E** por producto
8. ✅ **Realizar pruebas piloto** de generación de casos

---

## 📚 ARCHIVOS RELACIONADOS

**Flujos por producto (completar):**

- [PROM_VUELOS.md](../../products/B2B2C/PPM/PROM/PROM_VUELOS.md)
- [PROM_HOTELES.md](../../products/B2B2C/PPM/PROM/PROM_HOTELES.md)
- [PROM_AUTOS.md](../../products/B2B2C/PPM/PROM/PROM_AUTOS.md)
- [PROM_ACTIVIDADES.md](../../products/B2B2C/PPM/PROM/PROM_ACTIVIDADES.md)
- [PROM_DISNEY.md](../../products/B2B2C/PPM/PROM/PROM_DISNEY.md)

**Agente:**

- [PROM_QA_Assistant.agent.md](../../agents/PROM_QA_Assistant.agent.md)

**Documentación:**

- [PROM/README.md](../../docs/B2B2C/PPM/PROM/README.md)

---

**Última actualización:** 2026-01-23  
**Versión:** 0.2  
**Estado:** 🔄 Parcial (modelo confirmado; reglas finas y emisión pendientes)  
**Responsable:** Equipo QA Célula Kepler
