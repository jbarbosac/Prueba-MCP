# 📋 REGLAS COMUNES PROMERICA REWARDS (PROM)

Documento de referencia con reglas, validaciones y estructura compartida para todos los productos de Promerica Rewards.

---

## 🎯 IDENTIFICACIÓN Y ALCANCE

**Portal:** [PENDIENTE DEFINIR URL]  
**País:** [PENDIENTE DEFINIR]  
**Prefijo obligatorio:** [PROM]  

**Productos disponibles:**
- ✅ Vuelos
- ✅ Hoteles
- ✅ Autos
- ✅ Actividades
- ✅ Tickets Disney

---

## 💰 MODELO DE NEGOCIO

⚠️ **PENDIENTE DE DEFINIR**

### ECUACIÓN DE PAGO:

**OPCIÓN A - Modelo Fijo (como PM):**
```
Producto = 100% MILLAS
Fee (solo vuelos) = TARJETA DE CRÉDITO
Emisión = AUTOMÁTICA
```

**OPCIÓN B - Modelo Slider (como BGR/CME):**
```
Producto = MILLAS + PLATA (ajustable con slider)
Mínimo slider = [DEFINIR: 20% o 2875 millas según producto]
Emisión = AUTOMÁTICA (100% millas) o MANUAL (mixto)
```

**🔍 ACCIÓN REQUERIDA:** Definir cuál modelo aplica para Promerica

---

## 📦 ESTRUCTURA DE PROVEEDORES

⚠️ **PENDIENTE DE DEFINIR**

```
PROMERICA REWARDS (PROM)
├─ 🛫 VUELOS [Tecnología: PENDIENTE]
│  └─ Proveedores: [PENDIENTE DEFINIR]
│
├─ 🚗 AUTOS [Tecnología: PENDIENTE]
│  └─ Proveedores: [PENDIENTE DEFINIR]
│
├─ 🏨 HOTELES [Tecnología: PENDIENTE]
│  └─ Proveedores: [PENDIENTE DEFINIR]
│
├─ 🎢 ACTIVIDADES [Tecnología: PENDIENTE]
│  └─ Proveedores: [PENDIENTE DEFINIR]
│
└─ 🎡 DISNEY [Tecnología: PENDIENTE]
   └─ Proveedores: [PENDIENTE DEFINIR]
```

**🔍 ACCIÓN REQUERIDA:** Documentar proveedores y tecnologías específicas

---

## 🏷️ FORMATO DE TÍTULO ESPECÍFICO PROM

```
[PROM] [Producto] - [Escenario] - [Variante] - [Proveedor si aplica]
```

**Ejemplos (ajustar según modelo definido):**
```
✅ [PROM] Vuelos - Ida y vuelta - SABRE - 1 adulto clase económica
✅ [PROM] Hoteles - 3 noches - HotelBeds - 2 habitaciones
✅ [PROM] Autos - 5 días - Hertz - Dropoff diferente
✅ [PROM] Actividades - Tour - HotelBeds - 4 personas
✅ [PROM] Disney - Parques - DerbySoft - 2 adultos 1 niño
```

**URL de login:**
```
[PENDIENTE DEFINIR]
```

---

## ✅ VALIDACIONES COMUNES A TODOS LOS PRODUCTOS

### VALIDACIONES BÁSICAS (Aplicables mientras se define el modelo):

✅ **Integridad de datos:** Consistencia entre todas las pantallas del flujo  
✅ **Campos obligatorios:** Validación completa antes de habilitar botón de compra  
✅ **Links funcionales:** Términos y condiciones, tratamiento de datos abren correctamente  
✅ **Estados de reserva:** Confirmada en admin con todos los datos completos  
✅ **Proveedor:** Confirmación correcta del proveedor correspondiente  
✅ **Cálculo correcto:** Millas/puntos canjeados calculados correctamente  

### VALIDACIONES ESPECÍFICAS (Dependen del modelo de negocio):

**SI ES MODELO FIJO (100% Millas):**
✅ Validar cálculo de millas por producto  
✅ Validar fee solo en vuelos (si aplica)  
✅ Validar emisión automática inmediata  
✅ Validar que NO se solicite tarjeta (excepto fee vuelos)  

**SI ES MODELO SLIDER (Millas + Plata):**
✅ Validar visibilidad y funcionalidad del slider  
✅ Validar mínimo por producto (definir valores)  
✅ Validar cálculo dinámico: Millas + Plata = Total  
✅ Validar solicitud de tarjeta cuando hay copago  
✅ Validar emisión automática (100% millas) vs manual (mixto)  

---

## 🔄 PROCESO DE EMISIÓN

⚠️ **PENDIENTE DE DEFINIR**

**OPCIÓN A - Emisión Automática (como PM):**
- Estado EMITIDA inmediato
- Sin intervención manual
- Aplica a todos los productos

**OPCIÓN B - Emisión Condicional (como BGR):**
- Automática: 100% millas → Estado EMITIDA inmediato
- Manual: Millas + Plata → Estado PENDIENTE → Proceso manual en admin

**🔍 ACCIÓN REQUERIDA:** Definir tipo de emisión para Promerica

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
✅ Millas/puntos calculados correctamente  
✅ Valores consistentes en todas las pantallas  
✅ Resumen final coincide con selección  

### USABILIDAD:
✅ Botones habilitados solo con campos completos  
✅ Mensajes de error claros y específicos  
✅ Navegación intuitiva entre pantallas  

---

## ⚠️ DIFERENCIAS CON OTROS MODELOS (Actualizar según definición)

### PROM vs PM:
- [PENDIENTE: Documentar diferencias cuando se defina el modelo]

### PROM vs BGR:
- [PENDIENTE: Documentar diferencias cuando se defina el modelo]

### PROM vs CME:
- [PENDIENTE: Documentar diferencias cuando se defina el modelo]

---

## 📊 MATRIZ DE PRODUCTOS (Template)

| Producto | Proveedor | Tecnología | Mínimo Millas | Emisión | Fee |
|----------|-----------|------------|---------------|---------|-----|
| Vuelos | [DEFINIR] | [DEFINIR] | [DEFINIR] | [DEFINIR] | [DEFINIR] |
| Hoteles | [DEFINIR] | [DEFINIR] | [DEFINIR] | [DEFINIR] | No |
| Autos | [DEFINIR] | [DEFINIR] | [DEFINIR] | [DEFINIR] | No |
| Actividades | [DEFINIR] | [DEFINIR] | [DEFINIR] | [DEFINIR] | No |
| Disney | [DEFINIR] | [DEFINIR] | [DEFINIR] | [DEFINIR] | No |

---

## 📝 CAMPOS ESPECÍFICOS AZURE DEVOPS

**Campos adicionales para casos de Promerica:**
```yaml
Area Path: ultragroupla\Kepler
Iteration Path: ultragroupla\[DEFINIR SPRINT]
Tags: PROM, Promerica, [PRODUCTO], [PROVEEDOR]
```

---

## 🚀 PRÓXIMOS PASOS PARA COMPLETAR

1. ✅ **Definir URL del portal**
2. ✅ **Definir país(es) de operación**
3. ✅ **Definir modelo de negocio:**
   - ¿100% Millas (como PM)?
   - ¿Slider Millas + Plata (como BGR/CME)?
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

**Última actualización:** 2026-01-20  
**Versión:** 0.1 (Draft)  
**Estado:** 🔄 Pendiente de definición completa  
**Responsable:** Equipo QA Célula Kepler
