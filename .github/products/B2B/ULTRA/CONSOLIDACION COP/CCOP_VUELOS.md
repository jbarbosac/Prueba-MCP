# 📋 [CCOP] VUELOS - Consolidación COP

> Documentación específica para el producto VUELOS en Consolidación COP (Colombia).

---

## 🎯 IDENTIFICACIÓN

**Producto:** Vuelos  
**Portal:** Consolidación COP  
**País:** Colombia  
**Prefijo:** [CCOP]  
**Framework:** [Angular / React / Otro - A DEFINIR]  
**Estado:** 🔄 PENDIENTE DEFINICIÓN  

---

## 📦 PROVEEDORES

### **Proveedor Principal - AGGREGATOR NETACTICA** (Ejemplo)
- **Nombre:** [A DEFINIR]
- **Tecnología:** [API REST / SOAP / Otro]
- **Características:**
  - [CARACTERÍSTICA 1 - ej: Múltiples aerolíneas]
  - [CARACTERÍSTICA 2 - ej: Búsqueda en tiempo real]
  - [CARACTERÍSTICA 3 - ej: Sin dispersión]

### **Proveedores Adicionales**
- **AGGREGATOR SABRE:** [A DEFINIR si aplica]
- **SABRE EDIFACT:** [A DEFINIR si aplica]
- **Otros:** [A DEFINIR]

---

## 💰 MODELO DE PAGO

**Ecuación de pago:**
```
[A DEFINIR]
Ejemplo:
Producto = X% MILLAS/PUNTOS + Y% COP
Fee de procesamiento = [SÍ/NO]
```

**Componentes:**
- **Producto:** [100% Millas / Mixto / 100% Efectivo - A DEFINIR]
- **Fee:** [Sí / No] - [Descripción del fee si aplica]
- **Tarjeta requerida:** [Sí / No]
- **Slider:** [Sí / No] - [Rango mínimo/máximo si aplica]

**Validaciones de pago:**
- Validar saldo suficiente antes de búsqueda
- [VALIDACIÓN 2 - A DEFINIR]
- [VALIDACIÓN 3 - A DEFINIR]

---

## 🔄 FLUJO DE COMPRA

### **1. BÚSQUEDA**

**Campos obligatorios:**
- Origen (ciudad/aeropuerto)
- Destino (ciudad/aeropuerto)
- Fecha de ida
- Tipo de viaje (ida/ida y vuelta)
- Número de pasajeros (adultos/niños/infantes)

**Validaciones:**
- Fecha de ida no puede ser anterior a hoy
- Fecha de vuelta debe ser posterior a fecha de ida
- Número de pasajeros válido (máximo típicamente 9)
- Origen y destino no pueden ser iguales

### **2. RESULTADOS**

**Información mostrada:**
- Aerolínea
- Número de vuelo
- Horarios (salida/llegada)
- Duración
- Escalas
- Precio en [MILLAS/COP - según modelo]
- Clase de servicio

**Filtros disponibles:**
- Por aerolínea
- Por número de escalas
- Por horario
- Por precio
- [OTROS - A DEFINIR]

### **3. DETALLE Y SELECCIÓN**

**Información del vuelo:**
- Detalles completos del itinerario
- Política de equipaje
- Términos y condiciones
- Política de cambios/cancelación
- Servicios incluidos

**Validaciones:**
- Disponibilidad confirmada antes de continuar
- Precio bloqueado temporalmente
- [OTRAS - A DEFINIR]

### **4. CHECKOUT**

**Campos del formulario:**
- Datos del pasajero (nombre, apellido, documento, fecha nacimiento) - Obligatorio
- Email de contacto - Obligatorio
- Teléfono de contacto - Obligatorio
- Datos de tarjeta (si requiere fee o pago efectivo) - Según modelo
- Aceptación términos y condiciones - Obligatorio
- [OTROS - A DEFINIR]

**Validaciones críticas:**
- Formato de documento válido
- Edad del pasajero válida según categoría (adulto/niño/infante)
- Email válido
- Teléfono válido
- Tarjeta válida (si aplica)
- Saldo suficiente (si aplica millas/puntos)

### **5. EMISIÓN**

**Tipo de emisión:** [Automática / Manual / Semiautomática - A DEFINIR]

**Flujo:**
```
[A DEFINIR - Ejemplo:]
Usuario confirma compra
       ↓
Sistema procesa pago
       ↓
Sistema emite ticket
       ↓
Estado: EMITIDA
       ↓
Email de confirmación enviado
```

**Estados posibles:**
- PENDIENTE - Reserva creada, pago pendiente
- PAGADA - Pago procesado, emisión pendiente
- EMITIDA - Ticket emitido exitosamente
- CANCELADA - Reserva cancelada
- ERROR - Error en proceso
- [OTROS - A DEFINIR]

---

## ✅ VALIDACIONES CRÍTICAS

### **Validación 1: Saldo de Millas/Puntos**
- **Cuándo:** Antes de búsqueda y antes de confirmar compra
- **Qué valida:** Usuario tiene saldo suficiente para el vuelo seleccionado
- **Mensaje de error:** "Saldo insuficiente. Tu saldo actual es [X] [MILLAS/PUNTOS] y necesitas [Y] [MILLAS/PUNTOS]"
- **Comportamiento esperado:** No permitir continuar si saldo insuficiente

### **Validación 2: Disponibilidad del Vuelo**
- **Cuándo:** Al seleccionar vuelo y antes de checkout
- **Qué valida:** Vuelo sigue disponible al precio cotizado
- **Mensaje de error:** "Lo sentimos, este vuelo ya no está disponible. Por favor realiza una nueva búsqueda."
- **Comportamiento esperado:** Redirigir a resultados o búsqueda

### **Validación 3: Datos del Pasajero**
- **Cuándo:** En checkout
- **Qué valida:** Nombres coinciden con formato pasaporte/documento, edad coherente
- **Mensaje de error:** Específico por campo (ej: "El formato del nombre no es válido")
- **Comportamiento esperado:** Resaltar campo con error, no permitir continuar

### **Validación 4: Política de Equipaje**
- **Cuándo:** En detalle y checkout
- **Qué valida:** Usuario está informado de la política de equipaje incluida
- **Mensaje de error:** N/A (informativo)
- **Comportamiento esperado:** Mostrar claramente equipaje de mano y bodega incluido

---

## 🎯 CASOS DE PRUEBA TIPO

### **Formato de título:**
```
[CCOP] Vuelos - {Escenario} - {Proveedor} - {Variante}
```

### **Ejemplos:**

**Caso positivo básico:**
```
[CCOP] Vuelos - Compra exitosa ida - [Proveedor] - 1 adulto nacional
[CCOP] Vuelos - Compra exitosa ida y vuelta - [Proveedor] - 2 adultos internacional
```

**Caso con variantes:**
```
[CCOP] Vuelos - Compra con slider mixto - [Proveedor] - Millas + COP
[CCOP] Vuelos - Compra con fee procesamiento - [Proveedor] - Tarjeta crédito
```

**Caso negativo:**
```
[CCOP] Vuelos - Validación saldo insuficiente - [Proveedor]
[CCOP] Vuelos - Validación vuelo no disponible - [Proveedor]
```

---

## 📝 TEMPLATE DE CASO DE PRUEBA

### **Título:**
```
[CCOP] Vuelos - Compra exitosa ida y vuelta - [PROVEEDOR] - 1 adulto nacional
```

### **Pasos:**
```
1. **PRECONDICIONES:**
   - Usuario autenticado en portal Consolidación COP
   - Usuario con saldo suficiente: [CANTIDAD] [MILLAS/PUNTOS/COP]
   - Framework: [Angular/React/Otro]

2. **PASO:** Ingresar a sección Vuelos
   - **RESULTADO ESPERADO:** Se muestra formulario de búsqueda con campos obligatorios

3. **PASO:** Completar búsqueda con:
   - Origen: Bogotá (BOG)
   - Destino: Cartagena (CTG)
   - Fecha ida: [Fecha +7 días]
   - Fecha vuelta: [Fecha +14 días]
   - Pasajeros: 1 adulto
   - **RESULTADO ESPERADO:** Se muestran resultados de vuelos disponibles del proveedor [PROVEEDOR]

4. **PASO:** Seleccionar vuelo de ida:
   - Aerolínea: [Aerolínea disponible]
   - Horario: [Horario disponible]
   - Precio: [X] [MILLAS/PUNTOS/COP]
   - **RESULTADO ESPERADO:** Vuelo de ida se agrega al itinerario

5. **PASO:** Seleccionar vuelo de vuelta:
   - Aerolínea: [Aerolínea disponible]
   - Horario: [Horario disponible]
   - Precio: [Y] [MILLAS/PUNTOS/COP]
   - **RESULTADO ESPERADO:** Se muestra resumen completo del itinerario (ida + vuelta)

6. **PASO:** Hacer clic en "Continuar" o "Reservar"
   - **RESULTADO ESPERADO:** Se carga checkout con formulario de pasajero y resumen

7. **PASO:** Completar datos del pasajero:
   - Nombre: Juan
   - Apellido: Pérez
   - Documento: 1234567890
   - Fecha nacimiento: 01/01/1990
   - Email: juan.perez@email.com
   - Teléfono: +57 300 1234567
   - **RESULTADO ESPERADO:** Todos los campos se validan correctamente

8. **PASO:** [SI APLICA SLIDER] Ajustar slider de pago:
   - Configuración: [X%] Millas + [Y%] COP
   - **RESULTADO ESPERADO:** Cálculo se actualiza dinámicamente mostrando desglose

9. **PASO:** [SI REQUIERE TARJETA] Ingresar datos de tarjeta de crédito:
   - Número: 4111111111111111
   - Vencimiento: 12/27
   - CVV: 123
   - **RESULTADO ESPERADO:** Datos se validan y se acepta la tarjeta

10. **PASO:** Aceptar términos y condiciones y confirmar compra
    - **RESULTADO ESPERADO:** 
      - Se muestra pantalla de confirmación con PNR
      - Estado de reserva: [EMITIDA/PENDIENTE según modelo]
      - Se envía email de confirmación a juan.perez@email.com
      - Se descuentan [CANTIDAD] [MILLAS/PUNTOS] o se cobra tarjeta
      - Reserva visible en "Mis Reservas"

11. **PASO:** Validar en admin Consolidación COP que la reserva:
    - Estado: [EMITIDA/PENDIENTE según modelo]
    - Proveedor: [PROVEEDOR]
    - Itinerario: BOG-CTG (ida) / CTG-BOG (vuelta)
    - Pasajero: Juan Pérez - Doc 1234567890
    - Monto: [CANTIDAD] [MILLAS/PUNTOS/COP]
    - PNR generado correctamente
    - [SI APLICA] Requiere emisión manual: [Sí/No]
    - **RESULTADO ESPERADO:** Toda la información es correcta y trazable
```

---

## 🚨 CASOS EDGE Y ERRORES COMUNES

### **Error 1: Saldo Insuficiente**
- **Escenario:** Usuario intenta comprar vuelo sin saldo suficiente
- **Causa:** Saldo actual menor al precio del vuelo
- **Mensaje esperado:** "Saldo insuficiente. Tu saldo actual es [X] millas y necesitas [Y] millas"
- **Acción QA:** Validar que el mensaje se muestra y no permite continuar

### **Error 2: Vuelo No Disponible**
- **Escenario:** Vuelo cotizado se agota antes de confirmar compra
- **Causa:** Otro usuario compró el último asiento
- **Mensaje esperado:** "Lo sentimos, este vuelo ya no está disponible. Por favor realiza una nueva búsqueda."
- **Acción QA:** Validar que redirige a resultados y no pierde filtros aplicados

### **Error 3: Datos del Pasajero Inválidos**
- **Escenario:** Usuario ingresa documento con formato incorrecto
- **Causa:** Formato no cumple validación (letras en campo numérico, etc.)
- **Mensaje esperado:** "El formato del documento no es válido"
- **Acción QA:** Validar que resalta el campo en rojo y muestra mensaje específico

### **Error 4: Timeout de Emisión**
- **Escenario:** Proveedor no responde en tiempo esperado
- **Causa:** Problema de conectividad o lentitud del proveedor
- **Mensaje esperado:** "Tu reserva está en proceso. Recibirás un email cuando esté confirmada."
- **Acción QA:** Validar que reserva queda en estado PENDIENTE y se notifica usuario

### **Error 5: Tarjeta Rechazada**
- **Escenario:** Banco rechaza la transacción
- **Causa:** Fondos insuficientes, tarjeta bloqueada, etc.
- **Mensaje esperado:** "Transacción rechazada. Por favor verifica los datos de tu tarjeta."
- **Acción QA:** Validar que no se descuentan millas y se puede reintentar

---

## 🔍 PARTICULARIDADES DEL PROVEEDOR

### **[PROVEEDOR 1 - A DEFINIR]**
- Particularidad 1: [ej: Requiere validación adicional para vuelos internacionales]
- Particularidad 2: [ej: Política de equipaje varía según aerolínea]
- Particularidad 3: [ej: Emisión tarda hasta 2 horas en horario nocturno]

### **[PROVEEDOR 2]** (si aplica)
- Particularidad 1: [A DEFINIR]
- Particularidad 2: [A DEFINIR]

---

## 📊 MATRIZ DE CASOS RECOMENDADA

| Escenario | Proveedor | Variante | Prioridad | Complejidad |
|-----------|-----------|----------|-----------|-------------|
| Compra exitosa ida | [Proveedor 1] | 1 adulto nacional | Alta | Baja |
| Compra exitosa ida y vuelta | [Proveedor 1] | 1 adulto nacional | Alta | Media |
| Compra con múltiples pasajeros | [Proveedor 1] | 2 adultos + 1 niño | Alta | Media |
| Compra vuelo internacional | [Proveedor 1] | 1 adulto | Alta | Media |
| Validación saldo insuficiente | [Proveedor 1] | Cualquier configuración | Alta | Baja |
| Validación vuelo no disponible | [Proveedor 1] | Cualquier configuración | Media | Media |
| Compra con slider mixto | [Proveedor 1] | Millas + COP | Alta | Alta |
| Compra con fee procesamiento | [Proveedor 1] | Tarjeta requerida | Alta | Media |
| Vuelo con múltiples escalas | [Proveedor 1] | 2+ escalas | Media | Media |
| Cambio de vuelo | [Proveedor 1] | Según políticas | Media | Alta |
| Cancelación de vuelo | [Proveedor 1] | Según políticas | Media | Alta |

**Total casos recomendados:** 10-15 casos mínimos

---

## 🔗 REFERENCIAS

**Reglas comunes:**
- [CCOP_COMMON_RULES.md](../../../shared/Kepler/CCOP_COMMON_RULES.md)
- [SHARED_QA_RULES.md](../../../shared/SHARED_QA_RULES.md)

**Agente especializado:**
- [CCOP_QA_Assistant.agent.md](../../../agents/CCOP_QA_Assistant.agent.md)

**Azure DevOps:**
- Test Plan: [planId a definir]
- Test Suite Vuelos: [suiteId a definir]

---

## 📝 NOTAS DE IMPLEMENTACIÓN

**Estado:** 🔄 PENDIENTE DEFINICIÓN

**Pendientes:**
- [ ] Definir proveedor(es) específico(s)
- [ ] Definir framework tecnológico (Angular/React/Otro)
- [ ] Definir modelo de pago exacto (slider, fee, tarjeta)
- [ ] Definir tipo de emisión (automática/manual/semiautomática)
- [ ] Definir validaciones específicas por proveedor
- [ ] Crear matriz de casos de prueba completa
- [ ] Configurar suiteId "Vuelos" en Azure DevOps
- [ ] Validar flujo con equipo de desarrollo
- [ ] Validar políticas con PO/PM

**Última actualización:** 2026-01-22  
**Responsable:** [A DEFINIR]
