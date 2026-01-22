# 📋 [CCOP] ASISTENCIAS - Consolidación COP

> Documentación específica para el producto ASISTENCIAS DE VIAJE en Consolidación COP (Colombia).

---

## 🎯 IDENTIFICACIÓN

**Producto:** Asistencias de Viaje (Seguros de viaje)  
**Portal:** Consolidación COP  
**País:** Colombia  
**Prefijo:** [CCOP]  
**Framework:** [Angular / React / Otro - A DEFINIR]  
**Estado:** 🔄 PENDIENTE DEFINICIÓN  

---

## 📦 PROVEEDORES

### **Proveedor Principal**
- **Nombre:** [Universal Assistance / Assist Card / Intermundial / Otro - A DEFINIR]
- **Tecnología:** [API REST / Integración específica]
- **Coberturas típicas:**
  - Asistencia médica
  - Cancelación de viaje
  - Pérdida de equipaje
  - Retrasos de vuelos
  - Repatriación
  - [OTRAS - A DEFINIR]
- **Características:**
  - Planes por región (nacional/internacional)
  - Planes por cobertura (básica/premium)
  - Cobertura por días (1-365 días)
  - [OTRAS - A DEFINIR]

### **Proveedores Adicionales**
- [A DEFINIR si existen otros proveedores]

---

## 💰 MODELO DE PAGO

**Ecuación de pago:**
```
[A DEFINIR]
Ejemplo:
Producto (asistencia) = 100% MILLAS/PUNTOS
O
Producto (asistencia) = X% MILLAS + Y% COP
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
- Destino (país/región)
- Fecha de inicio del viaje
- Fecha de fin del viaje
- Número de viajeros por categoría:
  - Adultos (18-69 años típicamente)
  - Adultos mayores (70+ años)
  - Niños/Menores (0-17 años)
- Tipo de plan (básico/premium/personalizado)

**Validaciones:**
- Fecha inicio no puede ser anterior a hoy
- Fecha fin debe ser posterior a inicio
- Duración máxima típicamente 365 días (validar con proveedor)
- Número de viajeros válido
- [OTRAS - A DEFINIR]

### **2. RESULTADOS/OPCIONES**

**Información mostrada:**
- Planes disponibles (básico, plus, premium, etc.)
- Coberturas incluidas por plan:
  - Monto máximo asistencia médica
  - Cobertura cancelación
  - Cobertura equipaje
  - Cobertura COVID-19 (si aplica)
  - Otros beneficios
- Precio por viajero
- Precio total en [MILLAS/COP - según modelo]
- Términos y condiciones
- Política de cancelación

**Comparativa de planes:**
- Tabla comparativa entre planes disponibles
- Destacar diferencias principales
- [OTROS - A DEFINIR]

### **3. DETALLE Y SELECCIÓN**

**Información del plan:**
- Descripción completa de coberturas
- Exclusiones importantes
- Procedimiento para activar asistencia
- Números de emergencia 24/7
- Documentación requerida
- Restricciones por edad
- Cobertura de preexistencias (si aplica)
- Términos y condiciones completos

**Validaciones:**
- Disponibilidad confirmada para fechas y destino
- Precio bloqueado temporalmente
- [OTRAS - A DEFINIR]

### **4. CHECKOUT**

**Campos del formulario:**
- Datos por cada viajero:
  - Nombre completo - Obligatorio
  - Fecha de nacimiento - Obligatorio
  - Documento de identidad - Obligatorio
  - Nacionalidad - Obligatorio
  - Condiciones preexistentes (declaración) - Obligatorio
- Datos de contacto:
  - Email principal - Obligatorio
  - Teléfono móvil - Obligatorio
  - Contacto de emergencia - Obligatorio
- Detalles del viaje:
  - Destino específico - Obligatorio
  - Motivo del viaje (turismo/negocios/otro) - Opcional
- Datos de tarjeta (si requiere fee o pago efectivo) - Según modelo
- Aceptación términos y condiciones - Obligatorio
- [OTROS - A DEFINIR]

**Validaciones críticas:**
- Edad del viajero válida para plan seleccionado
- Declaración de condiciones preexistentes completa
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
Sistema emite póliza
       ↓
Estado: EMITIDA
       ↓
Email con póliza y voucher enviado
```

**Estados posibles:**
- PENDIENTE - Compra creada, emisión pendiente
- EMITIDA - Póliza emitida activa
- ACTIVA - Asistencia vigente (dentro de fechas de viaje)
- VENCIDA - Viaje finalizado
- CANCELADA - Póliza cancelada antes de inicio
- [OTROS - A DEFINIR]

---

## ✅ VALIDACIONES CRÍTICAS

### **Validación 1: Edad del Viajero**
- **Cuándo:** En checkout
- **Qué valida:** Edad del viajero es válida para el plan seleccionado
- **Mensaje de error:** "La edad del viajero [Nombre] requiere un plan específico. Por favor contacta soporte."
- **Comportamiento esperado:** Informar si requiere plan especial (ej: adultos mayores 70+)

### **Validación 2: Duración del Viaje**
- **Cuándo:** En selección de fechas
- **Qué valida:** Duración no excede máximo permitido por plan
- **Mensaje de error:** "La duración máxima para este plan es de [X] días"
- **Comportamiento esperado:** No permitir continuar si excede límite

### **Validación 3: Destino Cubierto**
- **Cuándo:** En selección de destino
- **Qué valida:** Destino está dentro de la cobertura del plan
- **Mensaje de error:** "El destino seleccionado requiere un plan internacional. Precio: [X]"
- **Comportamiento esperado:** Sugerir plan adecuado según destino

### **Validación 4: Declaración de Preexistencias**
- **Cuándo:** En checkout
- **Qué valida:** Usuario completa declaración de condiciones preexistentes
- **Mensaje de error:** "Debes completar la declaración de condiciones de salud"
- **Comportamiento esperado:** No permitir continuar sin completar declaración

---

## 🎯 CASOS DE PRUEBA TIPO

### **Formato de título:**
```
[CCOP] Asistencias - {Escenario} - {Proveedor} - {Variante}
```

### **Ejemplos:**

**Caso positivo básico:**
```
[CCOP] Asistencias - Compra exitosa nacional - [Proveedor] - Plan básico 1 adulto
[CCOP] Asistencias - Compra exitosa internacional - [Proveedor] - Plan premium 2 adultos
```

**Caso con variantes:**
```
[CCOP] Asistencias - Compra con slider mixto - [Proveedor] - Millas + COP
[CCOP] Asistencias - Compra familia - [Proveedor] - 2 adultos 2 niños 7 días
```

**Caso negativo:**
```
[CCOP] Asistencias - Validación edad adulto mayor - [Proveedor] - 75 años plan estándar
[CCOP] Asistencias - Validación duración excedida - [Proveedor] - 400 días
```

---

## 📝 TEMPLATE DE CASO DE PRUEBA

### **Título:**
```
[CCOP] Asistencias - Compra exitosa internacional - [PROVEEDOR] - Plan premium 1 adulto 7 días
```

### **Pasos:**
```
1. **PRECONDICIONES:**
   - Usuario autenticado en portal Consolidación COP
   - Usuario con saldo suficiente: [CANTIDAD] [MILLAS/PUNTOS/COP]
   - Framework: [Angular/React/Otro]

2. **PASO:** Ingresar a sección Asistencias
   - **RESULTADO ESPERADO:** Se muestra formulario de cotización con campos obligatorios

3. **PASO:** Completar cotización con:
   - Destino: Estados Unidos
   - Fecha inicio: [Fecha +10 días]
   - Fecha fin: [Fecha +17 días] (7 días de viaje)
   - Adultos: 1
   - Niños: 0
   - **RESULTADO ESPERADO:** Se muestran planes disponibles con coberturas y precios

4. **PASO:** Comparar planes disponibles:
   - Plan Básico: Cobertura médica USD 50,000
   - Plan Plus: Cobertura médica USD 100,000
   - Plan Premium: Cobertura médica USD 250,000 + beneficios adicionales
   - **RESULTADO ESPERADO:** Se muestra tabla comparativa clara

5. **PASO:** Seleccionar Plan Premium:
   - Precio: [X] [MILLAS/COP]
   - Cobertura médica: USD 250,000
   - Incluye: Cancelación, COVID-19, equipaje, repatriación
   - **RESULTADO ESPERADO:** Se muestra detalle completo del plan seleccionado

6. **PASO:** Hacer clic en "Continuar" o "Comprar"
   - **RESULTADO ESPERADO:** Se carga checkout con formulario de viajero

7. **PASO:** Completar datos del viajero:
   - Nombre: Juan Pérez
   - Fecha nacimiento: 01/01/1990 (36 años)
   - Documento: 1234567890
   - Nacionalidad: Colombiana
   - Condiciones preexistentes: Ninguna
   - **RESULTADO ESPERADO:** Datos se validan correctamente

8. **PASO:** Completar datos de contacto:
   - Email: juan.perez@email.com
   - Teléfono: +57 300 1234567
   - Contacto emergencia: María López - +57 310 9876543
   - **RESULTADO ESPERADO:** Datos validados correctamente

9. **PASO:** Confirmar detalles del viaje:
   - Destino específico: Miami, Florida
   - Motivo: Turismo
   - **RESULTADO ESPERADO:** Información registrada

10. **PASO:** [SI APLICA SLIDER] Ajustar slider de pago:
    - Configuración: [X%] Millas + [Y%] COP
    - **RESULTADO ESPERADO:** Cálculo se actualiza dinámicamente

11. **PASO:** [SI REQUIERE TARJETA] Ingresar datos de tarjeta:
    - Número: 4111111111111111
    - Vencimiento: 12/27
    - CVV: 123
    - **RESULTADO ESPERADO:** Tarjeta validada correctamente

12. **PASO:** Aceptar términos y condiciones y confirmar compra
    - **RESULTADO ESPERADO:** 
      - Se muestra pantalla de confirmación
      - Estado: EMITIDA
      - Se envía email con póliza digital a juan.perez@email.com
      - Póliza incluye: número de póliza, coberturas, teléfonos emergencia 24/7
      - Se descuentan [CANTIDAD] [MILLAS/PUNTOS] o se procesa pago
      - Instrucciones de activación incluidas

13. **PASO:** Validar en admin Consolidación COP que la compra:
    - Estado: EMITIDA
    - Proveedor: [PROVEEDOR]
    - Plan: Premium
    - Destino: Estados Unidos (Miami)
    - Viajero: Juan Pérez - Doc 1234567890 - 36 años
    - Vigencia: [Fecha inicio] al [Fecha fin] (7 días)
    - Cobertura: USD 250,000
    - Monto: [CANTIDAD] [MILLAS/PUNTOS/COP]
    - Póliza generada correctamente
    - **RESULTADO ESPERADO:** Toda la información es correcta y trazable
```

---

## 🚨 CASOS EDGE Y ERRORES COMUNES

### **Error 1: Edad Requiere Plan Especial**
- **Escenario:** Usuario mayor de 70 años selecciona plan estándar
- **Causa:** Planes estándar tienen límite de edad
- **Mensaje esperado:** "Para viajeros mayores de 70 años, requiere plan especial. Contacta soporte."
- **Acción QA:** Validar que informa correctamente y ofrece alternativa

### **Error 2: Duración Excede Máximo**
- **Escenario:** Usuario intenta comprar asistencia para 400 días
- **Causa:** Plan tiene duración máxima de 365 días
- **Mensaje esperado:** "La duración máxima permitida es de 365 días"
- **Acción QA:** Validar que no permite continuar y sugiere dividir en múltiples pólizas

### **Error 3: Destino No Cubierto**
- **Escenario:** Usuario selecciona destino no cubierto por plan básico
- **Causa:** Plan nacional pero destino internacional
- **Mensaje esperado:** "El destino requiere plan internacional. ¿Deseas cambiar a plan internacional?"
- **Acción QA:** Validar que sugiere plan adecuado automáticamente

### **Error 4: Declaración Incompleta**
- **Escenario:** Usuario no completa declaración de salud
- **Causa:** Campo obligatorio sin completar
- **Mensaje esperado:** "Debes completar la declaración de condiciones de salud"
- **Acción QA:** Validar que resalta campo y no permite continuar

### **Error 5: Póliza No Generada**
- **Escenario:** Pago exitoso pero falla emisión de póliza
- **Causa:** Error de integración con proveedor
- **Mensaje esperado:** "Tu compra se procesó. La póliza llegará a tu email en máximo 2 horas."
- **Acción QA:** Validar que compra queda pendiente y se puede reemitir

---

## 🔍 PARTICULARIDADES DEL PROVEEDOR

### **[PROVEEDOR - A DEFINIR]**
- Pólizas son digitales, se envían por email
- Teléfono de emergencia 24/7 disponible desde cualquier país
- Cobertura activa desde inicio de viaje especificado
- No cubre preexistencias no declaradas
- Cancelación permitida hasta [X] horas antes de inicio de viaje
- Reembolsos según política de cancelación
- [OTRAS PARTICULARIDADES - A DEFINIR]

---

## 📊 MATRIZ DE CASOS RECOMENDADA

| Escenario | Plan | Variante | Prioridad | Complejidad |
|-----------|------|----------|-----------|-------------|
| Compra nacional básico | Básico | 1 adulto 3 días | Alta | Baja |
| Compra internacional premium | Premium | 1 adulto 7 días | Alta | Media |
| Compra familia | Plus | 2 adultos 2 niños 10 días | Alta | Media |
| Validación adulto mayor | Estándar | 75 años | Alta | Media |
| Validación duración excedida | Cualquiera | 400 días | Alta | Baja |
| Validación destino incorrecto | Básico nacional | Destino internacional | Alta | Baja |
| Compra con slider mixto | Premium | Millas + COP | Alta | Alta |
| Cancelación antes de viaje | Cualquiera | Según políticas | Media | Media |
| Modificación de póliza | Cualquiera | Cambio fechas/viajeros | Media | Alta |
| Activación de asistencia | Cualquiera | Durante viaje | Alta | Alta |

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
- Test Suite Asistencias: [suiteId a definir]

---

## 📝 NOTAS DE IMPLEMENTACIÓN

**Estado:** 🔄 PENDIENTE DEFINICIÓN

**Pendientes:**
- [ ] Confirmar proveedor específico (Universal Assistance/Assist Card/Otro)
- [ ] Definir framework tecnológico (Angular/React/Otro)
- [ ] Definir modelo de pago exacto (slider, fee, tarjeta)
- [ ] Definir tipo de emisión (automática/manual)
- [ ] Definir planes disponibles y coberturas
- [ ] Definir políticas de cancelación/modificación
- [ ] Definir proceso de activación de asistencia
- [ ] Crear matriz de casos de prueba completa
- [ ] Configurar suiteId "Asistencias" en Azure DevOps
- [ ] Validar con equipo de desarrollo
- [ ] Validar políticas con PO/PM y proveedor

**Última actualización:** 2026-01-22  
**Responsable:** [A DEFINIR]
