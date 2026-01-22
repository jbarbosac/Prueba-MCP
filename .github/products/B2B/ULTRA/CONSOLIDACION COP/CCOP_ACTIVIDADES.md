# 📋 [CCOP] ACTIVIDADES - Consolidación COP

> Documentación específica para el producto ACTIVIDADES (Tours y experiencias) en Consolidación COP (Colombia).

---

## 🎯 IDENTIFICACIÓN

**Producto:** Actividades (Tours, excursiones, experiencias)  
**Portal:** Consolidación COP  
**País:** Colombia  
**Prefijo:** [CCOP]  
**Framework:** [Angular / React / Otro - A DEFINIR]  
**Estado:** 🔄 PENDIENTE DEFINICIÓN  

---

## 📦 PROVEEDORES

### **Proveedor Principal - HotelBeds**
- **Nombre:** HotelBeds (típicamente usado para actividades)
- **Tecnología:** API REST
- **Tipos de actividades:**
  - Tours guiados
  - Excursiones
  - Entradas a atracciones
  - Experiencias gastronómicas
  - Deportes y aventura
  - Espectáculos
  - [OTRAS - A DEFINIR]
- **Características:**
  - Actividades en múltiples ciudades
  - Búsqueda por destino y fecha
  - Actividades con horarios fijos y flexibles
  - Cancelación según políticas
  - [OTRAS - A DEFINIR]

### **Proveedores Adicionales**
- [A DEFINIR si existen otros proveedores]

---

## 💰 MODELO DE PAGO

**Ecuación de pago:**
```
[A DEFINIR]
Ejemplo:
Producto (actividad) = 100% MILLAS/PUNTOS
O
Producto (actividad) = X% MILLAS + Y% COP
Fee = [SÍ/NO]
```

**Componentes:**
- **Producto:** [100% Millas / Mixto / 100% Efectivo - A DEFINIR]
- **Fee:** [Sí / No] - [Descripción del fee si aplica]
- **Tarjeta requerida:** [Sí / No]
- **Slider:** [Sí / No] - [Rango mínimo/máximo si aplica]

**Validaciones de pago:**
- Validar saldo suficiente antes de búsqueda
- Validar disponibilidad antes de pago
- [VALIDACIÓN 3 - A DEFINIR]

---

## 🔄 FLUJO DE COMPRA

### **1. BÚSQUEDA**

**Campos obligatorios:**
- Destino (ciudad/región)
- Fecha de la actividad (o rango de fechas)
- Número de participantes por categoría:
  - Adultos
  - Niños (según rango de edad de la actividad)
  - Infantes (si aplica)

**Validaciones:**
- Fecha no puede ser anterior a hoy
- Número de participantes válido
- [OTRAS - A DEFINIR]

### **2. RESULTADOS**

**Información mostrada:**
- Nombre de la actividad
- Categoría (tour, excursión, entrada, etc.)
- Duración estimada
- Horarios disponibles
- Idioma (español, inglés, etc.)
- Precio por persona en [MILLAS/COP - según modelo]
- Calificación/reseñas (si aplica)
- Foto principal
- Política de cancelación

**Filtros disponibles:**
- Por categoría de actividad
- Por precio
- Por duración
- Por horario
- Por calificación
- [OTROS - A DEFINIR]

### **3. DETALLE Y SELECCIÓN**

**Información de la actividad:**
- Descripción completa
- Qué incluye / Qué no incluye
- Punto de encuentro
- Horarios disponibles específicos
- Idiomas disponibles
- Duración exacta
- Requisitos (edad mínima, condición física, etc.)
- Política de cancelación detallada
- Qué llevar (ropa, documentos, etc.)
- Galería de fotos
- Mapa de ubicación
- Términos y condiciones

**Validaciones:**
- Disponibilidad confirmada para fecha y horario seleccionado
- Cupos disponibles
- Precio bloqueado temporalmente
- [OTRAS - A DEFINIR]

### **4. CHECKOUT**

**Campos del formulario:**
- Datos del contacto principal:
  - Nombre completo - Obligatorio
  - Email - Obligatorio
  - Teléfono - Obligatorio
- Datos por cada participante:
  - Nombre completo - Obligatorio
  - Edad o fecha de nacimiento - Según actividad
  - Requisitos especiales (dieta, accesibilidad, etc.) - Opcional
- Horario específico seleccionado - Obligatorio
- Punto de encuentro confirmado - Obligatorio
- Datos de tarjeta (si requiere fee o pago efectivo) - Según modelo
- Aceptación términos y condiciones - Obligatorio
- [OTROS - A DEFINIR]

**Validaciones críticas:**
- Edad de participantes válida para actividad seleccionada
- Email válido
- Teléfono válido
- Horario seleccionado disponible
- Tarjeta válida (si aplica)
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
Sistema confirma con proveedor
       ↓
Estado: CONFIRMADA
       ↓
Email con voucher y detalles enviado
```

**Estados posibles:**
- PENDIENTE - Reserva creada, confirmación pendiente
- CONFIRMADA - Actividad confirmada con proveedor
- EMITIDA - Voucher emitido
- REALIZADA - Actividad completada
- CANCELADA - Reserva cancelada
- ERROR - Error en proceso
- [OTROS - A DEFINIR]

---

## ✅ VALIDACIONES CRÍTICAS

### **Validación 1: Edad Mínima Requerida**
- **Cuándo:** Al seleccionar actividad y en checkout
- **Qué valida:** Participantes cumplen edad mínima requerida
- **Mensaje de error:** "Esta actividad requiere edad mínima de [X] años"
- **Comportamiento esperado:** No permitir continuar si no cumple requisito

### **Validación 2: Disponibilidad y Cupos**
- **Cuándo:** Antes de confirmar compra
- **Qué valida:** Actividad tiene cupos disponibles para fecha/horario seleccionado
- **Mensaje de error:** "Lo sentimos, no hay cupos disponibles para el horario seleccionado. Elige otro horario."
- **Comportamiento esperado:** Mostrar solo horarios con disponibilidad

### **Validación 3: Requisitos Especiales**
- **Cuándo:** En detalle y checkout
- **Qué valida:** Usuario está informado de requisitos (condición física, documentos, etc.)
- **Mensaje de error:** N/A (informativo)
- **Comportamiento esperado:** Mostrar claramente requisitos y confirmar aceptación

### **Validación 4: Punto de Encuentro**
- **Cuándo:** En confirmación
- **Qué valida:** Usuario tiene claro dónde y cuándo debe presentarse
- **Mensaje de error:** N/A (informativo)
- **Comportamiento esperado:** Incluir dirección exacta y hora en voucher

---

## 🎯 CASOS DE PRUEBA TIPO

### **Formato de título:**
```
[CCOP] Actividades - {Escenario} - {Proveedor} - {Variante}
```

### **Ejemplos:**

**Caso positivo básico:**
```
[CCOP] Actividades - Reserva exitosa tour - HotelBeds - City tour Bogotá 2 adultos
[CCOP] Actividades - Reserva exitosa entrada - HotelBeds - Museo del Oro 1 adulto
```

**Caso con variantes:**
```
[CCOP] Actividades - Reserva con slider mixto - HotelBeds - Millas + COP
[CCOP] Actividades - Reserva familia - HotelBeds - 2 adultos 2 niños
```

**Caso negativo:**
```
[CCOP] Actividades - Validación edad mínima - HotelBeds - Niño 5 años actividad 12+
[CCOP] Actividades - Validación sin cupos - HotelBeds - Horario agotado
```

---

## 📝 TEMPLATE DE CASO DE PRUEBA

### **Título:**
```
[CCOP] Actividades - Reserva exitosa tour - HotelBeds - City tour Bogotá 2 adultos
```

### **Pasos:**
```
1. **PRECONDICIONES:**
   - Usuario autenticado en portal Consolidación COP
   - Usuario con saldo suficiente: [CANTIDAD] [MILLAS/PUNTOS/COP]
   - Framework: [Angular/React/Otro]

2. **PASO:** Ingresar a sección Actividades
   - **RESULTADO ESPERADO:** Se muestra formulario de búsqueda con campos obligatorios

3. **PASO:** Completar búsqueda con:
   - Destino: Bogotá, Colombia
   - Fecha: [Fecha +5 días]
   - Adultos: 2
   - Niños: 0
   - **RESULTADO ESPERADO:** Se muestran actividades disponibles en Bogotá para la fecha

4. **PASO:** Filtrar por categoría "Tours"
   - **RESULTADO ESPERADO:** Se muestran solo tours guiados

5. **PASO:** Seleccionar actividad "City Tour Bogotá Histórico":
   - Duración: 4 horas
   - Idioma: Español
   - Horarios: 9:00 AM, 2:00 PM
   - Precio por persona: [X] [MILLAS/COP]
   - Calificación: 4.5/5
   - **RESULTADO ESPERADO:** Se carga pantalla de detalle con información completa

6. **PASO:** Revisar detalle de la actividad:
   - Incluye: Guía, transporte, entrada museo
   - No incluye: Alimentos, propinas
   - Punto encuentro: Plaza de Bolívar
   - Edad mínima: 5 años
   - Política cancelación: Gratis hasta 24h antes
   - **RESULTADO ESPERADO:** Información clara y completa

7. **PASO:** Seleccionar horario 9:00 AM y hacer clic en "Reservar"
   - **RESULTADO ESPERADO:** Se carga checkout con formulario de participantes

8. **PASO:** Completar datos del contacto:
   - Nombre: Juan Pérez
   - Email: juan.perez@email.com
   - Teléfono: +57 300 1234567
   - **RESULTADO ESPERADO:** Datos validados correctamente

9. **PASO:** Completar datos de participantes:
   - Participante 1: Juan Pérez - Adulto
   - Participante 2: María López - Adulto
   - **RESULTADO ESPERADO:** Datos validados correctamente

10. **PASO:** [SI APLICA SLIDER] Ajustar slider de pago:
    - Configuración: [X%] Millas + [Y%] COP
    - **RESULTADO ESPERADO:** Cálculo se actualiza dinámicamente

11. **PASO:** [SI REQUIERE TARJETA] Ingresar datos de tarjeta:
    - Número: 4111111111111111
    - Vencimiento: 12/27
    - CVV: 123
    - **RESULTADO ESPERADO:** Tarjeta validada correctamente

12. **PASO:** Aceptar términos y condiciones y confirmar reserva
    - **RESULTADO ESPERADO:** 
      - Se muestra pantalla de confirmación
      - Estado: CONFIRMADA
      - Se envía email con voucher a juan.perez@email.com
      - Voucher incluye: código confirmación, fecha, horario 9:00 AM, punto encuentro exacto
      - Instrucciones: Llegar 15 min antes, llevar documento identidad
      - Se descuentan [CANTIDAD] [MILLAS/PUNTOS] o se procesa pago

13. **PASO:** Validar en admin Consolidación COP que la reserva:
    - Estado: CONFIRMADA
    - Proveedor: HotelBeds
    - Actividad: City Tour Bogotá Histórico
    - Fecha: [Fecha seleccionada]
    - Horario: 9:00 AM
    - Participantes: Juan Pérez, María López (2 adultos)
    - Punto encuentro: Plaza de Bolívar
    - Monto: [CANTIDAD] [MILLAS/PUNTOS/COP]
    - Voucher generado correctamente
    - **RESULTADO ESPERADO:** Toda la información es correcta y trazable
```

---

## 🚨 CASOS EDGE Y ERRORES COMUNES

### **Error 1: Edad Mínima No Cumplida**
- **Escenario:** Niño menor a edad mínima requerida para actividad
- **Causa:** Edad participante menor a requisito
- **Mensaje esperado:** "Esta actividad requiere edad mínima de [X] años"
- **Acción QA:** Validar que bloquea la reserva

### **Error 2: Sin Cupos Disponibles**
- **Escenario:** Horario seleccionado se agota antes de confirmar
- **Causa:** Otro usuario reservó último cupo
- **Mensaje esperado:** "Lo sentimos, no hay cupos disponibles para el horario seleccionado"
- **Acción QA:** Validar que muestra horarios alternativos

### **Error 3: Actividad Cancelada por Proveedor**
- **Escenario:** Proveedor cancela actividad (mal tiempo, cupo mínimo no alcanzado)
- **Causa:** Condiciones externas
- **Mensaje esperado:** "La actividad ha sido cancelada. Se reembolsarán [MILLAS/COP] automáticamente"
- **Acción QA:** Validar que notifica usuario y procesa reembolso

### **Error 4: Punto de Encuentro No Claro**
- **Escenario:** Voucher no incluye dirección exacta
- **Causa:** Error en generación de voucher
- **Mensaje esperado:** N/A (prevención)
- **Acción QA:** Validar que voucher siempre incluye dirección completa y mapa

### **Error 5: Confirmación Tardía**
- **Escenario:** Proveedor no confirma inmediatamente
- **Causa:** Proceso manual de confirmación
- **Mensaje esperado:** "Tu reserva está pendiente de confirmación. Recibirás email en máximo 24 horas."
- **Acción QA:** Validar que reserva queda en estado PENDIENTE y se notifica cuando confirma

---

## 🔍 PARTICULARIDADES DEL PROVEEDOR

### **HotelBeds**
- Actividades requieren confirmación del proveedor (puede ser inmediata o en 24h)
- Vouchers son digitales, algunos requieren impresión
- Punto de encuentro puede ser hotel del cliente (pickup)
- Políticas de cancelación varían por actividad
- Algunos tours tienen cupo mínimo para operar
- Idiomas disponibles según disponibilidad de guías
- [OTRAS PARTICULARIDADES - A DEFINIR]

---

## 📊 MATRIZ DE CASOS RECOMENDADA

| Escenario | Tipo Actividad | Variante | Prioridad | Complejidad |
|-----------|----------------|----------|-----------|-------------|
| Reserva tour ciudad | City tour | 2 adultos | Alta | Baja |
| Reserva entrada museo | Entrada | 1 adulto | Alta | Baja |
| Reserva excursión | Excursión día completo | 2 adultos 1 niño | Alta | Media |
| Validación edad mínima | Tour aventura | Niño menor edad | Alta | Baja |
| Validación sin cupos | Tour popular | Horario agotado | Alta | Media |
| Reserva con pickup | Tour con recogida | Hotel específico | Media | Media |
| Reserva con slider mixto | Cualquiera | Millas + COP | Alta | Alta |
| Cancelación antes 24h | Tour ciudad | Reembolso completo | Media | Media |
| Cancelación después 24h | Tour ciudad | Sin reembolso | Media | Baja |
| Modificación de reserva | Cualquiera | Cambio fecha/horario | Media | Alta |

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
- Test Suite Actividades: [suiteId a definir]

---

## 📝 NOTAS DE IMPLEMENTACIÓN

**Estado:** 🔄 PENDIENTE DEFINICIÓN

**Pendientes:**
- [ ] Confirmar proveedor específico (HotelBeds/Otro)
- [ ] Definir framework tecnológico (Angular/React/Otro)
- [ ] Definir modelo de pago exacto (slider, fee, tarjeta)
- [ ] Definir tipo de emisión/confirmación (inmediata/24h)
- [ ] Definir categorías de actividades disponibles
- [ ] Definir políticas de cancelación estándar
- [ ] Definir proceso de pickup (si aplica)
- [ ] Crear matriz de casos de prueba completa
- [ ] Configurar suiteId "Actividades" en Azure DevOps
- [ ] Validar con equipo de desarrollo
- [ ] Validar políticas con PO/PM

**Última actualización:** 2026-01-22  
**Responsable:** [A DEFINIR]
