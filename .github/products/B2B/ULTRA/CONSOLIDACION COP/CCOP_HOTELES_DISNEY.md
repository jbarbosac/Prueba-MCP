# 📋 [CCOP] HOTELES DISNEY - Consolidación COP

> Documentación específica para el producto HOTELES DISNEY en Consolidación COP (Colombia).

---

## 🎯 IDENTIFICACIÓN

**Producto:** Hoteles Disney  
**Portal:** Consolidación COP  
**País:** Colombia  
**Prefijo:** [CCOP]  
**Framework:** Angular  
**Estado:** 🔄 PENDIENTE DEFINICIÓN  

---

## 📦 PROVEEDORES

### **Proveedor Principal**
- **Nombre:** HotelBeds
- **Tecnología:** API REST
- **Hoteles disponibles:**
  - Disney's Grand Floridian Resort & Spa
  - Disney's Contemporary Resort
  - Disney's Polynesian Village Resort
  - Disney's Wilderness Lodge
  - Disney's Beach Club Resort
  - Disney's Yacht Club Resort
  - Disney's BoardWalk Inn
  - Disney's Animal Kingdom Lodge
  - Disney's Caribbean Beach Resort
  - Disney's Port Orleans Resort (French Quarter y Riverside)
  - Disney's Coronado Springs Resort
  - Disney's All-Star Resorts (Movies, Music, Sports)
  - Disney's Pop Century Resort
  - Disney's Art of Animation Resort
  - [OTROS - VALIDAR CATÁLOGO COMPLETO]

### **Proveedores Adicionales**
- [A DEFINIR si existen otros proveedores]

---

## 💰 MODELO DE PAGO

**Ecuación de pago:**
```
[A DEFINIR]
Ejemplo:
Producto (hoteles Disney) = 100% COP
O
Producto (hoteles Disney) = X% MILLAS + Y% COP
Fee = [SÍ/NO]
```

**Componentes:**
- **Producto:** [100% Efectivo COP / Mixto / 100% Millas - A DEFINIR]
- **Fee:** [Sí / No] - [Descripción del fee si aplica]
- **Tarjeta requerida:** [Sí / No]
- **Slider:** [Sí / No] - [Rango mínimo/máximo si aplica]

**Validaciones de pago:**
- Validar saldo/tarjeta suficiente antes de compra
- Validar disponibilidad del hotel en fechas seleccionadas
- Validar número de habitaciones vs ocupación
- [VALIDACIÓN 4 - A DEFINIR]

---

## 🔄 FLUJO DE COMPRA

### **1. BÚSQUEDA**

**Campos obligatorios:**
- Destino: Orlando, Florida (Disney World)
- Fecha de Check-In
- Fecha de Check-Out
- Número de habitaciones
- Ocupación por habitación:
  - Adultos (18+ años)
  - Niños (0-17 años) → Validar rangos de edad por hotel
  - Edades de niños (requerido)

**Validaciones:**
- Check-In no puede ser anterior a hoy + [X días anticipación]
- Check-Out debe ser posterior a Check-In
- Mínimo 1 noche
- Máximo [X noches - A DEFINIR]
- Ocupación no puede exceder capacidad por habitación
- Número de niños requiere especificar edades

### **2. RESULTADOS**

**Información mostrada:**
- Nombre del hotel
- Categoría (Value / Moderate / Deluxe / Deluxe Villa)
- Tipo de habitación disponible
- Ocupación máxima
- Precio por noche en COP
- Precio total estadía (noches x habitaciones) en COP
- Amenidades incluidas:
  - Transporte gratuito a parques
  - Extra Magic Hours
  - MagicBand incluido
  - [OTRAS - A DEFINIR]
- Imágenes del hotel y habitaciones
- Ubicación relativa a parques
- Beneficios de huésped Disney (FastPass+, reservas restaurantes, etc.)

**Filtros disponibles:**
- Rango de precio
- Categoría de hotel (Value/Moderate/Deluxe)
- Servicios (piscina, restaurante, spa, etc.)
- Proximidad a parques específicos
- [OTROS - A DEFINIR]

**Opciones de ordenamiento:**
- Precio: menor a mayor / mayor a menor
- Categoría: Value → Deluxe
- Popularidad
- [OTROS - A DEFINIR]

### **3. DETALLE DE HOTEL**

**Información completa:**
- Descripción del hotel
- Galería de imágenes (habitaciones, áreas comunes, piscinas, restaurantes)
- Mapa de ubicación
- Amenidades y servicios:
  - Restaurantes
  - Piscinas (temáticas/recreativas/tranquilas)
  - Gimnasio
  - Spa
  - Actividades recreativas
  - Transporte a parques
- Tipos de habitación disponibles:
  - Standard View
  - Garden/Pool View
  - Water View
  - Theme Park View
  - Suites
- Ocupación máxima por tipo de habitación
- Política de cancelación específica
- Horarios Check-In / Check-Out
- Términos y condiciones

**Selección:**
- Tipo de habitación
- Número de habitaciones
- Confirmación de fechas y ocupación
- [Agregar opciones especiales si aplican]

### **4. CHECKOUT**

**Datos de reserva:**

**a) Datos de huéspedes:**
- Nombre completo del titular (debe coincidir con documento)
- Documento de identidad (Cédula/Pasaporte)
- Por cada huésped adicional:
  - Nombre completo
  - Edad (si es niño)

**b) Datos de contacto:**
- Email (para envío de confirmación)
- Teléfono de contacto (incluir código país +57)
- [OTROS - A DEFINIR]

**c) Datos de facturación:**
- Persona natural / jurídica
- Documento (NIT si es empresa)
- Nombre completo / Razón social
- Dirección
- Ciudad
- [OTROS - A DEFINIR]

**d) Método de pago:**
- Tarjeta de Crédito/Débito (PlacetoPay)
- Pago en Agencia Física

**Validaciones Checkout:**
1. **Autenticación:** Usuario debe estar logueado
2. **Disponibilidad:** Confirmar disponibilidad en tiempo real antes de pago
3. **Datos completos:** Todos los campos obligatorios diligenciados
4. **Formato datos:** Email válido, teléfono válido, documento válido (10 dígitos CC)
5. **Método pago:** Tarjeta válida o confirmación pago agencia
6. **[OTRAS - A DEFINIR]**

### **5. CONFIRMACIÓN**

**Información mostrada:**
- ✅ Mensaje: "¡Reserva confirmada!"
- Código de reserva (localizador único)
- Detalle de la reserva:
  - Hotel reservado
  - Fechas Check-In / Check-Out
  - Tipo y número de habitaciones
  - Huéspedes
  - Precio total pagado en COP
- Instrucciones Check-In:
  - Hora Check-In / Check-Out
  - Documentos requeridos
  - Dirección del hotel
- Instrucciones MagicBand (si aplica)
- Beneficios de huésped Disney disponibles
- Políticas de cancelación
- Botón: "Descargar voucher PDF"
- Botón: "Ver mis reservas"

**Notificación email:**
- Email de confirmación con voucher adjunto
- Información completa de la reserva
- Instrucciones para Check-In
- Contacto soporte

---

## ✅ ESTADOS DE RESERVA

Los estados de reserva de Hoteles Disney siguen el modelo estándar de CCOP:

| Estado | Descripción | Trigger |
|--------|-------------|---------|
| **EMITIDA** | Reserva confirmada y pagada | Pago exitoso + confirmación proveedor |
| **PENDIENTE** | En proceso de confirmación | Pago en agencia / confirmación manual / problemas proveedor |
| **CANCELADA** | Reserva cancelada | Por usuario, por sistema, o por proveedor |

**Causas específicas de PENDIENTE:**
1. **Pago en agencia física:** Cliente no ha completado el pago
2. **Confirmación manual con proveedor:** Hotel requiere validación adicional
3. **Problemas técnicos:** Fallo comunicación con proveedor, requiere retry

**Notificaciones por estado:**
- EMITIDA → Email con voucher + código reserva
- PENDIENTE → Email explicando causa + instrucciones
- CANCELADA → Email confirmando cancelación + términos de reembolso (si aplica)

---

## 🔍 VALIDACIONES ESPECÍFICAS

### **Validaciones de búsqueda:**
1. ✅ Fechas Check-In/Check-Out válidas y futuras
2. ✅ Mínimo 1 noche de estadía
3. ✅ Ocupación válida por habitación
4. ✅ Edades de niños especificadas

### **Validaciones de disponibilidad:**
1. ✅ Hotel disponible para fechas seleccionadas
2. ✅ Tipo de habitación disponible
3. ✅ Suficientes habitaciones disponibles

### **Validaciones de checkout:**
1. ✅ Usuario autenticado (login obligatorio)
2. ✅ Disponibilidad confirmada en tiempo real
3. ✅ Datos de huéspedes completos y válidos
4. ✅ Documento válido (CC: 10 dígitos, Pasaporte: formato válido)
5. ✅ Email válido con formato correcto
6. ✅ Teléfono válido formato +57XXXXXXXXXX
7. ✅ Método de pago válido
8. ✅ [OTRAS - A DEFINIR]

### **Validaciones de políticas Disney:**
1. ✅ Edad de niños válida para categoría de precios
2. ✅ Ocupación no excede máximo por tipo de habitación
3. ✅ Check-In cumple anticipación mínima [X días]
4. ✅ [OTRAS - A DEFINIR según políticas Disney]

---

## 🚨 CASOS ESPECIALES

### **1. Cambios de reserva**
- [A DEFINIR]: ¿Se permiten cambios de fecha?
- [A DEFINIR]: ¿Se permiten cambios de tipo de habitación?
- [A DEFINIR]: Penalidades por cambio
- [A DEFINIR]: Proceso de solicitud de cambio

### **2. Cancelaciones**
- [A DEFINIR]: Política de cancelación (días antes Check-In)
- [A DEFINIR]: Penalidades por cancelación (% de reembolso)
- [A DEFINIR]: Cancelaciones por fuerza mayor (huracanes, etc.)
- [A DEFINIR]: Proceso de solicitud de cancelación

### **3. Upgrade de habitación**
- [A DEFINIR]: ¿Se permite upgrade en sitio?
- [A DEFINIR]: Costo adicional de upgrade
- [A DEFINIR]: Disponibilidad sujeta a ocupación del hotel

### **4. No-Show (no presentarse)**
- [A DEFINIR]: Penalidades por no-show
- [A DEFINIR]: Política de reembolso
- [A DEFINIR]: Notificación requerida

### **5. Solicitudes especiales**
- Camas adicionales (cunas, camas plegables)
- Habitaciones accesibles (discapacidad)
- Habitaciones contiguas (familias numerosas)
- Ocasiones especiales (cumpleaños, aniversarios)
- [A DEFINIR]: ¿Cómo se gestionan estas solicitudes?

---

## 📋 CASOS DE PRUEBA PRINCIPALES

### **[CCOP] [Home] Hoteles Disney: Validar búsqueda con datos válidos (+)**

**Precondiciones:**
- Usuario en home de Hoteles Disney (sin login requerido)

**Pasos:**
1. Ingresar destino: Orlando (Disney World)
2. Seleccionar Check-In: [Fecha futura válida]
3. Seleccionar Check-Out: [Fecha posterior a Check-In]
4. Seleccionar 1 habitación, 2 adultos, 0 niños
5. Clic en "Buscar hoteles"

**Resultado esperado:**
- Sistema muestra listado de hoteles Disney disponibles
- Cada hotel muestra: nombre, categoría, precio por noche, precio total, imagen
- Filtros y ordenamiento disponibles

---

### **[CCOP] [Availability] Hoteles Disney: Validar selección de hotel y tipo de habitación (+)**

**Precondiciones:**
- Búsqueda realizada con resultados disponibles

**Pasos:**
1. Seleccionar un hotel del listado (ej: Disney's Contemporary Resort)
2. Ver detalle completo del hotel
3. Seleccionar tipo de habitación (ej: Standard View)
4. Validar ocupación y precio
5. Clic en "Reservar ahora"

**Resultado esperado:**
- Sistema muestra detalle completo del hotel con galería e información
- Tipos de habitación disponibles con precios diferenciados
- Al reservar, sistema redirige a login (si no hay sesión activa)
- Tras login, redirige a checkout con selección preservada

---

### **[CCOP] [Checkout] Hoteles Disney: Validar reserva completa con Tarjeta PlacetoPay (+)**

**Precondiciones:**
- Usuario autenticado
- Hotel y habitación seleccionados
- Disponibilidad confirmada

**Pasos:**
1. Completar datos de huéspedes (titular + adicionales)
2. Completar datos de contacto (email, teléfono)
3. Completar datos de facturación (persona natural, CC)
4. Seleccionar método de pago: Tarjeta
5. Ingresar datos de tarjeta en PlacetoPay
6. Confirmar pago

**Resultado esperado:**
- Pago procesado exitosamente por PlacetoPay
- Reserva confirmada con proveedor HotelBeds
- Estado: EMITIDA
- Sistema muestra pantalla de confirmación con código de reserva
- Email enviado con voucher adjunto
- Voucher descargable en PDF

---

### **[CCOP] [Checkout] Hoteles Disney: Validar reserva con Pago en Agencia (+)**

**Precondiciones:**
- Usuario autenticado
- Hotel y habitación seleccionados

**Pasos:**
1. Completar todos los datos requeridos
2. Seleccionar método de pago: Pago en Agencia Física
3. Confirmar reserva

**Resultado esperado:**
- Reserva creada con estado: PENDIENTE
- Sistema muestra mensaje: "Reserva pendiente de pago en agencia"
- Código de reserva generado
- Email enviado con instrucciones para completar pago en agencia
- Plazo de pago indicado (ej: 48 horas)

---

### **[CCOP] [Checkout] Hoteles Disney: Validar error por ocupación excedida (-)**

**Precondiciones:**
- Usuario en checkout
- Habitación seleccionada: Standard (máx. 4 personas)

**Pasos:**
1. Intentar reservar con 5 adultos en 1 habitación Standard
2. Proceder a checkout

**Resultado esperado:**
- Sistema muestra error: "La ocupación excede el máximo permitido para este tipo de habitación (máx. 4 personas)"
- No permite continuar hasta corregir ocupación
- Sugiere agregar habitaciones adicionales o cambiar tipo de habitación

---

### **[CCOP] [Checkout] Hoteles Disney: Validar error por fechas inválidas (-)**

**Precondiciones:**
- Usuario en búsqueda

**Pasos:**
1. Seleccionar Check-In: [Fecha pasada]
2. Intentar buscar

**Resultado esperado:**
- Sistema muestra error: "La fecha de Check-In debe ser futura"
- No ejecuta búsqueda hasta corregir fecha
- Campo Check-In resaltado en rojo

---

### **[CCOP] [Availability] Hoteles Disney: Validar sin disponibilidad para fechas seleccionadas (-)**

**Precondiciones:**
- Fechas de alta demanda o hotel sin disponibilidad

**Pasos:**
1. Buscar hotel para fechas sin disponibilidad
2. Ver resultados

**Resultado esperado:**
- Sistema muestra mensaje: "No hay disponibilidad para las fechas seleccionadas"
- Sugiere modificar fechas o seleccionar otro hotel
- Opción "Cambiar búsqueda" disponible

---

## 📊 MÉTRICAS Y MONITOREO

**KPIs del producto:**
- Tasa de conversión (búsquedas → reservas)
- Ticket promedio (valor promedio por reserva)
- Tiempo promedio de checkout
- Tasa de cancelación
- Tasa de No-Show
- [OTROS - A DEFINIR]

**Errores a monitorear:**
- Fallos de integración con HotelBeds
- Fallos de pago (PlacetoPay)
- Timeouts en búsqueda/disponibilidad
- Reservas duplicadas
- [OTROS - A DEFINIR]

---

## 🔗 REFERENCIAS

**Documentación relacionada:**
- [CCOP_COMMON_RULES.md](../../shared/Reglas%20Marketplace/CCOP_COMMON_RULES.md) - Reglas comunes del portal
- [SHARED_QA_RULES.md](../../shared/SHARED_QA_RULES.md) - Estándares ISTQB y formato de casos
- [CCOP_DISNEY.md](./CCOP_DISNEY.md) - Producto Disney (Tickets parques)
- [CCOP_DISNEY_EVENTOS_ESPECIALES.md](./CCOP_DISNEY_EVENTOS_ESPECIALES.md) - Disney Eventos Especiales

**Proveedores:**
- HotelBeds - API de hoteles Disney

**Azure DevOps:**
- Project: [A DEFINIR]
- Test Plan: [A DEFINIR]
- Test Suite Hoteles Disney: [A DEFINIR]

---

## 📝 PENDIENTES DE DEFINICIÓN

**Alto impacto:**
- [ ] Framework confirmado (Angular vs React)
- [ ] Modelo de pago completo (100% COP vs mixto con millas)
- [ ] Política de cancelación completa
- [ ] Política de cambios de reserva
- [ ] Catálogo completo de hoteles disponibles
- [ ] Rangos de edad para pricing de niños
- [ ] Anticipación mínima para reservas

**Medio impacto:**
- [ ] Amenidades exactas por categoría de hotel
- [ ] Proceso de solicitudes especiales (cunas, accesibilidad)
- [ ] Política de No-Show
- [ ] Política de upgrade de habitación
- [ ] Beneficios de huésped Disney exactos (FastPass+, etc.)

**Bajo impacto:**
- [ ] Límite máximo de noches
- [ ] Imágenes y descripciones específicas por hotel
- [ ] Actividades recreativas por hotel

---

**Última actualización:** 2026-01-23  
**Responsable:** CCOP_QA_Assistant  
**Estado:** 🔄 En definición
