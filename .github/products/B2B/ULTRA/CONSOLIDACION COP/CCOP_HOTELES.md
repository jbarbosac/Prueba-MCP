# 📋 [CCOP] HOTELES - Consolidación COP

> Documentación específica para el producto HOTELES en Consolidación COP (Colombia).

---

## 🎯 IDENTIFICACIÓN

**Producto:** Hoteles (Alojamiento)  
**Portal:** Consolidación COP  
**País:** Colombia  
**Prefijo:** [CCOP]  
**Framework:** [Angular / React / Otro - A DEFINIR]  
**Estado:** 🔄 PENDIENTE DEFINICIÓN  

---

## 📦 PROVEEDORES

### **Proveedor Principal - HotelBeds**
- **Nombre:** HotelBeds (típicamente usado para hoteles)
- **Tecnología:** API REST
- **Cobertura:**
  - Hoteles en Colombia
  - Hoteles internacionales
  - Diferentes categorías (1-5 estrellas)
  - Múltiples tipos de habitación
  - [OTROS - A DEFINIR]
- **Características:**
  - Búsqueda en tiempo real
  - Disponibilidad actualizada
  - Diferentes regímenes (solo hospedaje, desayuno, todo incluido)
  - Políticas de cancelación variables
  - [OTRAS - A DEFINIR]

### **Proveedores Adicionales**
- **DerbySoft:** [A DEFINIR si aplica]
- **Otros:** [A DEFINIR]

---

## 💰 MODELO DE PAGO

**Ecuación de pago:**
```
[A DEFINIR]
Ejemplo:
Producto (hotel) = 100% MILLAS/PUNTOS
O
Producto (hotel) = X% MILLAS + Y% COP
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
- Destino (ciudad/región/hotel específico)
- Fecha de check-in
- Fecha de check-out
- Número de habitaciones
- Número de huéspedes por habitación:
  - Adultos (por habitación)
  - Niños (por habitación, con edades)

**Validaciones:**
- Fecha check-in no puede ser anterior a hoy
- Fecha check-out debe ser posterior a check-in
- Número de habitaciones válido (mínimo 1, típicamente máximo 9)
- Número de adultos válido por habitación
- Edades de niños válidas
- [OTRAS - A DEFINIR]

### **2. RESULTADOS**

**Información mostrada:**
- Nombre del hotel
- Categoría (estrellas)
- Ubicación (dirección, distancia centro)
- Foto principal
- Precio por noche y precio total en [MILLAS/COP - según modelo]
- Tipo de habitación disponible
- Régimen (solo hospedaje, desayuno incluido, etc.)
- Servicios destacados (WiFi, piscina, gym, parking, etc.)
- Calificación/reseñas (si aplica)
- Política de cancelación
- Disponibilidad ("Última habitación", "Solo quedan X", etc.)

**Filtros disponibles:**
- Por precio
- Por categoría (estrellas)
- Por servicios (WiFi, piscina, estacionamiento, etc.)
- Por zona/ubicación
- Por régimen alimenticio
- Por calificación
- Por política de cancelación (gratuita/no reembolsable)
- [OTROS - A DEFINIR]

### **3. DETALLE Y SELECCIÓN**

**Información del hotel:**
- Descripción completa del hotel
- Galería de fotos
- Ubicación en mapa
- Servicios completos del hotel
- Opciones de habitaciones disponibles:
  - Tipo de habitación (estándar, suite, etc.)
  - Capacidad (camas, personas)
  - Tamaño (m²)
  - Servicios de habitación
  - Precio por noche
  - Precio total
  - Régimen incluido
  - Política de cancelación
- Reseñas de huéspedes (si aplica)
- Políticas del hotel (check-in/check-out, mascotas, fumadores, etc.)
- Términos y condiciones

**Validaciones:**
- Disponibilidad confirmada para fechas seleccionadas
- Precio bloqueado temporalmente
- [OTRAS - A DEFINIR]

### **4. CHECKOUT**

**Campos del formulario:**
- Datos del huésped principal:
  - Nombre completo - Obligatorio
  - Email - Obligatorio
  - Teléfono - Obligatorio
  - Documento de identidad - Obligatorio
- Datos adicionales:
  - Hora estimada de llegada - Opcional
  - Peticiones especiales (cama extra, cuna, piso alto, etc.) - Opcional
- Datos de tarjeta de crédito (garantía hotel o pago) - Según modelo y política
- Aceptación términos y condiciones - Obligatorio
- [OTROS - A DEFINIR]

**Validaciones críticas:**
- Email válido
- Teléfono válido
- Tarjeta válida (si se requiere garantía)
- Saldo suficiente (si aplica millas/puntos)
- Disponibilidad confirmada al momento de pago

### **5. EMISIÓN**

**Tipo de emisión:** [Automática / Manual / Semiautomática - A DEFINIR]

**Flujo:**
```
[A DEFINIR - Ejemplo:]
Usuario confirma reserva
       ↓
Sistema procesa pago
       ↓
Sistema confirma con hotel
       ↓
Estado: CONFIRMADA
       ↓
Email con voucher enviado
```

**Estados posibles:**
- PENDIENTE - Reserva creada, confirmación pendiente
- CONFIRMADA - Hotel confirmó disponibilidad
- EMITIDA - Voucher emitido
- CHECK-IN - Huésped se registró en hotel
- COMPLETADA - Estadía finalizada
- CANCELADA - Reserva cancelada
- NO-SHOW - Huésped no se presentó
- ERROR - Error en proceso
- [OTROS - A DEFINIR]

---

## ✅ VALIDACIONES CRÍTICAS

### **Validación 1: Disponibilidad de Habitación**
- **Cuándo:** Al seleccionar habitación y antes de pago
- **Qué valida:** Habitación sigue disponible para las fechas
- **Mensaje de error:** "Lo sentimos, esta habitación ya no está disponible. Por favor selecciona otra opción."
- **Comportamiento esperado:** Mostrar opciones alternativas o redirigir a resultados

### **Validación 2: Fechas Válidas**
- **Cuándo:** En búsqueda
- **Qué valida:** Check-in no es anterior a hoy y check-out es posterior a check-in
- **Mensaje de error:** "Las fechas seleccionadas no son válidas"
- **Comportamiento esperado:** Calendario solo permite fechas válidas

### **Validación 3: Capacidad de Habitación**
- **Cuándo:** Al seleccionar habitación
- **Qué valida:** Número de huéspedes no excede capacidad de habitación
- **Mensaje de error:** "Esta habitación tiene capacidad máxima de [X] personas"
- **Comportamiento esperado:** Solo mostrar habitaciones con capacidad suficiente

### **Validación 4: Política de Cancelación**
- **Cuándo:** En detalle y checkout
- **Qué valida:** Usuario está informado de política (reembolsable/no reembolsable)
- **Mensaje de error:** N/A (informativo)
- **Comportamiento esperado:** Mostrar claramente si es cancelable y hasta cuándo

---

## 🎯 CASOS DE PRUEBA TIPO

### **Formato de título:**
```
[CCOP] Hoteles - {Escenario} - {Proveedor} - {Variante}
```

### **Ejemplos:**

**Caso positivo básico:**
```
[CCOP] Hoteles - Reserva exitosa nacional - HotelBeds - 1 hab 2 noches Bogotá
[CCOP] Hoteles - Reserva exitosa internacional - HotelBeds - 1 hab 5 noches Miami
```

**Caso con variantes:**
```
[CCOP] Hoteles - Reserva con slider mixto - HotelBeds - Millas + COP
[CCOP] Hoteles - Reserva múltiples habitaciones - HotelBeds - 2 hab familia
```

**Caso negativo:**
```
[CCOP] Hoteles - Validación habitación no disponible - HotelBeds
[CCOP] Hoteles - Validación capacidad excedida - HotelBeds - 5 personas hab 2 pax
```

---

## 📝 TEMPLATE DE CASO DE PRUEBA

### **Título:**
```
[CCOP] Hoteles - Reserva exitosa nacional - HotelBeds - 1 hab 2 noches Bogotá
```

### **Pasos:**
```
1. **PRECONDICIONES:**
   - Usuario autenticado en portal Consolidación COP
   - Usuario con saldo suficiente: [CANTIDAD] [MILLAS/PUNTOS/COP]
   - Framework: [Angular/React/Otro]

2. **PASO:** Ingresar a sección Hoteles
   - **RESULTADO ESPERADO:** Se muestra formulario de búsqueda con campos obligatorios

3. **PASO:** Completar búsqueda con:
   - Destino: Bogotá, Colombia
   - Check-in: [Fecha +7 días]
   - Check-out: [Fecha +9 días] (2 noches)
   - Habitaciones: 1
   - Adultos: 2
   - Niños: 0
   - **RESULTADO ESPERADO:** Se muestran hoteles disponibles en Bogotá para las fechas

4. **PASO:** Filtrar por:
   - Categoría: 4 estrellas
   - Zona: Zona T (Chapinero)
   - Servicios: WiFi gratis, Desayuno incluido
   - **RESULTADO ESPERADO:** Resultados filtrados según criterios

5. **PASO:** Seleccionar hotel "Hotel Ejemplo 4*":
   - Ubicación: Zona T, Bogotá
   - Precio: [X] [MILLAS/COP] por noche
   - Total: [Y] [MILLAS/COP] (2 noches)
   - Régimen: Desayuno incluido
   - Cancelación: Gratis hasta 24h antes
   - **RESULTADO ESPERADO:** Se carga pantalla de detalle del hotel

6. **PASO:** Revisar detalle del hotel:
   - Fotos: Galería de 10+ imágenes
   - Ubicación: Mapa interactivo
   - Servicios: WiFi, gym, restaurante, parking
   - Reseñas: 4.5/5
   - **RESULTADO ESPERADO:** Información completa y clara

7. **PASO:** Seleccionar tipo de habitación:
   - Habitación Estándar Doble
   - Capacidad: 2 adultos
   - Tamaño: 25 m²
   - Cama: 1 cama doble o 2 individuales
   - Régimen: Desayuno incluido
   - Precio: [X] [MILLAS/COP]/noche
   - **RESULTADO ESPERADO:** Habitación seleccionada y agregada al carrito

8. **PASO:** Hacer clic en "Continuar" o "Reservar"
   - **RESULTADO ESPERADO:** Se carga checkout con formulario de huésped

9. **PASO:** Completar datos del huésped:
   - Nombre: Juan Pérez
   - Email: juan.perez@email.com
   - Teléfono: +57 300 1234567
   - Documento: 1234567890
   - Hora llegada estimada: 15:00
   - Peticiones: Habitación piso alto
   - **RESULTADO ESPERADO:** Datos validados correctamente

10. **PASO:** [SI APLICA SLIDER] Ajustar slider de pago:
    - Configuración: [X%] Millas + [Y%] COP
    - **RESULTADO ESPERADO:** Cálculo se actualiza dinámicamente

11. **PASO:** [SI REQUIERE TARJETA] Ingresar datos de tarjeta:
    - Número: 4111111111111111
    - Titular: Juan Pérez
    - Vencimiento: 12/27
    - CVV: 123
    - **RESULTADO ESPERADO:** Tarjeta validada correctamente

12. **PASO:** Revisar resumen y aceptar términos y confirmar reserva
    - **RESULTADO ESPERADO:** 
      - Se muestra pantalla de confirmación
      - Estado: CONFIRMADA
      - Se envía email con voucher a juan.perez@email.com
      - Voucher incluye: código confirmación, dirección hotel, check-in/check-out, régimen
      - Instrucciones: Check-in 15:00, Check-out 12:00
      - Se descuentan [CANTIDAD] [MILLAS/PUNTOS] o se procesa pago

13. **PASO:** Validar en admin Consolidación COP que la reserva:
    - Estado: CONFIRMADA
    - Proveedor: HotelBeds
    - Hotel: Hotel Ejemplo 4* - Zona T, Bogotá
    - Check-in: [Fecha seleccionada]
    - Check-out: [Fecha seleccionada]
    - Noches: 2
    - Habitación: Estándar Doble
    - Huésped: Juan Pérez - Doc 1234567890
    - Régimen: Desayuno incluido
    - Monto: [CANTIDAD] [MILLAS/PUNTOS/COP]
    - Voucher generado correctamente
    - **RESULTADO ESPERADO:** Toda la información es correcta y trazable
```

---

## 🚨 CASOS EDGE Y ERRORES COMUNES

### **Error 1: Habitación No Disponible**
- **Escenario:** Habitación seleccionada se agota antes de confirmar
- **Causa:** Otro usuario reservó la última habitación
- **Mensaje esperado:** "Lo sentimos, esta habitación ya no está disponible. Mostrando opciones similares..."
- **Acción QA:** Validar que muestra alternativas automáticamente

### **Error 2: Precio Ha Cambiado**
- **Escenario:** Precio aumenta entre selección y confirmación
- **Causa:** Tarifa dinámica del proveedor
- **Mensaje esperado:** "El precio ha cambiado. Nuevo precio: [Y] [MILLAS/COP]. ¿Deseas continuar?"
- **Acción QA:** Validar que informa claramente y requiere nueva aceptación

### **Error 3: Capacidad Excedida**
- **Escenario:** Usuario intenta reservar habitación para más personas que su capacidad
- **Causa:** Habitación máximo 2 personas pero busca para 4
- **Mensaje esperado:** "Esta habitación tiene capacidad máxima de 2 personas"
- **Acción QA:** Validar que solo muestra habitaciones con capacidad suficiente

### **Error 4: Cancelación Fuera de Plazo**
- **Escenario:** Usuario intenta cancelar después del plazo permitido
- **Causa:** Política de cancelación no permite reembolso
- **Mensaje esperado:** "Esta reserva no es reembolsable. ¿Estás seguro de cancelar?"
- **Acción QA:** Validar que informa pérdida de monto y requiere confirmación

### **Error 5: Confirmación Tardía**
- **Escenario:** Hotel no confirma inmediatamente
- **Causa:** Requiere confirmación manual del hotel
- **Mensaje esperado:** "Tu reserva está pendiente de confirmación. Recibirás email en máximo 24 horas."
- **Acción QA:** Validar que reserva queda PENDIENTE y se notifica cuando confirma

---

## 🔍 PARTICULARIDADES DEL PROVEEDOR

### **HotelBeds**
- Confirmación típicamente inmediata (puede ser hasta 24h)
- Vouchers son digitales, algunos hoteles pueden requerir impresión
- Políticas de cancelación varían por hotel y tarifa
- Algunos hoteles cobran depósito adicional en check-in (no cubierto por reserva)
- Impuestos hoteleros locales pueden aplicar (pago directo en hotel)
- Check-in estándar 15:00, Check-out estándar 12:00
- Early check-in o late check-out sujeto a disponibilidad
- [OTRAS PARTICULARIDADES - A DEFINIR]

### **DerbySoft** (si aplica)
- [PARTICULARIDADES - A DEFINIR]

---

## 📊 MATRIZ DE CASOS RECOMENDADA

| Escenario | Destino | Variante | Prioridad | Complejidad |
|-----------|---------|----------|-----------|-------------|
| Reserva nacional 1 hab | Bogotá | 2 noches 2 adultos | Alta | Baja |
| Reserva internacional 1 hab | Miami | 5 noches 2 adultos | Alta | Media |
| Reserva múltiples habitaciones | Cartagena | 2 hab 3 noches | Alta | Media |
| Reserva con niños | Bogotá | 1 hab 2 adultos 2 niños | Alta | Media |
| Validación habitación no disponible | Cualquiera | Última habitación agotada | Alta | Media |
| Validación capacidad excedida | Cualquiera | 4 pax hab 2 pax | Alta | Baja |
| Reserva con slider mixto | Cualquiera | Millas + COP | Alta | Alta |
| Reserva no reembolsable | Cualquiera | Tarifa más económica | Media | Baja |
| Cancelación antes plazo | Cualquiera | Reembolso completo | Media | Media |
| Cancelación después plazo | Cualquiera | Sin reembolso | Media | Baja |
| Modificación de reserva | Cualquiera | Cambio fechas | Media | Alta |

**Total casos recomendados:** 11-15 casos mínimos

---

## 🔗 REFERENCIAS

**Reglas comunes:**
- [CCOP_COMMON_RULES.md](../../../shared/Kepler/CCOP_COMMON_RULES.md)
- [SHARED_QA_RULES.md](../../../shared/SHARED_QA_RULES.md)

**Agente especializado:**
- [CCOP_QA_Assistant.agent.md](../../../agents/CCOP_QA_Assistant.agent.md)

**Azure DevOps:**
- Test Plan: [planId a definir]
- Test Suite Hoteles: [suiteId a definir]

---

## 📝 NOTAS DE IMPLEMENTACIÓN

**Estado:** 🔄 PENDIENTE DEFINICIÓN

**Pendientes:**
- [ ] Confirmar proveedor específico (HotelBeds/DerbySoft/Otro)
- [ ] Definir framework tecnológico (Angular/React/Otro)
- [ ] Definir modelo de pago exacto (slider, fee, tarjeta)
- [ ] Definir tipo de emisión/confirmación (inmediata/24h)
- [ ] Definir regímenes disponibles (solo hospedaje, desayuno, media pensión, todo incluido)
- [ ] Definir políticas de cancelación estándar
- [ ] Definir si aplican impuestos locales adicionales
- [ ] Crear matriz de casos de prueba completa
- [ ] Configurar suiteId "Hoteles" en Azure DevOps
- [ ] Validar con equipo de desarrollo
- [ ] Validar políticas con PO/PM

**Última actualización:** 2026-01-22  
**Responsable:** [A DEFINIR]
