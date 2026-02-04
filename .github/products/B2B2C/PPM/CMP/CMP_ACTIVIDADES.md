# 🎢 CMP - Flujo E2E de Actividades

> **Club Miles Perú** - Documentación completa del flujo End-to-End de Actividades y Tours

---

## 📌 Información General

| Campo           | Valor                                       |
| --------------- | ------------------------------------------- |
| **Marketplace** | Club Miles Perú (CMP)                       |
| **Producto**    | Actividades 🎢                              |
| **Tecnología**  | Angular                                     |
| **URL**         | https://demotravel-puntospe.smartlinks.dev/ |
| **Prefijo**     | `[CMP]`                                     |
| **Estado**      | ✅ Activo                                   |

---

## 🔌 Proveedor de Actividades

| Proveedor     | Tipo             | Cobertura   | Estado    |
| ------------- | ---------------- | ----------- | --------- |
| **HOTELBEDS** | Agregador Global | 180+ países | ✅ Activo |

**Características:**

- Proveedor único: HOTELBEDS
- Cobertura global de actividades y tours
- Tipos: Tours, Excursiones, Entradas, Experiencias, Traslados
- Sistema de búsqueda y reserva directo

---

## 🏗️ Arquitectura

```
┌─────────────────────────────────────────────────────┐
│       FLUJO E2E ACTIVIDADES - CLUB MILES PERÚ       │
└─────────────────────────────────────────────────────┘

1️⃣ LOGIN (PPM)
   └─ https://clubmilesperu.preprodppm.com/
      ├─ Ingresar credenciales
      ├─ Validar OTP
      └─ Sesión establecida

2️⃣ HOME (PPM)
   └─ Dashboard Club Miles Perú
      ├─ Ver saldo de millas
      └─ Clic en "Actividades" → Redirección cross-domain

3️⃣ MÓDULO ACTIVIDADES - HOME (Angular)
   └─ https://demotravel-puntospe.smartlinks.dev/activities
      ├─ Verificar sesión activa
      ├─ Formulario de búsqueda
      └─ Enviar búsqueda

4️⃣ DISPONIBILIDAD (Angular)
   └─ Resultados de búsqueda
      ├─ Listar actividades HOTELBEDS
      ├─ Filtros y ordenamiento
      └─ Seleccionar actividad y modalidad

5️⃣ CHECKOUT (Angular)
   └─ Confirmar reserva
      ├─ Datos de participantes
      ├─ ⚠️ Modelo de pago (pendiente confirmar)
      └─ Confirmación

6️⃣ CONFIRMACIÓN (Angular)
   └─ Resumen de reserva
      ├─ Código de confirmación/voucher
      ├─ Débito de millas
      └─ Email confirmación
```

---

## 📋 MÓDULO 1: HOME DE ACTIVIDADES

### **Objetivo**

Capturar criterios de búsqueda de actividades y tours

### **URL**

```
https://demotravel-puntospe.smartlinks.dev/activities
```

### **Precondiciones**

- ✅ Usuario autenticado en PPM
- ✅ Sesión activa transferida desde PPM
- ✅ VPN activa

### **Campos del Formulario de Búsqueda**

#### **1️⃣ Destino**

- **Tipo:** Autocomplete con búsqueda inteligente
- **Validación:** Ciudad, región o país válido
- **Formato:** Nombre ciudad/región
- **Ejemplo:** Lima, Cusco, Machu Picchu, Paracas
- **Búsqueda:** Permite búsqueda con nombre completo o tres primeras letras
- **Autocompletado:** Sugerencias dinámicas de ciudades y destinos turísticos
- **Cobertura:** Soporta búsquedas nacionales e internacionales

#### **2️⃣ Fecha de la Actividad**

- **Tipo:** Date picker con calendario
- **Validación:** Fecha futura (hoy + 1 día mínimo típicamente)
- **Formato:** Año/Mes/Día (según configuración regional)
- **Restricciones:** Sistema aplica restricciones de días mínimos/máximos adelante
- **No permite:** Seleccionar fechas pasadas
- **Nota:** Algunas actividades pueden permitir búsqueda sin fecha específica

#### **3️⃣ Participantes**

- **Tipo:** Selector con sub-configuración
- **Adultos:** 1-20 adultos
  - Contador con botones +/- o flechas
  - Opción de escribir cantidad directamente
  - Validación de límites máximos/mínimos
- **Niños (CHL):** 0-10 niños
  - Contador con botones +/- o flechas
  - Opción de escribir cantidad directamente
  - **Campo de edad obligatorio por cada niño**
  - Sistema genera automáticamente campo de edad al agregar niños
- **Infantes (INF):** Dependiendo de la actividad
  - **Campo de edad obligatorio por cada infante**
  - Sistema genera automáticamente campo de edad al agregar infantes

**Escenarios de búsqueda soportados:**

- **Búsquedas nacionales e internacionales:** Sistema diferencia y procesa correctamente ambos tipos
- **Con 1 adulto:** Búsqueda básica individual
- **Con múltiples adultos:** Grupos de adultos sin menores
- **Con múltiples adultos y niños:** Grupos familiares con composición mixta

#### **4️⃣ Categoría** (opcional)

- Tours culturales
- Aventura y deportes
- Entradas y tickets
- Gastronomía
- Traslados
- Experiencias únicas
- Vida nocturna
- Naturaleza y vida silvestre

### **Validaciones Críticas**

| Validación                       | Comportamiento Esperado                                                             |
| -------------------------------- | ----------------------------------------------------------------------------------- |
| **Fecha pasada**                 | Mensaje de error, bloquear búsqueda                                                 |
| **Destino vacío**                | Mensaje de error, resaltar campo requerido                                          |
| **Sin participantes**            | Asumir 1 adulto por defecto o requerir mínimo 1 adulto                              |
| **Edad de niño sin especificar** | Requerir edad si se seleccionan niños - Campo de edad obligatorio y visible         |
| **Edad de INF sin especificar**  | Requerir edad si se seleccionan infantes - Campo de edad obligatorio y visible      |
| **Campos obligatorios vacíos**   | Resaltar visualmente y mostrar mensaje de error específico                          |
| **Formato de fecha**             | Validar formato Año/Mes/Día según configuración regional                            |
| **Restricciones de edad**        | Validar si la actividad tiene restricciones de edad mínima o máxima para participar |

### **Acciones Disponibles**

- **Buscar:** Envía búsqueda a módulo de disponibilidad
- **Explorar categorías:** Navegar sin fecha específica
- **Limpiar:** Resetea formulario a valores por defecto
- **Volver:** Regresa a dashboard PPM

---

## 📋 MÓDULO 2: DISPONIBILIDAD DE ACTIVIDADES

### **Objetivo**

Mostrar actividades disponibles del proveedor HOTELBEDS

### **Descripción**

Módulo que muestra los resultados de búsqueda de actividades turísticas y experiencias disponibles desde HOTELBEDS. Incluye opciones de filtrado, visualización detallada de actividades, selección de fechas y cantidades, y funcionalidades específicas como modal de preguntas requeridas.

### **URL**

```
https://demotravel-puntospe.smartlinks.dev/activities/results
```

### **Precondiciones**

- ✅ Búsqueda enviada desde Home o navegación por categorías
- ✅ Criterios de búsqueda válidos
- ✅ Usuario autenticado
- ✅ Sesión activa

### **Estructura de Resultados**

#### **Sección Superior: Resumen de Búsqueda**

- Destino
- Fecha seleccionada (si aplica)
- Participantes
- **Botón "Modificar búsqueda"** → Regresa a Home con criterios precargados

#### **Sección Principal: Listado de Actividades**

**Información por Actividad:**

| Campo                 | Descripción                                   |
| --------------------- | --------------------------------------------- |
| **Nombre**            | Título de la actividad o tour                 |
| **Categoría**         | Tipo de actividad                             |
| **Duración**          | Horas, días, o "Flexible"                     |
| **Foto Principal**    | Imagen destacada                              |
| **Calificación**      | Rating de usuarios (si disponible)            |
| **Descripción Corta** | Resumen de la experiencia                     |
| **Precio en Millas**  | ⚠️ Modelo pendiente confirmar                 |
| **Copago**            | ⚠️ Si aplica Slider                           |
| **Cancelación**       | Política (Gratuita hasta X / No reembolsable) |
| **Disponibilidad**    | Fechas o días disponibles                     |
| **Idiomas**           | Español, Inglés, etc.                         |

#### **Filtros Disponibles**

| Filtro           | Opciones                             |
| ---------------- | ------------------------------------ |
| **Precio**       | Rango de millas                      |
| **Categoría**    | Tours, Aventura, Entradas, etc.      |
| **Duración**     | Medio día, Día completo, Varios días |
| **Calificación** | Rango de rating                      |
| **Cancelación**  | Gratuita, Parcial, No reembolsable   |
| **Idioma**       | Español, Inglés, Otros               |
| **Horario**      | Mañana, Tarde, Noche, Todo el día    |
| **Incluye**      | Comida, Transporte, Guía, Entrada    |

#### **Ordenamiento**

- Precio menor a mayor
- Calificación mayor a menor
- Duración
- Popularidad
- Nombre alfabéticamente

### **Escenarios Posibles**

#### **✅ Resultados Encontrados**

- Mostrar actividades disponibles de HOTELBEDS
- Permitir selección de actividad y modalidad

#### **⚠️ Sin Resultados**

- Mensaje claro: "No se encontraron actividades para tu búsqueda"
- Sugerencias: Modificar fecha, destino, o explorar todas las categorías
- Botón "Nueva búsqueda"

#### **❌ Error de Proveedor**

- Mensaje genérico de error
- Opción de reintentar
- No exponer detalles técnicos

### **Selección de Actividad**

#### **Paso 1: Ver Detalles de la Actividad**

Al hacer clic en una actividad, mostrar:

- Galería de fotos
- Descripción completa
- Itinerario detallado (si aplica)
- Qué incluye / Qué no incluye
- Punto de encuentro / Recogida
- Duración exacta
- Idiomas disponibles
- Restricciones (edad, condición física, etc.)
- Políticas de cancelación
- Calificaciones y reseñas de usuarios

#### **Paso 2: Seleccionar Modalidad**

Algunas actividades tienen modalidades:

| Modalidad                | Descripción                  |
| ------------------------ | ---------------------------- |
| **Horario**              | Mañana, Tarde, Noche         |
| **Tipo de tour**         | Privado, Compartido          |
| **Opciones adicionales** | Con almuerzo, Sin almuerzo   |
| **Nivel de dificultad**  | Básico, Intermedio, Avanzado |
| **Transporte**           | Con recogida, Sin recogida   |

#### **Paso 3: Seleccionar Fecha y Cantidad**

1. Elegir fecha específica (si requerido)
2. Especificar cantidad de participantes:
   - Adultos
   - Niños (con edades)
   - Seniors (si aplica descuento)
3. Sistema valida disponibilidad
4. Muestra precio total en millas
5. Botón "Continuar a checkout" se activa

---

## 📋 MÓDULO 3: CHECKOUT

### **Objetivo**

Capturar datos de participantes, información de contacto y procesar el pago para confirmar la reserva de actividad.

### **Descripción**

Módulo de finalización de compra para actividades y experiencias donde se capturan los datos de los participantes, información de contacto, se procesan métodos de pago y se genera la confirmación de reserva. Incluye validaciones específicas de actividades turísticas, cantidad de participantes y métodos de pago.

### **URL**

```
https://demotravel-puntospe.smartlinks.dev/activities/checkout
```

### **Precondiciones**

- ✅ Actividad y modalidad seleccionadas desde módulo de Disponibilidad
- ✅ Usuario autenticado
- ✅ Sesión activa

---

### **🔹 Resumen de Reserva**

**Descripción:** Pantalla inicial del checkout que consolida la información de la actividad seleccionada antes de capturar datos de participantes, permitiendo verificar detalles, fecha y aplicación de puntos.

**Componentes:**

- **Información de la actividad:**
  - Nombre completo de la actividad
  - Descripción completa
  - Categoría (Tour, Entrada, Aventura, Gastronomía, etc.)
  - Imagen principal de la actividad
  - Duración de la actividad
  - Idiomas disponibles

- **Fecha y hora:**
  - Fecha de la actividad (formato: Día, DD de Mes de AAAA)
  - Hora de inicio (si aplica horario específico)
  - Punto de encuentro o salida con dirección exacta

- **Participantes:**
  - Cantidad de adultos
  - Cantidad de niños (con edades si aplica)
  - Cantidad de infantes (si aplica)

- **Qué incluye / Qué no incluye:**
  - Lista detallada de lo que incluye la actividad
  - Lista de lo que NO incluye

- **Desglose de precios:**
  - Precio por persona (adulto/niño/senior)
  - Cantidad de participantes
  - Subtotal
  - Fee de servicio
  - **Total en millas**

- **Desglose de puntos:**
  - Puntos requeridos para la reserva
  - Saldo disponible en cuenta
  - Valor de canje

- **Distribución para copago (si aplica):**
  - Slider de puntos vs cash
  - Cálculo dinámico de monto

- **Políticas:**
  - Políticas de cancelación de la actividad
  - Restricciones (edad, condición física, etc.)

- **Botón "Continuar":** Avanza al formulario de participantes

**Comportamiento esperado:**

1. Muestra toda la información de la actividad seleccionada de manera clara y estructurada
2. Fecha y horario de la actividad son visibles y destacados
3. Calcula correctamente puntos requeridos y saldo disponible
4. Para copago, permite distribuir entre puntos y dinero con slider
5. Valida saldo suficiente de puntos antes de continuar
6. Precio se calcula correctamente: precio por persona × cantidad de participantes
7. Diferencia precios si hay tarifas distintas para adultos y niños
8. Políticas de cancelación son visibles y claras
9. Información de punto de encuentro es específica y útil
10. Qué incluye/no incluye es claro y legible

---

### **🔹 Datos de Contacto**

**Descripción:** Sección del checkout que captura la información de contacto del responsable de la reserva para notificaciones, confirmaciones y vouchers.

**Componentes:**

- **Nombre** (campo de texto)
- **Apellido** (campo de texto)
- **Email\*** (campo de texto con validación)
- **Teléfono\*** (campo numérico con código de país)
- **Hotel/Dirección de recogida** (si la actividad incluye transporte)
- Indicadores de campo obligatorio (\*)
- Validaciones en tiempo real
- Mensajes de error específicos

**Comportamiento esperado:**

1. Todos los campos son obligatorios
2. Solo permite letras y espacios en nombre/apellido (permite tildes y ñ)
3. Email debe incluir @ y dominio válido (.com, .co, .net, etc.)
4. Teléfono valida longitud según código de país seleccionado
5. Campo de hotel/dirección aparece solo si la actividad incluye recogida
6. Validaciones funcionan en tiempo real al escribir
7. No permite continuar sin datos completos y válidos
8. Información se usa para envío de confirmaciones, vouchers y comunicación
9. Muestra mensajes de error específicos por campo

---

### **🔹 Formulario de Datos de Participantes**

**Descripción:** Formulario obligatorio en el checkout donde se capturan los datos personales de todos los participantes de la actividad.

**Componentes:**

**Sección por cada participante:**

- Encabezado: "Participante 1", "Participante 2", etc.
- Diferenciación visual entre adultos y niños

**Campos por participante:**

- **Nombre\*** (campo de texto, máximo 2 nombres)
- **Apellido\*** (campo de texto, máximo 2 apellidos)
- **Tipo de documento\*** (dropdown: DNI, CE, Pasaporte)
- **Número de documento\*** (campo alfanumérico)
- **Fecha de nacimiento\*** (datepicker)
- **Género\*** (dropdown: Masculino/Femenino)

**Para participante principal:**

- **Email\*** (campo de texto con validación)
- **Teléfono de contacto\*** (campo numérico con código de país)

**Funcionalidades:**

- Sistema genera un formulario por cada participante según búsqueda original
- Precarga automática de datos del usuario logueado en participante principal
- Indicadores de campo obligatorio (\*)
- Validaciones en tiempo real
- Mensajes de error específicos por campo
- Usuario puede editar datos precargados

**Comportamiento esperado:**

1. Sistema genera formulario por cada participante según búsqueda original
2. Valida que cantidad de participantes coincida con búsqueda original
3. Datos del usuario logueado se precargan en participante principal
4. Solo permite letras y espacios en nombres/apellidos (permite tildes y ñ)
5. Máximo 2 nombres y 2 apellidos por participante
6. Valida edad si hay restricciones de edad para la actividad
7. Para niños, valida que la edad esté dentro del rango permitido
8. No permite fechas de nacimiento futuras
9. Validaciones funcionan en tiempo real
10. Muestra mensajes de error claros por cada validación
11. Formato de documento valida según tipo seleccionado

---

### **🔹 Solicitudes Especiales** (opcional)

**Descripción:** Sección opcional que permite al usuario agregar solicitudes o preferencias especiales para la actividad.

**Componentes:**

- **Restricciones alimenticias** (checkbox o campo de texto)
- **Necesidades especiales** (campo de texto libre)
  - Movilidad reducida
  - Alergias
  - Requerimientos médicos
- **Preferencias** (campo de texto libre)
- **Información de contacto de emergencia** (si la actividad lo requiere)
- **Comentarios adicionales** (campo de texto libre, área de texto)
- Indicación: "Estas solicitudes serán comunicadas al proveedor"

**Comportamiento esperado:**

1. Todos los campos son opcionales (excepto contacto de emergencia si es requerido)
2. Permite escribir solicitudes en texto libre
3. Sistema envía solicitudes al proveedor con la confirmación
4. Muestra mensaje claro indicando que solicitudes son comunicadas al proveedor
5. No bloquea el proceso de compra si no se completan (excepto campos obligatorios)
6. Información se incluye en voucher y correo de confirmación
7. Si actividad requiere contacto de emergencia, campo aparece y se valida

---

### **🔹 Servicios Adicionales (Upsell)**

**Descripción:** Sección opcional del checkout que permite agregar servicios extras a la actividad (traslados, comidas, seguro de viaje, upgrade de experiencia).

**Componentes:**

- Cards de servicios disponibles con descripción detallada
- Precio en puntos o moneda por servicio
- Checkboxes para selección de servicios
- Descripción clara de qué incluye cada servicio adicional
- Ejemplos:
  - Traslado desde/hacia hotel
  - Almuerzo o cena incluida
  - Seguro de viaje/cancelación
  - Upgrade de experiencia (tour privado, grupo pequeño)
  - Fotografía profesional
- Resumen de total actualizado al seleccionar
- Servicios varían según actividad y proveedor

**Comportamiento esperado:**

1. Muestra solo servicios activos y disponibles para la actividad seleccionada
2. Cada servicio tiene descripción clara y precio visible
3. Indica claramente si precio es por persona o total del grupo
4. Checkboxes funcionan correctamente
5. Total se actualiza automáticamente al seleccionar/deseleccionar
6. Precio de servicios se calcula correctamente (por persona o total según aplique)
7. Admin refleja los servicios contratados en la reserva
8. Permite continuar sin seleccionar servicios (son opcionales)

---

### **🔹 Métodos de Pago**

**Descripción:** Sección del checkout que permite seleccionar la forma de pago para la reserva de actividad, incluyendo Solo Puntos, copago (Puntos + Cash), PSE y métodos de pago con tarjetas por país.

**Componentes:**

- Selector de método de pago: Solo Puntos, Copago, PSE, Tarjeta de crédito/débito
- Formulario de tarjeta: Número, Titular, Fecha de expiración, CVV
- Slider de distribución para copago (puntos vs cash)
- Selector de banco para PSE
- Indicador de saldo de puntos disponibles
- Resumen de pago con desglose final
- Validación de datos de tarjeta encriptados
- Pasarelas por país: Colombia, Perú, Ecuador, México, Chile
- Campo Fee de procesamiento visible

**Consideraciones especiales:**

- **Privacidad en Checkout:** En el resumen de compra con "Solo Puntos", la dirección IP debe estar oculta tanto en desktop como en mobile

**Comportamiento esperado:**

1. **Selección de "Solo Puntos":**
   - Sistema bloquea cantidad exacta de puntos de la cuenta del usuario
   - No solicita información de tarjeta de crédito
   - Fee de procesamiento se aplica correctamente
   - Dirección IP oculta en resumen de compra (desktop y mobile)
   - Al confirmar, debe procesar el pago y navegar a Confirmación

2. **Selección de "Copago":**
   - Slider permite ajustar proporción de puntos vs. cash
   - Sistema recalcula en tiempo real el monto en puntos y moneda
   - Habilita campos para método de pago externo (tarjeta de crédito)
   - Fee se aplica sobre el monto total

3. Sistema valida saldo de puntos suficiente para pago total o copago
4. Formulario de tarjeta valida todos los campos obligatorios antes de continuar
5. Datos de tarjeta se envían encriptados (PCI-DSS compliant)
6. PSE redirige a pasarela bancaria y retorna correctamente al sitio
7. Puntos se bloquean al confirmar reserva
8. Pasarelas por país funcionan según configuración regional
9. Si pago falla, puntos no quedan bloqueados
10. Mensajes de error de pago son claros y ofrecen opción de reintentar

---

### **🔹 Validaciones Adicionales**

**Descripción:** Conjunto de validaciones complementarias que garantizan la seguridad, integridad y optimización del proceso de checkout de actividades.

**Componentes:**

- Validación de cantidad de participantes según capacidad de la actividad
- Validación de restricciones de edad (si aplica)
- Validación de condición física requerida (si aplica)
- Encriptación de datos sensibles (tarjetas)
- Manejo de errores del servicio de pagos
- Checkbox "Requiero Factura" con campos de empresa y NIT/RFC/RUC
- Checkbox de términos y condiciones con link a políticas completas
- Aceptación de políticas de cancelación específicas de la actividad
- Validación de llamados de servicio (evitar duplicados)
- Validación de disponibilidad en fecha seleccionada
- Información de contacto de emergencia (si la actividad lo requiere)
- Validación de privacidad (ocultamiento de dirección IP con Solo Puntos)

**Comportamiento esperado:**

1. Sistema valida que cantidad de participantes no exceda capacidad máxima de la actividad
2. Valida restricciones de edad si la actividad tiene límites (ej: mayores de 12 años)
3. Si requiere nivel físico específico, muestra advertencia o validación
4. Muestra mensaje claro si hay restricciones no cumplidas
5. Datos de tarjeta se envían encriptados (validable en Network → Request Payload)
6. Errores de pago muestran mensajes claros con opción de reintentar
7. Puntos no quedan bloqueados si la transacción falla
8. Campo de factura aparece solo si se activa el checkbox
9. Campos de empresa y NIT/RFC/RUC validan formato correcto
10. No permite continuar sin aceptar términos y condiciones generales
11. Políticas de cancelación específicas de la actividad deben ser aceptadas
12. Link a términos completos funciona y muestra políticas
13. Servicio Create se invoca una única vez al cargar checkout (validar en Network)
14. Si actividad requiere información de emergencia, campos aparecen y se validan
15. Valida disponibilidad de la actividad en la fecha seleccionada antes de confirmar
16. Si actividad está agotada, muestra mensaje y no permite continuar
17. En pago con "Solo Puntos", dirección IP debe estar oculta en resumen (desktop y mobile)

---

## 📋 MÓDULO 4: CONFIRMACIÓN

### **Objetivo**

Mostrar resumen completo de la reserva de actividad confirmada exitosamente después de procesar el pago.

### **Descripción**

Pantalla final que muestra la confirmación de la reserva de actividad con todos los detalles, envío de voucher/confirmación por correo y canales de soporte.

### **URL**

```
https://demotravel-puntospe.smartlinks.dev/activities/confirmation
```

### **Precondiciones**

- ✅ Pago procesado exitosamente
- ✅ Reserva confirmada
- ✅ Puntos debitados

---

### **🔹 Código de Reserva / Voucher**

**Descripción:** Código único de la reserva o voucher que identifica la transacción.

**Componentes:**

- Código de reserva/voucher visible y destacado
- Formato alfanumérico único
- Texto explicativo: "Tu código de reserva es:" o "Número de voucher:"
- Opción de copiar código fácilmente
- Código QR (si aplica para escaneo en la actividad)

**Comportamiento esperado:**

1. Código se muestra inmediatamente después de pago exitoso
2. Código es único para cada reserva
3. Formato es claro y legible
4. Usuario puede copiar código fácilmente
5. Código aparece en el correo de confirmación
6. Si aplica código QR, es escaneable y válido
7. Sistema registra código en Admin para seguimiento

---

### **🔹 Información de la Actividad Confirmada**

**Descripción:** Sección que muestra el resumen de la actividad reservada.

**Componentes:**

- Nombre completo de la actividad
- Descripción breve
- Categoría (Tour, Entrada, Aventura, Gastronomía, etc.)
- Imagen principal de la actividad
- Duración de la actividad
- Idiomas disponibles

**Comportamiento esperado:**

1. Información coincide exactamente con la actividad seleccionada
2. Imagen de la actividad se muestra correctamente
3. Todas las características son visibles y legibles
4. Datos son consistentes con disponibilidad y checkout

---

### **🔹 Fecha, Hora y Punto de Encuentro**

**Descripción:** Sección que muestra la información crítica sobre cuándo y dónde se realiza la actividad.

**Componentes:**

**Fecha y hora:**

- Fecha de la actividad (formato: Día de la semana, DD de Mes de AAAA)
- Hora de inicio (formato: HH:MM o "A partir de las HH:MM")
- Duración estimada de la actividad

**Punto de encuentro:**

- Ubicación exacta con dirección completa
- Nombre del lugar (hotel, plaza, terminal, etc.)
- Referencias adicionales para localización
- Mapa o enlace a mapa (si disponible)

**Información de recogida** (si aplica):

- Si la actividad incluye recogida en hotel
- Hora estimada de recogida
- Dirección del hotel ingresada

**Comportamiento esperado:**

1. Fecha y hora son prominentes y destacadas
2. Información de punto de encuentro es específica y útil
3. Si incluye recogida, horario y dirección son claros
4. Duración de la actividad es visible
5. Referencias ayudan a la localización

---

### **🔹 Datos de Participantes**

**Descripción:** Sección que muestra la información de los participantes registrados en la reserva.

**Componentes:**

**Participante Principal:**

- Nombre completo
- Tipo y número de documento
- Email de contacto
- Teléfono de contacto

**Participantes Adicionales:**

- Nombre completo de cada participante
- Tipo y número de documento
- Diferenciación de adultos y niños

**Solicitudes Especiales** (si aplica):

- Restricciones alimenticias comunicadas
- Necesidades especiales informadas
- Comentarios adicionales

**Comportamiento esperado:**

1. Todos los datos coinciden con los ingresados en el checkout
2. Información es legible y correctamente organizada
3. Datos sensibles pueden estar parcialmente enmascarados si aplica
4. Lista todos los participantes de la reserva
5. Solicitudes especiales son visibles si fueron ingresadas

---

### **🔹 Desglose de Pago**

**Descripción:** Sección que muestra el desglose completo del pago realizado.

**Componentes:**

- Precio base por persona (adulto/niño/senior)
- Cantidad de participantes por tipo
- Subtotal de actividad
- Servicios adicionales contratados con precios:
  - Traslados
  - Comidas
  - Seguro
  - Upgrades
- Fee de servicio
- **Total pagado en millas**
- Método de pago usado (Solo Puntos / Copago)
- Puntos debitados de la cuenta

**Comportamiento esperado:**

1. Cantidades muestran separador de miles (punto)
2. Total de Millas debitadas refleja el débito de la cuenta del usuario
3. Valores son consistentes con el precio mostrado en disponibilidad y checkout
4. Servicios adicionales se listan individualmente con sus precios
5. Desglose es claro y fácil de entender
6. Método de pago utilizado es visible
7. Cálculo de precio por persona × cantidad es correcto

---

### **🔹 Qué Llevar / Recomendaciones**

**Descripción:** Sección con información importante sobre qué debe llevar el participante y recomendaciones para la actividad.

**Componentes:**

**Qué llevar:**

- Documento de identidad o pasaporte
- Ropa cómoda o adecuada para la actividad
- Calzado apropiado
- Protección solar, sombrero, agua
- Cámara (si se permite)
- Artículos específicos de la actividad

**Recomendaciones:**

- Llegar 10-15 minutos antes
- Consideraciones climáticas
- Restricciones de equipaje o pertenencias
- Políticas de fotografía

**Comportamiento esperado:**

1. Lista es específica para el tipo de actividad
2. Recomendaciones son claras y prácticas
3. Información ayuda al participante a prepararse
4. Destacadas visualmente para fácil lectura

---

### **🔹 Políticas y Condiciones**

**Descripción:** Sección con información importante sobre políticas de la actividad.

**Componentes:**

**Políticas de cancelación:**

- Descripción de política aplicable (Gratuita hasta X / Parcial / No reembolsable)
- Fechas límite para cancelación sin cargo
- Cargos por cancelación si aplican

**Política de no-show:**

- Consecuencias de no presentarse
- Reembolsos (si aplican)

**Restricciones:**

- Edad mínima o máxima
- Condición física requerida
- Restricciones de salud

**Reembolsos por cancelación del proveedor:**

- Política si la actividad se cancela por mal clima
- Política si la actividad se cancela por falta de quórum
- Alternativas ofrecidas

**Comportamiento esperado:**

1. Políticas son claras y comprensibles
2. Fechas límite de cancelación son específicas
3. Condiciones importantes están destacadas
4. Políticas coinciden con las mostradas en disponibilidad y checkout
5. Restricciones son visibles y claras

---

### **🔹 Confirmación por Correo y Canales de Soporte**

**Descripción:** Sección que notifica sobre el envío del voucher/confirmación por correo y proporciona canales de comunicación.

**Componentes:**

**Banner de correo:**

- Ícono de sobre/correo
- Mensaje principal: "Tu voucher de confirmación ha sido enviado a [email]."
- Mensaje secundario: "En caso de no recibirlo, revise la bandeja de Correo no deseado."

**Canales de soporte:**

- WhatsApp con número de contacto
- Teléfono de atención al cliente
- Email de contacto
- Horarios de atención

**Información del proveedor** (si disponible):

- Contacto directo del proveedor de la actividad
- Número de emergencia durante la actividad

**Botones de acción:**

- **"Ver Resumen":** Muestra detalle completo de la reserva
- **"Descargar Voucher":** Genera PDF con todos los detalles
- **"Imprimir":** Abre diálogo de impresión
- **"Regresar al Home":** Vuelve al widget de búsqueda

**Comportamiento esperado:**

1. Correo de confirmación con voucher se envía automáticamente
2. Correo incluye todos los detalles: código, actividad, fecha, hora, punto de encuentro, participantes
3. Voucher incluye código QR si aplica
4. Formato del correo/voucher es correcto y profesional
5. Banner de notificación es visible y claro
6. Canales de soporte (WhatsApp, teléfono) son funcionales y visibles
7. Números de contacto y horarios son correctos
8. Botón "Ver Resumen" muestra información consistente
9. Botón "Descargar Voucher" genera PDF correctamente
10. PDF incluye: código/voucher, actividad, fecha, hora, punto de encuentro, participantes, qué llevar, políticas
11. Botón "Imprimir" abre diálogo de impresión del navegador
12. Botón "Regresar al Home" limpia el flujo y vuelve al inicio
13. Eventos de conversión (Meta Ads Pixel, Google Ads) se disparan correctamente
14. Voucher es presentable y contiene toda la información necesaria para el proveedor
15. Información de punto de encuentro, fecha y hora es clara y destacada en el voucher

---

## 🧪 Casos de Prueba Recomendados

### **Prioridad 1 (Crítica)**

| ID          | Título                                                               | Escenario                   |
| ----------- | -------------------------------------------------------------------- | --------------------------- |
| CMP-ACT-001 | [CMP] Actividades - Tour 1 día - HotelBeds - 2 adultos               | Flujo completo exitoso      |
| CMP-ACT-002 | [CMP] Actividades - Entrada museo - HotelBeds - Cancelación gratuita | Flujo completo exitoso      |
| CMP-ACT-003 | [CMP] Actividades - Sesión cross-domain - Validar persistencia       | Navegación PPM → Angular    |
| CMP-ACT-004 | [CMP] Actividades - Sin resultados - Mensaje error                   | Búsqueda sin disponibilidad |
| CMP-ACT-005 | [CMP] Actividades - Fecha pasada - Validación                        | Error de validación         |

### **Prioridad 2 (Alta)**

| ID          | Título                                                          | Escenario           |
| ----------- | --------------------------------------------------------------- | ------------------- |
| CMP-ACT-006 | [CMP] Actividades - Tour privado - 4 adultos + 2 niños          | Flujo completo      |
| CMP-ACT-007 | [CMP] Actividades - Filtros múltiples - Aventura + Día completo | Validar filtrado    |
| CMP-ACT-008 | [CMP] Actividades - Modificar búsqueda - Precarga criterios     | Edición de búsqueda |
| CMP-ACT-009 | [CMP] Actividades - Ver detalles - Itinerario completo          | Validar información |
| CMP-ACT-010 | [CMP] Actividades - Seleccionar modalidad - Con almuerzo        | Flujo completo      |

### **Prioridad 3 (Media)**

| ID          | Título                                       | Escenario            |
| ----------- | -------------------------------------------- | -------------------- |
| CMP-ACT-011 | [CMP] Actividades - Ordenar por calificación | Validar ordenamiento |
| CMP-ACT-012 | [CMP] Actividades - Filtrar por categoría    | Validar filtrado     |
| CMP-ACT-013 | [CMP] Actividades - Volver a Home PPM        | Navegación inversa   |
| CMP-ACT-014 | [CMP] Actividades - Timeout de búsqueda      | Manejo de error      |
| CMP-ACT-015 | [CMP] Actividades - Error de proveedor       | Manejo de error      |

---

## 🎯 Tipos de Actividades Disponibles

### **Categorías Comunes**

| Categoría            | Ejemplos                              | Características                  |
| -------------------- | ------------------------------------- | -------------------------------- |
| **Tours Culturales** | City tours, Museos, Sitios históricos | Duración variable, guía incluido |
| **Aventura**         | Rafting, Parapente, Tirolesa          | Restricciones de edad/salud      |
| **Entradas**         | Atracciones, Parques, Eventos         | Fecha específica requerida       |
| **Gastronomía**      | Tours gastronómicos, Cooking class    | Incluye comida                   |
| **Traslados**        | Aeropuerto-hotel, Privados            | Horario flexible                 |
| **Naturaleza**       | Avistamiento fauna, Trekking          | Nivel físico requerido           |
| **Experiencias**     | Spa, Workshops, Clases                | Reserva anticipada               |

---

## 📊 Comparación con Otros Modelos Kepler

| Aspecto          | PM           | BGR          | CME          | PROM         | **CMP**           |
| ---------------- | ------------ | ------------ | ------------ | ------------ | ----------------- |
| **Proveedor**    | HOTELBEDS    | HOTELBEDS    | HOTELBEDS    | HOTELBEDS    | **HOTELBEDS**     |
| **Tecnología**   | N/A          | N/A          | N/A          | N/A          | **Angular**       |
| **Arquitectura** | Monolítica   | Monolítica   | Monolítica   | Monolítica   | **Multi-dominio** |
| **Emisión**      | ⚠️ Pendiente | ⚠️ Pendiente | ⚠️ Pendiente | ⚠️ Pendiente | **⚠️ Pendiente**  |
| **Cobertura**    | Global       | Global       | Global       | Global       | **Global**        |

---

## ✅ Información Validada

### **Modelo de Pago**

- ✅ Soporta Solo Puntos y Copago (Slider Millas + Cash)
- ✅ Fee de procesamiento se aplica y se refleja en Admin
- ✅ Cálculo dinámico en tiempo real para copago
- ✅ Privacidad: Dirección IP oculta en resumen con "Solo Puntos" (desktop y mobile)

### **Emisión**

- ✅ Sistema procesa automáticamente la reserva al confirmar compra
- ✅ Genera código de confirmación/voucher único
- ✅ Débito de millas se efectúa al confirmar
- ✅ Voucher electrónico enviado por email
- ✅ Código QR incluido en voucher (si aplica)

### **Checkout**

- ✅ Campos completos de datos de contacto y participantes documentados
- ✅ Precarga automática de datos del usuario logueado (titular)
- ✅ Validaciones de documentos (DNI, CE, Pasaporte)
- ✅ Pasarelas de pago por país (Colombia, Perú, Ecuador, México, Chile)
- ✅ Solicitudes especiales disponibles (alergias, necesidades especiales)
- ✅ Servicios adicionales (Upsell): traslados, comidas, seguros, upgrades
- ✅ Flujo completo: Resumen → Datos → Pago → Confirmación

### **Políticas y Restricciones**

- ✅ Políticas de cancelación visibles y claras
- ✅ Política de no-show comunicada
- ✅ Restricciones de edad validadas según actividad
- ✅ Requisitos de condición física informados
- ✅ Reembolsos por cancelación del proveedor (mal clima, falta de quórum) documentados

### **Funcionalidades Adicionales**

- ✅ Búsquedas nacionales e internacionales
- ✅ Configuración flexible de participantes (Adultos, Niños con edad, Infantes con edad)
- ✅ Campos de edad autogenerados para menores
- ✅ Modificación de cantidad directa o con botones +/-
- ✅ Autocompletado de destino con sugerencias
- ✅ Múltiples categorías de actividades
- ✅ Validaciones en tiempo real en todos los formularios
- ✅ Voucher descargable en PDF
- ✅ Email de confirmación automático con voucher
- ✅ Canales de soporte (WhatsApp, teléfono, email) funcionales
- ✅ Información de qué llevar y recomendaciones en confirmación

---

## 📚 Referencias

- [CMP_QA_Assistant.agent.md](../../../agents/CMP_QA_Assistant.agent.md) - Agente especializado
- [CMP_COMMON_RULES.md](../../../../../documentation/knowledge-bases/shared/Reglas Marketplace/CMP_COMMON_RULES.md) - Reglas comunes
- [SHARED_QA_RULES.md](../../../../../documentation/knowledge-bases/shared/SHARED_QA_RULES.md) - Reglas universales

---

**Versión:** 1.1  
**Última actualización:** 2026-02-02  
**Estado:** ✅ Documentación Completa - Todos los módulos documentados y actualizados desde Knowledge Base CMP

**Historial de cambios:**

- **2026-02-02 (v1.1):** Actualización completa con información del Knowledge_Base_CMP.md
  - ✅ Módulo 2 (Disponibilidad): Agregada descripción detallada y precondiciones adicionales
  - ✅ Módulo 3 (Checkout): Agregada URL y Precondiciones
  - ✅ Módulo 4 (Confirmación): Agregada URL y Precondiciones
  - ✅ Todas las funcionalidades documentadas con componentes completos y comportamientos esperados
- **2026-01-26 (v1.0):** Documentación inicial completa de todos los módulos
