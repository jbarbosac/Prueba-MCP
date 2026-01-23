# 📋 [CCOP] DISNEY EVENTOS ESPECIALES - Consolidación COP

> Documentación específica para el producto DISNEY EVENTOS ESPECIALES en Consolidación COP (Colombia).

---

## 🎯 IDENTIFICACIÓN

**Producto:** Disney Eventos Especiales  
**Portal:** Consolidación COP  
**País:** Colombia  
**Prefijo:** [CCOP]  
**Framework:** React  
**Estado:** 🔄 PENDIENTE DEFINICIÓN  

---

## 📦 PROVEEDORES

### **Proveedor Principal**
- **Nombre:** DerbySoft
- **Tecnología:** API REST
- **Eventos disponibles:**
  - Mickey's Very Merry Christmas Party (Noviembre-Diciembre)
  - Mickey's Not-So-Scary Halloween Party (Agosto-Octubre)
  - Epcot International Food & Wine Festival
  - Epcot International Flower & Garden Festival
  - Disney After Hours (eventos nocturnos exclusivos)
  - Disney Villains After Hours
  - Disney Early Morning Magic
  - Moonlight Magic (exclusivo DVC)
  - [OTROS EVENTOS - VALIDAR CATÁLOGO COMPLETO]

### **Proveedores Adicionales**
- [A DEFINIR si existen otros proveedores o ventas offline]

---

## 💰 MODELO DE PAGO

**Ecuación de pago:**
```
[A DEFINIR]
Ejemplo:
Producto (evento especial) = 100% USD
O
Producto (evento especial) = X% MILLAS + Y% USD
Fee = [SÍ/NO]
```

**Componentes:**
- **Producto:** [100% USD / Mixto / 100% Millas - A DEFINIR]
- **Moneda:** USD (según CCOP_COMMON_RULES.md)
- **Fee:** [Sí / No] - [Descripción del fee si aplica]
- **Tarjeta requerida:** [Sí / No]
- **Slider:** [Sí / No] - [Rango mínimo/máximo si aplica]

**Validaciones de pago:**
- Validar saldo/tarjeta suficiente antes de compra
- Validar disponibilidad del evento en fecha seleccionada
- Validar número de tickets vs disponibilidad
- [VALIDACIÓN 4 - A DEFINIR]

---

## 🔄 FLUJO DE COMPRA

### **1. BÚSQUEDA/SELECCIÓN**

**Campos obligatorios:**
- Tipo de evento especial (selección de lista)
- Fecha del evento (calendario con fechas disponibles)
- Número de tickets por categoría:
  - Adultos (10+ años)
  - Niños (3-9 años)
  - Infantes (0-2 años - política según evento)

**Validaciones:**
- Evento seleccionado debe tener fechas disponibles
- Fecha del evento no puede ser anterior a hoy
- Fecha debe ser una de las fechas programadas para ese evento
- Número de tickets válido (mínimo 1)
- [OTRAS - A DEFINIR]

### **2. RESULTADOS/DISPONIBILIDAD**

**Información mostrada:**
- Nombre del evento especial
- Descripción del evento:
  - Parque(s) incluido(s)
  - Horario del evento (ej: 7:00 PM - 12:00 AM)
  - Atracciones disponibles durante el evento
  - Shows y entretenimiento especial
  - Personajes disponibles
  - Comida/bebida incluida (si aplica)
- Fecha seleccionada
- Disponibilidad (tickets disponibles)
- Precio por categoría (adulto/niño) en USD
- Precio total en USD
- Política de cancelación específica del evento
- Términos y condiciones
- Galería de imágenes del evento

**Características especiales según evento:**
- **Halloween Party:** Trick-or-treating, shows exclusivos, desfile de villanos
- **Christmas Party:** Nieve artificial, shows navideños, galletas y chocolate caliente
- **After Hours:** Acceso limitado (pocos visitantes), tiempos de espera mínimos, snacks incluidos
- **Early Morning Magic:** Acceso temprano antes de apertura, desayuno incluido
- [OTROS - VALIDAR POR EVENTO]

### **3. DETALLE DEL EVENTO**

**Información completa:**
- Descripción detallada del evento
- Fecha y horario exacto
- Parque(s) donde se realiza
- Mapa del parque con áreas activas durante el evento
- Lista completa de atracciones disponibles
- Shows y horarios
- Encuentros con personajes programados
- Comida y bebida incluida (si aplica)
- Áreas de photopass
- Consejos y recomendaciones (qué llevar, cómo aprovechar el evento)
- Política de admisión (¿requiere ticket de parque regular?)
- Política de reingreso
- Política de clima (eventos bajo lluvia)
- Términos y condiciones completos
- Política de cancelación específica

**Selección:**
- Confirmación de fecha
- Confirmación de número de tickets por categoría
- [Agregar opciones especiales si aplican]

### **4. CHECKOUT**

**Datos de reserva:**

**a) Datos de asistentes:**
- Nombre completo del titular (debe coincidir con documento)
- Documento de identidad (Cédula/Pasaporte)
- Por cada asistente adicional:
  - Nombre completo
  - Edad (si es niño)

**b) Datos de contacto:**
- Email (para envío de tickets electrónicos)
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
- Tarjeta de Crédito/Débito (PlacetoPay) - **Cobro en USD**
- Pago en Agencia Física

**Validaciones Checkout:**
1. **Autenticación:** Usuario debe estar logueado
2. **Disponibilidad:** Confirmar disponibilidad en tiempo real antes de pago
3. **Datos completos:** Todos los campos obligatorios diligenciados
4. **Formato datos:** Email válido, teléfono válido, documento válido (10 dígitos CC)
5. **Método pago:** Tarjeta válida (con capacidad USD) o confirmación pago agencia
6. **Número de tickets:** No exceder disponibilidad del evento
7. **[OTRAS - A DEFINIR]**

### **5. CONFIRMACIÓN**

**Información mostrada:**
- ✅ Mensaje: "¡Compra confirmada!"
- Código de reserva (localizador único)
- Detalle de la compra:
  - Evento especial reservado
  - Fecha del evento
  - Horario del evento
  - Número de tickets (adultos/niños)
  - Precio total pagado en USD
- Instrucciones de uso:
  - Cómo acceder al parque (presentar confirmación o vincular a MagicBand)
  - Hora de inicio del evento
  - Dónde recoger brazalete/wristband de acceso (si aplica)
  - Qué llevar al evento
- Recomendaciones:
  - Llegar temprano
  - Descargar app My Disney Experience
  - Revisar horarios de shows y personajes
- Política de cancelación
- Botón: "Descargar tickets PDF"
- Botón: "Agregar a My Disney Experience"
- Botón: "Ver mis compras"

**Notificación email:**
- Email de confirmación con tickets adjuntos (PDF)
- Código QR para ingreso al evento
- Información completa del evento
- Instrucciones de uso
- Contacto soporte

---

## ✅ ESTADOS DE RESERVA

Los estados de reserva de Disney Eventos Especiales siguen el modelo estándar de CCOP:

| Estado | Descripción | Trigger |
|--------|-------------|---------|
| **EMITIDA** | Tickets confirmados y pagados | Pago exitoso + confirmación proveedor |
| **PENDIENTE** | En proceso de confirmación | Pago en agencia / confirmación manual / problemas proveedor |
| **CANCELADA** | Compra cancelada | Por usuario, por sistema, o por proveedor |

**Causas específicas de PENDIENTE:**
1. **Pago en agencia física:** Cliente no ha completado el pago
2. **Confirmación manual con proveedor:** Evento requiere validación adicional
3. **Problemas técnicos:** Fallo comunicación con proveedor DerbySoft, requiere retry

**Notificaciones por estado:**
- EMITIDA → Email con tickets PDF + código QR
- PENDIENTE → Email explicando causa + instrucciones
- CANCELADA → Email confirmando cancelación + términos de reembolso (si aplica)

---

## 🔍 VALIDACIONES ESPECÍFICAS

### **Validaciones de búsqueda:**
1. ✅ Evento especial seleccionado válido
2. ✅ Fecha del evento válida y futura
3. ✅ Fecha corresponde a una fecha programada del evento
4. ✅ Número de tickets válido (mínimo 1)

### **Validaciones de disponibilidad:**
1. ✅ Evento disponible para fecha seleccionada
2. ✅ Suficientes tickets disponibles para número solicitado
3. ✅ Evento no está sold out
4. ✅ Evento no ha sido cancelado por Disney

### **Validaciones de checkout:**
1. ✅ Usuario autenticado (login obligatorio)
2. ✅ Disponibilidad confirmada en tiempo real
3. ✅ Datos de asistentes completos y válidos
4. ✅ Documento válido (CC: 10 dígitos, Pasaporte: formato válido)
5. ✅ Email válido con formato correcto
6. ✅ Teléfono válido formato +57XXXXXXXXXX
7. ✅ Método de pago válido (tarjeta con capacidad USD)
8. ✅ [OTRAS - A DEFINIR]

### **Validaciones de políticas Disney:**
1. ✅ Edad de niños válida para categoría de precios
2. ✅ Compra cumple anticipación mínima [X días - A DEFINIR]
3. ✅ Tickets vinculables a cuenta My Disney Experience
4. ✅ [OTRAS - A DEFINIR según políticas Disney]

---

## 🚨 CASOS ESPECIALES

### **1. Cancelación del evento por Disney**
- [A DEFINIR]: Política de reembolso automático
- [A DEFINIR]: Notificación a clientes afectados
- [A DEFINIR]: Opciones de reprogramación
- [A DEFINIR]: Compensación adicional (si aplica)

### **2. Cambio de fecha por el cliente**
- [A DEFINIR]: ¿Se permiten cambios de fecha?
- [A DEFINIR]: Penalidades por cambio
- [A DEFINIR]: Sujeto a disponibilidad en nueva fecha
- [A DEFINIR]: Proceso de solicitud de cambio

### **3. Cancelaciones por el cliente**
- [A DEFINIR]: Política de cancelación (días antes del evento)
- [A DEFINIR]: Penalidades por cancelación (% de reembolso)
- [A DEFINIR]: Cancelaciones por fuerza mayor
- [A DEFINIR]: Proceso de solicitud de cancelación

### **4. No-Show (no presentarse al evento)**
- [A DEFINIR]: Política de no-show
- [A DEFINIR]: ¿Reembolso disponible?
- [A DEFINIR]: Notificación requerida

### **5. Eventos con clima adverso**
- [A DEFINIR]: ¿Eventos se cancelan por lluvia?
- [A DEFINIR]: Política de reembolso por clima
- [A DEFINIR]: Eventos se realizan bajo techo (parcial/total)
- [A DEFINIR]: Notificación al cliente

### **6. Requisitos especiales**
- Admisión para personas con discapacidad
- Restricciones de edad (algunos eventos 18+)
- Disfraces permitidos/prohibidos (ej: Halloween Party)
- [A DEFINIR]: ¿Cómo se gestionan estos casos?

---

## 📋 CASOS DE PRUEBA PRINCIPALES

### **[CCOP] [Home] Disney Eventos: Validar búsqueda de evento con datos válidos (+)**

**Precondiciones:**
- Usuario en home de Disney Eventos Especiales (sin login requerido)

**Pasos:**
1. Seleccionar tipo de evento: Mickey's Very Merry Christmas Party
2. Seleccionar fecha del evento: [Fecha futura válida programada]
3. Seleccionar 2 tickets adultos, 1 ticket niño
4. Clic en "Buscar disponibilidad"

**Resultado esperado:**
- Sistema muestra disponibilidad del evento
- Información completa del evento mostrada (horario, parque, descripción)
- Precio por categoría (adulto/niño) en USD
- Precio total en USD
- Botón "Comprar" disponible

---

### **[CCOP] [Availability] Disney Eventos: Validar detalle completo del evento (+)**

**Precondiciones:**
- Búsqueda realizada con disponibilidad confirmada

**Pasos:**
1. Ver detalle completo del evento
2. Revisar información: horarios, shows, atracciones, personajes
3. Validar política de cancelación
4. Clic en "Comprar ahora"

**Resultado esperado:**
- Sistema muestra detalle exhaustivo del evento
- Galería de imágenes del evento
- Lista de shows con horarios
- Lista de atracciones disponibles
- Política de cancelación visible
- Al comprar, sistema redirige a login (si no hay sesión activa)
- Tras login, redirige a checkout con selección preservada

---

### **[CCOP] [Checkout] Disney Eventos: Validar compra completa con Tarjeta PlacetoPay (+)**

**Precondiciones:**
- Usuario autenticado
- Evento y tickets seleccionados
- Disponibilidad confirmada

**Pasos:**
1. Completar datos de asistentes (titular + adicionales)
2. Completar datos de contacto (email, teléfono)
3. Completar datos de facturación (persona natural, CC)
4. Seleccionar método de pago: Tarjeta
5. Ingresar datos de tarjeta en PlacetoPay (tarjeta con capacidad USD)
6. Confirmar pago

**Resultado esperado:**
- Pago procesado exitosamente por PlacetoPay en USD
- Compra confirmada con proveedor DerbySoft
- Estado: EMITIDA
- Sistema muestra pantalla de confirmación con código de reserva
- Email enviado con tickets PDF adjuntos (código QR)
- Tickets descargables en PDF

---

### **[CCOP] [Checkout] Disney Eventos: Validar compra con Pago en Agencia (+)**

**Precondiciones:**
- Usuario autenticado
- Evento y tickets seleccionados

**Pasos:**
1. Completar todos los datos requeridos
2. Seleccionar método de pago: Pago en Agencia Física
3. Confirmar compra

**Resultado esperado:**
- Compra creada con estado: PENDIENTE
- Sistema muestra mensaje: "Compra pendiente de pago en agencia"
- Código de reserva generado
- Email enviado con instrucciones para completar pago en agencia
- Plazo de pago indicado (ej: 48 horas)

---

### **[CCOP] [Availability] Disney Eventos: Validar sin disponibilidad (Sold Out) (-)**

**Precondiciones:**
- Evento sin disponibilidad (sold out)

**Pasos:**
1. Seleccionar evento sold out
2. Seleccionar fecha sin disponibilidad
3. Intentar buscar

**Resultado esperado:**
- Sistema muestra mensaje: "Este evento está agotado para la fecha seleccionada"
- Sugerencia: "Prueba con otra fecha o evento"
- No permite continuar a compra
- Opción "Cambiar búsqueda" disponible

---

### **[CCOP] [Checkout] Disney Eventos: Validar error por fecha del evento en el pasado (-)**

**Precondiciones:**
- Usuario en búsqueda

**Pasos:**
1. Intentar seleccionar fecha del evento en el pasado
2. Intentar buscar

**Resultado esperado:**
- Sistema muestra error: "La fecha del evento debe ser futura"
- No ejecuta búsqueda hasta corregir fecha
- Campo fecha resaltado en rojo

---

### **[CCOP] [Checkout] Disney Eventos: Validar error por datos de asistentes incompletos (-)**

**Precondiciones:**
- Usuario en checkout con 2 tickets adultos

**Pasos:**
1. Completar datos solo del titular
2. Dejar campos del segundo adulto vacíos
3. Intentar proceder a pago

**Resultado esperado:**
- Sistema muestra error: "Debes completar los datos de todos los asistentes"
- Campos faltantes resaltados en rojo
- No permite continuar hasta completar todos los datos

---

### **[CCOP] [Checkout] Disney Eventos: Validar error por número de tickets excedido (-)**

**Precondiciones:**
- Evento con disponibilidad limitada (ej: 5 tickets disponibles)

**Pasos:**
1. Intentar comprar 10 tickets
2. Proceder a checkout

**Resultado esperado:**
- Sistema muestra error: "Solo quedan 5 tickets disponibles para este evento"
- Sugiere reducir número de tickets
- No permite continuar con compra de 10 tickets

---

## 🎭 EVENTOS ESPECIALES DISPONIBLES

### **1. Mickey's Very Merry Christmas Party**
- **Temporada:** Noviembre - Diciembre
- **Parque:** Magic Kingdom
- **Horario:** 7:00 PM - 12:00 AM
- **Incluye:** Shows navideños, nieve artificial, desfile, galletas y chocolate caliente, personajes con trajes navideños
- **Requiere ticket de parque regular:** No

### **2. Mickey's Not-So-Scary Halloween Party**
- **Temporada:** Agosto - Octubre
- **Parque:** Magic Kingdom
- **Horario:** 7:00 PM - 12:00 AM
- **Incluye:** Trick-or-treating, shows exclusivos, desfile de villanos, personajes raros
- **Disfraces:** Permitidos para todas las edades
- **Requiere ticket de parque regular:** No

### **3. Disney After Hours**
- **Disponibilidad:** Fechas selectas durante el año
- **Parques:** Magic Kingdom, Hollywood Studios, Animal Kingdom
- **Horario:** 3 horas después del cierre del parque
- **Incluye:** Acceso limitado (pocos visitantes), tiempos de espera mínimos, snacks y bebidas incluidos
- **Requiere ticket de parque regular:** No

### **4. Disney Early Morning Magic**
- **Disponibilidad:** Fechas selectas
- **Horario:** 1-2 horas antes de apertura del parque
- **Incluye:** Acceso temprano, desayuno incluido, atracciones selectas disponibles
- **Requiere ticket de parque regular:** Sí

### **5. Epcot Festivals**
- **Food & Wine Festival:** Julio - Noviembre
- **Flower & Garden Festival:** Marzo - Julio
- **Festival of the Arts:** Enero - Febrero
- **Incluye:** Eventos especiales, conciertos, degustaciones
- **Nota:** Algunos eventos del festival requieren ticket adicional
- [A DEFINIR: ¿Qué eventos específicos se venden en CCOP?]

### **[OTROS EVENTOS - A VALIDAR]**

---

## 📊 MÉTRICAS Y MONITOREO

**KPIs del producto:**
- Tasa de conversión (búsquedas → compras)
- Ticket promedio (valor promedio por compra)
- Tiempo promedio de checkout
- Tasa de cancelación
- Eventos más populares
- [OTROS - A DEFINIR]

**Errores a monitorear:**
- Fallos de integración con DerbySoft
- Fallos de pago (PlacetoPay en USD)
- Timeouts en búsqueda/disponibilidad
- Compras duplicadas
- Eventos sold out no reflejados correctamente
- [OTROS - A DEFINIR]

---

## 🔗 REFERENCIAS

**Documentación relacionada:**
- [CCOP_COMMON_RULES.md](../../shared/Reglas%20Marketplace/CCOP_COMMON_RULES.md) - Reglas comunes del portal
- [SHARED_QA_RULES.md](../../shared/SHARED_QA_RULES.md) - Estándares ISTQB y formato de casos
- [CCOP_DISNEY.md](./CCOP_DISNEY.md) - Producto Disney (Tickets parques)
- [CCOP_HOTELES_DISNEY.md](./CCOP_HOTELES_DISNEY.md) - Hoteles Disney

**Proveedores:**
- DerbySoft - API de eventos especiales Disney

**Azure DevOps:**
- Project: [A DEFINIR]
- Test Plan: [A DEFINIR]
- Test Suite Disney Eventos Especiales: [A DEFINIR]

---

## 📝 PENDIENTES DE DEFINICIÓN

**Alto impacto:**
- [ ] Modelo de pago completo (100% USD vs mixto con millas)
- [ ] Política de cancelación completa por tipo de evento
- [ ] Política de cambios de fecha
- [ ] Catálogo exacto de eventos vendidos en CCOP
- [ ] Requisito de ticket de parque regular por evento
- [ ] Anticipación mínima para compra

**Medio impacto:**
- [ ] Política de clima adverso (cancelaciones por lluvia)
- [ ] Proceso de vinculación a My Disney Experience
- [ ] Restricciones de edad por evento
- [ ] Políticas de disfraces (para Halloween Party)
- [ ] Horarios exactos de shows por evento
- [ ] Política de No-Show

**Bajo impacto:**
- [ ] Límite máximo de tickets por compra
- [ ] Descuentos por compra de múltiples eventos
- [ ] Opciones de accesibilidad por evento
- [ ] Fotografías específicas por evento

---

**Última actualización:** 2026-01-23  
**Responsable:** CCOP_QA_Assistant  
**Estado:** 🔄 En definición
