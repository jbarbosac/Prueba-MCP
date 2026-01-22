# 📋 [CCOP] AUTOS - Consolidación COP

> Documentación específica para el producto AUTOS (Renta de vehículos) en Consolidación COP (Colombia).

---

## 🎯 IDENTIFICACIÓN

**Producto:** Autos (Renta de vehículos)  
**Portal:** Consolidación COP  
**País:** Colombia  
**Prefijo:** [CCOP]  
**Framework:** [Meteor / Angular / React - A DEFINIR]  
**Estado:** 🔄 PENDIENTE DEFINICIÓN  

---

## 📦 PROVEEDORES

### **Proveedor Principal - SABRE**
- **Nombre:** Sabre (típicamente usado para autos)
- **Rentadoras incluidas (ejemplo):**
  - Hertz
  - Dollar
  - Thrifty
  - Avis
  - Budget
  - [OTRAS - A DEFINIR]
- **Tecnología:** [API REST / SOAP - A DEFINIR]
- **Características:**
  - Múltiples rentadoras
  - Búsqueda en tiempo real
  - Políticas y seguros incluidos

### **Proveedores Adicionales**
- [A DEFINIR si existen otros proveedores]

---

## 💰 MODELO DE PAGO

**Ecuación de pago:**
```
[A DEFINIR]
Ejemplo:
Producto (renta auto) = 100% MILLAS/PUNTOS
O
Producto (renta auto) = X% MILLAS + Y% COP
Fee = [SÍ/NO]
```

**Componentes:**
- **Producto:** [100% Millas / Mixto / 100% Efectivo - A DEFINIR]
- **Fee:** [Sí / No] - [Descripción del fee si aplica]
- **Tarjeta requerida:** [Sí / No] - (Nota: Rentadoras suelen requerir tarjeta para depósito)
- **Slider:** [Sí / No] - [Rango mínimo/máximo si aplica]

**Validaciones de pago:**
- Validar saldo suficiente antes de búsqueda
- Validar tarjeta válida para depósito de rentadora
- [VALIDACIÓN 3 - A DEFINIR]

---

## 🔄 FLUJO DE COMPRA

### **1. BÚSQUEDA**

**Campos obligatorios:**
- Lugar de recogida (ciudad/aeropuerto)
- Fecha y hora de recogida
- Fecha y hora de devolución
- ¿Devolver en otro lugar? (Sí/No)
- Lugar de devolución (si aplica)
- Edad del conductor

**Validaciones:**
- Fecha de recogida no puede ser anterior a hoy
- Fecha de devolución debe ser posterior a recogida
- Edad del conductor válida (típicamente 21+ años, puede variar)
- Si devolución en otro lugar, debe seleccionar ubicación

### **2. RESULTADOS**

**Información mostrada:**
- Rentadora (Hertz, Dollar, Thrifty, etc.)
- Categoría del vehículo (Compacto, Mediano, SUV, etc.)
- Tipo de vehículo (Automático/Manual)
- Capacidad (pasajeros y maletas)
- Precio en [MILLAS/COP - según modelo]
- Política de kilometraje (limitado/ilimitado)
- Seguros incluidos

**Filtros disponibles:**
- Por rentadora
- Por categoría de vehículo
- Por precio
- Por tipo de transmisión
- Por capacidad
- [OTROS - A DEFINIR]

### **3. DETALLE Y SELECCIÓN**

**Información del auto:**
- Foto del vehículo o similar
- Especificaciones técnicas
- Política de kilometraje
- Seguros incluidos vs adicionales
- Términos y condiciones de la rentadora
- Política de combustible
- Política de cancelación
- Ubicación exacta de recogida/devolución
- Horarios de apertura de oficina

**Validaciones:**
- Disponibilidad confirmada
- Precio bloqueado temporalmente
- [OTRAS - A DEFINIR]

### **4. CHECKOUT**

**Campos del formulario:**
- Datos del conductor:
  - Nombre completo - Obligatorio
  - Documento de identidad - Obligatorio
  - Fecha de nacimiento - Obligatorio
  - Email - Obligatorio
  - Teléfono - Obligatorio
  - Licencia de conducir (número y vigencia) - Obligatorio
- Datos de tarjeta de crédito (para depósito rentadora) - Obligatorio
- Aceptación términos y condiciones - Obligatorio
- [OTROS - A DEFINIR]

**Validaciones críticas:**
- Edad del conductor válida (21+ años típicamente)
- Licencia vigente
- Tarjeta de crédito válida a nombre del conductor
- Email válido
- Teléfono válido
- Saldo suficiente (si aplica millas/puntos)

### **5. EMISIÓN**

**Tipo de emisión:** [Automática / Manual / Semiautomática - A DEFINIR]

**Flujo:**
```
[A DEFINIR - Ejemplo:]
Usuario confirma reserva
       ↓
Sistema procesa pago
       ↓
Sistema confirma con rentadora
       ↓
Estado: CONFIRMADA
       ↓
Email con voucher enviado
```

**Estados posibles:**
- PENDIENTE - Reserva creada, confirmación pendiente
- CONFIRMADA - Reserva confirmada con rentadora
- EMITIDA - Voucher emitido
- CANCELADA - Reserva cancelada
- ERROR - Error en proceso
- [OTROS - A DEFINIR]

---

## ✅ VALIDACIONES CRÍTICAS

### **Validación 1: Edad del Conductor**
- **Cuándo:** En búsqueda y en checkout
- **Qué valida:** Conductor cumple edad mínima requerida
- **Mensaje de error:** "La edad mínima para rentar vehículos es de 21 años"
- **Comportamiento esperado:** No permitir continuar si no cumple edad mínima

### **Validación 2: Licencia de Conducir Vigente**
- **Cuándo:** En checkout
- **Qué valida:** Licencia está vigente al momento de recogida
- **Mensaje de error:** "La licencia de conducir debe estar vigente durante todo el período de renta"
- **Comportamiento esperado:** No permitir continuar con licencia vencida

### **Validación 3: Tarjeta de Crédito**
- **Cuándo:** En checkout
- **Qué valida:** Tarjeta es válida y a nombre del conductor
- **Mensaje de error:** "Debes ingresar una tarjeta de crédito válida a nombre del conductor"
- **Comportamiento esperado:** No permitir continuar sin tarjeta válida

### **Validación 4: Horario de Recogida**
- **Cuándo:** En búsqueda
- **Qué valida:** Horario de recogida está dentro del horario de atención de la oficina
- **Mensaje de error:** "La oficina de [Rentadora] en [Ubicación] no está abierta en el horario seleccionado"
- **Comportamiento esperado:** Informar horarios disponibles o permitir modificar

---

## 🎯 CASOS DE PRUEBA TIPO

### **Formato de título:**
```
[CCOP] Autos - {Escenario} - {Proveedor/Rentadora} - {Variante}
```

### **Ejemplos:**

**Caso positivo básico:**
```
[CCOP] Autos - Reserva exitosa mismo lugar - Sabre Hertz - 3 días compacto
[CCOP] Autos - Reserva exitosa diferente lugar - Sabre Dollar - 7 días SUV
```

**Caso con variantes:**
```
[CCOP] Autos - Reserva con slider mixto - Sabre Thrifty - Millas + COP
[CCOP] Autos - Reserva kilometraje ilimitado - Sabre Avis - 5 días
```

**Caso negativo:**
```
[CCOP] Autos - Validación edad mínima - Sabre - Conductor menor 21 años
[CCOP] Autos - Validación licencia vencida - Sabre - Licencia expirada
```

---

## 📝 TEMPLATE DE CASO DE PRUEBA

### **Título:**
```
[CCOP] Autos - Reserva exitosa mismo lugar - Sabre Hertz - 3 días compacto
```

### **Pasos:**
```
1. **PRECONDICIONES:**
   - Usuario autenticado en portal Consolidación COP
   - Usuario con saldo suficiente: [CANTIDAD] [MILLAS/PUNTOS/COP]
   - Usuario mayor de 21 años con licencia vigente
   - Framework: [Meteor/Angular/Otro]

2. **PASO:** Ingresar a sección Autos
   - **RESULTADO ESPERADO:** Se muestra formulario de búsqueda con campos obligatorios

3. **PASO:** Completar búsqueda con:
   - Lugar recogida: Aeropuerto El Dorado Bogotá (BOG)
   - Fecha recogida: [Fecha +3 días] 10:00
   - Fecha devolución: [Fecha +6 días] 10:00
   - Devolver en mismo lugar: Sí
   - Edad conductor: 30 años
   - **RESULTADO ESPERADO:** Se muestran resultados de autos disponibles de múltiples rentadoras

4. **PASO:** Filtrar por rentadora Hertz
   - **RESULTADO ESPERADO:** Se muestran solo vehículos de Hertz

5. **PASO:** Seleccionar vehículo:
   - Categoría: Compacto
   - Transmisión: Automático
   - Pasajeros: 5
   - Maletas: 2
   - Precio: [X] [MILLAS/PUNTOS/COP]
   - Kilometraje: Ilimitado
   - **RESULTADO ESPERADO:** Se carga pantalla de detalle con información completa del vehículo

6. **PASO:** Revisar detalle y hacer clic en "Continuar" o "Reservar"
   - **RESULTADO ESPERADO:** Se carga checkout con formulario conductor y resumen

7. **PASO:** Completar datos del conductor:
   - Nombre: Juan Pérez
   - Documento: 1234567890
   - Fecha nacimiento: 01/01/1994 (30 años)
   - Email: juan.perez@email.com
   - Teléfono: +57 300 1234567
   - Licencia: 12345678 - Vigencia: 12/2027
   - **RESULTADO ESPERADO:** Todos los campos se validan correctamente

8. **PASO:** [SI APLICA SLIDER] Ajustar slider de pago:
   - Configuración: [X%] Millas + [Y%] COP
   - **RESULTADO ESPERADO:** Cálculo se actualiza dinámicamente mostrando desglose

9. **PASO:** Ingresar datos de tarjeta de crédito (depósito rentadora):
   - Número: 4111111111111111
   - Titular: Juan Pérez
   - Vencimiento: 12/27
   - CVV: 123
   - **RESULTADO ESPERADO:** Datos se validan y se acepta la tarjeta

10. **PASO:** Aceptar términos y condiciones y confirmar reserva
    - **RESULTADO ESPERADO:** 
      - Se muestra pantalla de confirmación con voucher
      - Estado de reserva: [CONFIRMADA/EMITIDA según modelo]
      - Se envía email con voucher a juan.perez@email.com
      - Voucher incluye: número confirmación, datos rentadora, ubicación recogida, horarios
      - Se descuentan [CANTIDAD] [MILLAS/PUNTOS] o se procesa pago

11. **PASO:** Validar en admin Consolidación COP que la reserva:
    - Estado: [CONFIRMADA/EMITIDA según modelo]
    - Proveedor: Sabre - Rentadora: Hertz
    - Ubicación: Aeropuerto El Dorado Bogotá
    - Fechas: [Fecha recogida] al [Fecha devolución]
    - Vehículo: Compacto automático o similar
    - Conductor: Juan Pérez - Lic 12345678
    - Monto: [CANTIDAD] [MILLAS/PUNTOS/COP]
    - Voucher generado correctamente
    - **RESULTADO ESPERADO:** Toda la información es correcta y trazable
```

---

## 🚨 CASOS EDGE Y ERRORES COMUNES

### **Error 1: Edad Mínima No Cumplida**
- **Escenario:** Usuario menor de 21 años intenta rentar
- **Causa:** Edad no cumple requisito mínimo
- **Mensaje esperado:** "La edad mínima para rentar vehículos es de 21 años"
- **Acción QA:** Validar que bloquea la reserva

### **Error 2: Licencia Vencida**
- **Escenario:** Licencia expira antes de fecha de devolución
- **Causa:** Fecha de vencimiento de licencia anterior a fecha devolución
- **Mensaje esperado:** "La licencia de conducir debe estar vigente durante todo el período de renta"
- **Acción QA:** Validar que no permite continuar

### **Error 3: Tarjeta Rechazada**
- **Escenario:** Tarjeta no válida o rechazada
- **Causa:** Tarjeta débito, fondos insuficientes, etc.
- **Mensaje esperado:** "Debes ingresar una tarjeta de crédito válida"
- **Acción QA:** Validar mensaje y permitir reintentar

### **Error 4: Vehículo No Disponible**
- **Escenario:** Vehículo seleccionado se agota antes de confirmar
- **Causa:** Otro usuario reservó el último vehículo disponible
- **Mensaje esperado:** "Lo sentimos, este vehículo ya no está disponible. Por favor selecciona otro."
- **Acción QA:** Validar que redirige a resultados

### **Error 5: Horario Fuera de Atención**
- **Escenario:** Usuario intenta recoger en horario cerrado de oficina
- **Causa:** Hora seleccionada fuera del horario de la rentadora
- **Mensaje esperado:** "La oficina de [Rentadora] no está abierta en el horario seleccionado. Horario: [Horario apertura]"
- **Acción QA:** Validar que informa horarios correctos

---

## 🔍 PARTICULARIDADES DEL PROVEEDOR

### **SABRE - Hertz**
- Requiere tarjeta de crédito obligatoria (no débito)
- Edad mínima 21 años (cargo adicional para menores de 25)
- Seguros básicos incluidos, adicionales opcionales
- Política de combustible: Lleno a lleno

### **SABRE - Dollar**
- Similar a Hertz
- Promociones especiales según temporada
- [PARTICULARIDAD A DEFINIR]

### **SABRE - Thrifty**
- Categorías de vehículos económicas
- [PARTICULARIDAD A DEFINIR]

---

## 📊 MATRIZ DE CASOS RECOMENDADA

| Escenario | Rentadora | Variante | Prioridad | Complejidad |
|-----------|-----------|----------|-----------|-------------|
| Reserva mismo lugar | Hertz | 3 días compacto | Alta | Baja |
| Reserva diferente lugar | Dollar | 7 días SUV | Alta | Media |
| Reserva con múltiples conductores | Thrifty | 5 días mediano | Media | Media |
| Validación edad mínima | Cualquiera | Menor 21 años | Alta | Baja |
| Validación licencia vencida | Cualquiera | Licencia expirada | Alta | Baja |
| Reserva con slider mixto | Avis | Millas + COP | Alta | Alta |
| Reserva con seguros adicionales | Hertz | Cobertura completa | Media | Media |
| Cambio de reserva | Dollar | Modificar fechas | Media | Alta |
| Cancelación de reserva | Hertz | Según políticas | Media | Media |
| Reserva larga duración | Thrifty | 30+ días | Baja | Media |

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
- Test Suite Autos: [suiteId a definir]

---

## 📝 NOTAS DE IMPLEMENTACIÓN

**Estado:** 🔄 PENDIENTE DEFINICIÓN

**Pendientes:**
- [ ] Confirmar proveedor y rentadoras disponibles
- [ ] Definir framework tecnológico (Meteor/Angular/Otro)
- [ ] Definir modelo de pago exacto (slider, fee, tarjeta)
- [ ] Definir tipo de emisión (automática/manual)
- [ ] Confirmar edad mínima y políticas por rentadora
- [ ] Definir seguros incluidos vs adicionales
- [ ] Crear matriz de casos de prueba completa
- [ ] Configurar suiteId "Autos" en Azure DevOps
- [ ] Validar con equipo de desarrollo
- [ ] Validar políticas con PO/PM

**Última actualización:** 2026-01-22  
**Responsable:** [A DEFINIR]
