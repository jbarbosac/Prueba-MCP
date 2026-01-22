# 📋 [CCOP] DISNEY - Consolidación COP

> Documentación específica para el producto DISNEY (Tickets parques Disney) en Consolidación COP (Colombia).

---

## 🎯 IDENTIFICACIÓN

**Producto:** Disney (Tickets parques Disney)  
**Portal:** Consolidación COP  
**País:** Colombia  
**Prefijo:** [CCOP]  
**Framework:** [React / Angular / Otro - A DEFINIR]  
**Estado:** 🔄 PENDIENTE DEFINICIÓN  

---

## 📦 PROVEEDORES

### **Proveedor Principal**
- **Nombre:** [DerbySoft / OffLine / Otro - A DEFINIR]
- **Tecnología:** [API REST / Integración específica / Manual]
- **Parques disponibles:**
  - Magic Kingdom
  - Epcot
  - Hollywood Studios
  - Animal Kingdom
  - [OTROS - A DEFINIR]
- **Características:**
  - Tickets de 1 a 10+ días
  - Opciones Park Hopper (múltiples parques en mismo día)
  - Tickets con fecha específica vs flexibles
  - [OTRAS - A DEFINIR]

### **Proveedores Adicionales**
- [A DEFINIR si existen otros proveedores]

---

## 💰 MODELO DE PAGO

**Ecuación de pago:**
```
[A DEFINIR]
Ejemplo:
Producto (tickets Disney) = 100% MILLAS/PUNTOS
O
Producto (tickets Disney) = X% MILLAS + Y% COP
Fee = [SÍ/NO]
```

**Componentes:**
- **Producto:** [100% Millas / Mixto / 100% Efectivo - A DEFINIR]
- **Fee:** [Sí / No] - [Descripción del fee si aplica]
- **Tarjeta requerida:** [Sí / No]
- **Slider:** [Sí / No] - [Rango mínimo/máximo si aplica]

**Validaciones de pago:**
- Validar saldo suficiente antes de compra
- Validar tarjeta si requiere fee o pago efectivo
- [VALIDACIÓN 3 - A DEFINIR]

---

## 🔄 FLUJO DE COMPRA

### **1. BÚSQUEDA/SELECCIÓN**

**Campos obligatorios:**
- Tipo de ticket (Magic Kingdom, Epcot, Hollywood Studios, Animal Kingdom, Multi-parque)
- Número de días (1 día, 2 días, 3 días, etc.)
- Fecha de visita (si es ticket con fecha específica)
- Número de tickets por categoría:
  - Adultos (10+ años)
  - Niños (3-9 años)
  - Infantes (0-2 años - típicamente gratis)
- Park Hopper: Sí / No (opción múltiples parques)

**Validaciones:**
- Fecha de visita no puede ser anterior a hoy
- Fecha debe estar dentro del rango permitido (típicamente hasta 1 año)
- Número de tickets válido (mínimo 1)
- [OTRAS - A DEFINIR]

### **2. RESULTADOS/OPCIONES**

**Información mostrada:**
- Tipo de ticket seleccionado
- Número de días
- Precio por categoría (adulto/niño)
- Precio total en [MILLAS/COP - según modelo]
- Beneficios incluidos (ej: Park Hopper, Memory Maker)
- Términos y condiciones
- Política de cancelación

**Opciones adicionales:**
- Memory Maker (fotos ilimitadas)
- Dining Plan
- [OTRAS - A DEFINIR]

### **3. DETALLE Y SELECCIÓN**

**Información del ticket:**
- Descripción completa del parque
- Atracciones incluidas
- Horarios del parque
- Restricciones (altura, edad, etc.)
- Política de uso (fechas, validez)
- Política de cancelación/cambios
- Términos y condiciones

**Validaciones:**
- Disponibilidad confirmada para fecha seleccionada
- Precio bloqueado temporalmente
- [OTRAS - A DEFINIR]

### **4. CHECKOUT**

**Campos del formulario:**
- Datos por cada visitante:
  - Nombre completo - Obligatorio
  - Fecha de nacimiento - Obligatorio
  - Documento de identidad - Obligatorio
- Email de contacto - Obligatorio
- Teléfono de contacto - Obligatorio
- Datos de tarjeta (si requiere fee o pago efectivo) - Según modelo
- Aceptación términos y condiciones Disney - Obligatorio
- [OTROS - A DEFINIR]

**Validaciones críticas:**
- Nombre coincide con documento
- Edad coherente con categoría seleccionada (adulto/niño)
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
Sistema genera vouchers/tickets
       ↓
Estado: EMITIDA/CONFIRMADA
       ↓
Email con vouchers enviado
```

**Estados posibles:**
- PENDIENTE - Compra creada, emisión pendiente
- CONFIRMADA - Tickets confirmados
- EMITIDA - Tickets emitidos listos para usar
- CANCELADA - Compra cancelada
- ERROR - Error en proceso
- [OTROS - A DEFINIR]

---

## ✅ VALIDACIONES CRÍTICAS

### **Validación 1: Edad del Visitante**
- **Cuándo:** En checkout
- **Qué valida:** Edad del visitante coincide con categoría de ticket comprada
- **Mensaje de error:** "La edad del visitante [Nombre] no coincide con la categoría de ticket [Adulto/Niño]"
- **Comportamiento esperado:** No permitir continuar si hay inconsistencia

### **Validación 2: Fecha de Visita Válida**
- **Cuándo:** En selección de fecha
- **Qué valida:** Fecha está disponible y dentro del rango permitido
- **Mensaje de error:** "La fecha seleccionada no está disponible. Por favor elige otra fecha."
- **Comportamiento esperado:** Mostrar calendario solo con fechas disponibles

### **Validación 3: Saldo Suficiente**
- **Cuándo:** Antes de confirmar compra
- **Qué valida:** Usuario tiene saldo suficiente para total de tickets
- **Mensaje de error:** "Saldo insuficiente. Tu saldo actual es [X] [MILLAS/PUNTOS] y necesitas [Y] [MILLAS/PUNTOS]"
- **Comportamiento esperado:** No permitir continuar sin saldo suficiente

### **Validación 4: Datos Coinciden con Documento**
- **Cuándo:** En checkout
- **Qué valida:** Nombres ingresados son válidos para generación de tickets
- **Mensaje de error:** "Verifica que los nombres coincidan con el documento de identidad"
- **Comportamiento esperado:** Validar formato y caracteres permitidos

---

## 🎯 CASOS DE PRUEBA TIPO

### **Formato de título:**
```
[CCOP] Disney - {Escenario} - {Proveedor} - {Variante}
```

### **Ejemplos:**

**Caso positivo básico:**
```
[CCOP] Disney - Compra exitosa 1 día - [Proveedor] - Magic Kingdom 1 adulto
[CCOP] Disney - Compra exitosa múltiples días - [Proveedor] - 3 días Park Hopper
```

**Caso con variantes:**
```
[CCOP] Disney - Compra con slider mixto - [Proveedor] - Millas + COP
[CCOP] Disney - Compra múltiples visitantes - [Proveedor] - 2 adultos 2 niños
```

**Caso negativo:**
```
[CCOP] Disney - Validación edad incorrecta - [Proveedor] - Adulto con edad niño
[CCOP] Disney - Validación saldo insuficiente - [Proveedor]
```

---

## 📝 TEMPLATE DE CASO DE PRUEBA

### **Título:**
```
[CCOP] Disney - Compra exitosa 3 días Park Hopper - [PROVEEDOR] - 2 adultos
```

### **Pasos:**
```
1. **PRECONDICIONES:**
   - Usuario autenticado en portal Consolidación COP
   - Usuario con saldo suficiente: [CANTIDAD] [MILLAS/PUNTOS/COP]
   - Framework: [React/Angular/Otro]

2. **PASO:** Ingresar a sección Disney
   - **RESULTADO ESPERADO:** Se muestra catálogo de tickets Disney disponibles

3. **PASO:** Seleccionar tipo de ticket:
   - Parque: Todos los parques (Park Hopper)
   - Número de días: 3 días
   - Fecha de visita: [Fecha +15 días]
   - Adultos: 2
   - Niños: 0
   - Park Hopper: Sí
   - **RESULTADO ESPERADO:** Se muestra precio y detalles del ticket seleccionado

4. **PASO:** Revisar detalle del ticket:
   - Precio por adulto: [X] [MILLAS/COP]
   - Total (2 adultos): [Y] [MILLAS/COP]
   - Beneficios: Acceso a 4 parques Disney por 3 días
   - **RESULTADO ESPERADO:** Información completa y clara del ticket

5. **PASO:** Hacer clic en "Continuar" o "Comprar"
   - **RESULTADO ESPERADO:** Se carga checkout con formulario de visitantes

6. **PASO:** Completar datos del visitante 1:
   - Nombre: Juan Pérez
   - Fecha nacimiento: 01/01/1990 (34 años - Adulto)
   - Documento: 1234567890
   - **RESULTADO ESPERADO:** Datos se validan correctamente como adulto

7. **PASO:** Completar datos del visitante 2:
   - Nombre: María López
   - Fecha nacimiento: 15/06/1992 (33 años - Adulto)
   - Documento: 9876543210
   - **RESULTADO ESPERADO:** Datos se validan correctamente como adulto

8. **PASO:** Completar datos de contacto:
   - Email: juan.perez@email.com
   - Teléfono: +57 300 1234567
   - **RESULTADO ESPERADO:** Datos validados correctamente

9. **PASO:** [SI APLICA SLIDER] Ajustar slider de pago:
   - Configuración: [X%] Millas + [Y%] COP
   - **RESULTADO ESPERADO:** Cálculo se actualiza dinámicamente

10. **PASO:** [SI REQUIERE TARJETA] Ingresar datos de tarjeta:
    - Número: 4111111111111111
    - Vencimiento: 12/27
    - CVV: 123
    - **RESULTADO ESPERADO:** Tarjeta validada correctamente

11. **PASO:** Aceptar términos y condiciones Disney y confirmar compra
    - **RESULTADO ESPERADO:** 
      - Se muestra pantalla de confirmación
      - Estado: [EMITIDA/CONFIRMADA según modelo]
      - Se envían 2 vouchers/tickets digitales a juan.perez@email.com
      - Vouchers incluyen: código QR, fecha visita, nombres visitantes
      - Se descuentan [CANTIDAD] [MILLAS/PUNTOS] o se procesa pago
      - Instrucciones de uso de tickets incluidas

12. **PASO:** Validar en admin Consolidación COP que la compra:
    - Estado: [EMITIDA/CONFIRMADA según modelo]
    - Proveedor: [PROVEEDOR]
    - Tipo ticket: 3 días Park Hopper
    - Fecha visita: [Fecha seleccionada]
    - Visitantes: 
      - Juan Pérez - Doc 1234567890 - Adulto
      - María López - Doc 9876543210 - Adulto
    - Monto: [CANTIDAD] [MILLAS/PUNTOS/COP]
    - Vouchers generados correctamente
    - **RESULTADO ESPERADO:** Toda la información es correcta y trazable
```

---

## 🚨 CASOS EDGE Y ERRORES COMUNES

### **Error 1: Edad No Coincide con Categoría**
- **Escenario:** Usuario compra ticket adulto pero ingresa fecha nacimiento de niño
- **Causa:** Inconsistencia entre categoría pagada y edad real
- **Mensaje esperado:** "La edad del visitante no coincide con la categoría de ticket comprada"
- **Acción QA:** Validar que detecta la inconsistencia y no permite continuar

### **Error 2: Fecha No Disponible**
- **Escenario:** Usuario selecciona fecha en que parque está cerrado
- **Causa:** Fecha blackout o mantenimiento del parque
- **Mensaje esperado:** "La fecha seleccionada no está disponible. Por favor elige otra fecha."
- **Acción QA:** Validar que calendario solo muestra fechas disponibles

### **Error 3: Saldo Insuficiente**
- **Escenario:** Usuario intenta comprar tickets sin saldo suficiente
- **Causa:** Saldo menor al precio total de tickets
- **Mensaje esperado:** "Saldo insuficiente. Tu saldo actual es [X] millas y necesitas [Y] millas"
- **Acción QA:** Validar que mensaje es claro y no permite continuar

### **Error 4: Voucher No Generado**
- **Escenario:** Pago exitoso pero falla generación de voucher
- **Causa:** Error de integración con proveedor
- **Mensaje esperado:** "Tu compra se procesó correctamente. Los vouchers llegarán a tu email en máximo 24 horas."
- **Acción QA:** Validar que compra queda en estado pendiente y se puede regenerar

### **Error 5: Email No Recibido**
- **Escenario:** Vouchers generados pero email no llega
- **Causa:** Error en envío de email, email inválido, spam
- **Mensaje esperado:** "Puedes descargar tus tickets desde 'Mis Compras'"
- **Acción QA:** Validar que hay método alternativo para obtener tickets

---

## 🔍 PARTICULARIDADES DEL PROVEEDOR

### **[PROVEEDOR - A DEFINIR]**
- Tickets son vouchers digitales con código QR
- Se pueden usar en cualquier entrada del parque
- No son reembolsables una vez emitidos
- Válidos solo para la fecha específica (si aplica)
- Park Hopper permite múltiples parques después de las 2:00 PM
- Infantes (0-2 años) entran gratis, no requieren ticket
- [OTRAS PARTICULARIDADES - A DEFINIR]

---

## 📊 MATRIZ DE CASOS RECOMENDADA

| Escenario | Parque | Variante | Prioridad | Complejidad |
|-----------|--------|----------|-----------|-------------|
| Compra 1 día Magic Kingdom | Magic Kingdom | 1 adulto | Alta | Baja |
| Compra múltiples días | Todos | 3 días Park Hopper 2 adultos | Alta | Media |
| Compra familia | Todos | 2 adultos 2 niños | Alta | Media |
| Validación edad incorrecta | Cualquiera | Adulto con edad niño | Alta | Baja |
| Validación saldo insuficiente | Cualquiera | Cualquier configuración | Alta | Baja |
| Compra con slider mixto | Cualquiera | Millas + COP | Alta | Alta |
| Compra con opciones adicionales | Cualquiera | Memory Maker incluido | Media | Media |
| Cancelación de tickets | Cualquiera | Según políticas | Media | Alta |
| Modificación de fecha | Cualquiera | Según políticas | Media | Alta |
| Compra tickets larga duración | Todos | 10 días | Baja | Media |

**Total casos recomendados:** 10-12 casos mínimos

---

## 🔗 REFERENCIAS

**Reglas comunes:**
- [CCOP_COMMON_RULES.md](../../../shared/Kepler/CCOP_COMMON_RULES.md)
- [SHARED_QA_RULES.md](../../../shared/SHARED_QA_RULES.md)

**Agente especializado:**
- [CCOP_QA_Assistant.agent.md](../../../agents/CCOP_QA_Assistant.agent.md)

**Azure DevOps:**
- Test Plan: [planId a definir]
- Test Suite Disney: [suiteId a definir]

---

## 📝 NOTAS DE IMPLEMENTACIÓN

**Estado:** 🔄 PENDIENTE DEFINICIÓN

**Pendientes:**
- [ ] Confirmar proveedor específico (DerbySoft/OffLine/Otro)
- [ ] Definir framework tecnológico (React/Angular/Otro)
- [ ] Definir modelo de pago exacto (slider, fee, tarjeta)
- [ ] Definir tipo de emisión (automática/manual)
- [ ] Confirmar parques Disney disponibles
- [ ] Definir opciones adicionales (Memory Maker, Dining Plan)
- [ ] Definir política de cancelación/modificación
- [ ] Crear matriz de casos de prueba completa
- [ ] Configurar suiteId "Disney" en Azure DevOps
- [ ] Validar con equipo de desarrollo
- [ ] Validar políticas con PO/PM y Disney

**Última actualización:** 2026-01-22  
**Responsable:** [A DEFINIR]
