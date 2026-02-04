# 🏨 CMP - Flujo E2E de Hoteles

> **Club Miles Perú** - Documentación completa del flujo End-to-End de Hoteles

---

## 📌 Información General

| Campo           | Valor                                       |
| --------------- | ------------------------------------------- |
| **Marketplace** | Club Miles Perú (CMP)                       |
| **Producto**    | Hoteles 🏨                                  |
| **Tecnología**  | Angular                                     |
| **URL**         | https://demotravel-puntospe.smartlinks.dev/ |
| **Prefijo**     | `[CMP]`                                     |
| **Estado**      | ✅ Activo                                   |

---

## 🔌 Proveedor de Hoteles

| Proveedor     | Tipo             | Cobertura   | Estado    |
| ------------- | ---------------- | ----------- | --------- |
| **HOTELBEDS** | Agregador Global | 180+ países | ✅ Activo |

**Características:**

- Proveedor único: HOTELBEDS
- Cobertura global de hoteles
- Múltiples categorías (1-5 estrellas, hostales, resorts)
- Sistema de búsqueda y reserva directo

---

## 🏗️ Arquitectura

```
┌─────────────────────────────────────────────────────┐
│          FLUJO E2E HOTELES - CLUB MILES PERÚ        │
└─────────────────────────────────────────────────────┘

1️⃣ LOGIN (PPM)
   └─ https://clubmilesperu.preprodppm.com/
      ├─ Ingresar credenciales
      ├─ Validar OTP
      └─ Sesión establecida

2️⃣ HOME (PPM)
   └─ Dashboard Club Miles Perú
      ├─ Ver saldo de millas
      └─ Clic en "Hoteles" → Redirección cross-domain

3️⃣ MÓDULO HOTELES - HOME (Angular)
   └─ https://demotravel-puntospe.smartlinks.dev/hotels
      ├─ Verificar sesión activa
      ├─ Formulario de búsqueda
      └─ Enviar búsqueda

4️⃣ DISPONIBILIDAD (Angular)
   └─ Resultados de búsqueda
      ├─ Listar hoteles HOTELBEDS
      ├─ Filtros y ordenamiento
      └─ Seleccionar hotel y habitación

5️⃣ CHECKOUT (Angular)
   └─ Confirmar reserva
      ├─ Datos de huéspedes
      ├─ ⚠️ Modelo de pago (pendiente confirmar)
      └─ Confirmación

6️⃣ CONFIRMACIÓN (Angular)
   └─ Resumen de reserva
      ├─ Código de confirmación
      ├─ Débito de millas
      └─ Email confirmación
```

---

## 📋 MÓDULO 1: HOME DE HOTELES

### **Objetivo**

Capturar criterios de búsqueda de hoteles

### **URL**

```
https://demotravel-puntospe.smartlinks.dev/hotels
```

### **Precondiciones**

- ✅ Usuario autenticado en PPM
- ✅ Sesión activa transferida desde PPM
- ✅ VPN activa

### **Campos del Formulario de Búsqueda**

#### **1️⃣ Destino**

- **Tipo:** Autocomplete con búsqueda inteligente
- **Validación:** Ciudad, hotel específico, o región válida
- **Formato:** Nombre ciudad/hotel
- **Ejemplo:** Lima, Cusco, Miraflores
- **Búsqueda:** Permite búsqueda con nombre completo o tres primeras letras
- **Autocompletado:** Sugerencias dinámicas de ciudades y destinos turísticos

#### **2️⃣ Fecha de Check-in**

- **Tipo:** Date picker con calendario
- **Validación:** Fecha futura (hoy + 1 día mínimo típicamente)
- **Formato:** DD/MM/YYYY
- **Restricciones:** Sistema aplica restricciones de días mínimos/máximos adelante
- **No permite:** Seleccionar fechas pasadas

#### **3️⃣ Fecha de Check-out**

- **Tipo:** Date picker con calendario
- **Validación:** Posterior a check-in (mínimo 1 noche)
- **Formato:** DD/MM/YYYY
- **Restricciones:** Debe ser igual o posterior a fecha de check-in
- **Cálculo automático:** Sistema calcula número de noches

#### **4️⃣ Habitaciones**

- **Tipo:** Selector con sub-configuración
- **Cantidad:** 1-9 habitaciones (permite 1 habitación o múltiples habitaciones)
- **Por cada habitación:**
  - **Adultos (ADT):** 1-8 adultos
    - Contador con botones +/- o flechas
    - Opción de escribir cantidad directamente
    - Validación de límites máximos/mínimos
  - **Niños (CHL):** 0-4 niños
    - Contador con botones +/- o flechas
    - Opción de escribir cantidad directamente
    - **Campo de edad obligatorio por cada niño**
    - Sistema genera automáticamente campo de edad al agregar niños
  - **Infantes (INF):** 0-2 infantes
    - Contador con botones +/- o flechas
    - Opción de escribir cantidad directamente
    - **Campo de edad obligatorio por cada infante**
    - Sistema genera automáticamente campo de edad al agregar infantes

**Ejemplo de configuración:**

```
Habitación 1:
  - 2 Adultos
  - 1 Niño (edad: 5 años) ← Campo generado automáticamente
  - 1 Infante (edad: 1 año) ← Campo generado automáticamente

Habitación 2:
  - 2 Adultos
  - 2 Niños (edad: 8 años, edad: 10 años) ← Campos generados automáticamente
```

**Escenarios de búsqueda soportados:**

- Múltiples adultos + 1 habitación
- ADT + CHL + INF + 1 habitación
- Múltiples adultos + múltiples habitaciones
- ADT + CHL + INF + múltiples habitaciones
- Cada habitación puede tener configuración diferente de pasajeros

#### **5️⃣ Nacionalidad** (opcional)

- **Tipo:** Dropdown con lista de países
- **Validación:** País válido
- **Uso:** Puede afectar tarifas y disponibilidad según destino

### **Validaciones Críticas**

| Validación                       | Comportamiento Esperado                                                     |
| -------------------------------- | --------------------------------------------------------------------------- |
| **Check-out <= Check-in**        | Mensaje de error, ajustar automáticamente                                   |
| **Fecha pasada**                 | Mensaje de error, bloquear búsqueda                                         |
| **Sin habitaciones**             | Mensaje de error, requerir al menos 1 habitación                            |
| **Sin adultos**                  | Mensaje de error, requerir al menos 1 adulto por habitación                 |
| **Edad de niño sin especificar** | Requerir edad si se seleccionan niños - Campo de edad obligatorio y visible |
| **Edad de INF sin especificar**  | Requerir edad si se seleccionan infantes - Campo de edad obligatorio        |
| **Destino vacío**                | Mensaje de error, resaltar campo                                            |
| **Campos obligatorios vacíos**   | Resaltar visualmente y mostrar mensaje de error específico                  |

### **Acciones Disponibles**

- **Buscar:** Envía búsqueda a módulo de disponibilidad
- **Limpiar:** Resetea formulario a valores por defecto
- **Volver:** Regresa a dashboard PPM

---

## 📋 MÓDULO 2: DISPONIBILIDAD DE HOTELES

### **Objetivo**

Mostrar hoteles disponibles del proveedor HOTELBEDS

### **Descripción**

Módulo que muestra los resultados de búsqueda de alojamiento disponible desde HOTELBEDS con información detallada de hoteles, filtros de refinamiento y opciones de selección de habitaciones.

### **URL**

```
https://demotravel-puntospe.smartlinks.dev/hotels/results
```

### **Precondiciones**

- ✅ Búsqueda enviada desde Home
- ✅ Criterios de búsqueda válidos
- ✅ Usuario autenticado
- ✅ Sesión activa

### **Estructura de Resultados**

#### **Sección Superior: Resumen de Búsqueda**

- Destino
- Fechas de check-in y check-out
- Noches totales
- Habitaciones y huéspedes
- **Botón "Modificar búsqueda"** → Regresa a Home con criterios precargados

#### **Sección Principal: Listado de Hoteles**

**Información por Hotel:**

| Campo                    | Descripción                                   |
| ------------------------ | --------------------------------------------- |
| **Nombre del Hotel**     | Nombre oficial                                |
| **Categoría**            | Estrellas (1-5) o tipo (Hostal, Resort, etc.) |
| **Ubicación**            | Zona/barrio de la ciudad                      |
| **Distancia**            | Km del centro o punto de referencia           |
| **Calificación**         | Rating de huéspedes (si disponible)           |
| **Foto Principal**       | Imagen destacada del hotel                    |
| **Precio en Millas**     | ⚠️ Modelo pendiente confirmar                 |
| **Copago**               | ⚠️ Si aplica Slider                           |
| **Cancelación**          | Política (Gratuita hasta X / No reembolsable) |
| **Servicios Destacados** | WiFi, Desayuno, Piscina, etc.                 |

#### **Filtros Disponibles**

| Filtro                      | Opciones                                      |
| --------------------------- | --------------------------------------------- |
| **Precio**                  | Rango de millas                               |
| **Categoría**               | 1-5 estrellas, sin categoría                  |
| **Calificación**            | Rango de rating de huéspedes                  |
| **Tipo de alojamiento**     | Hotel, Hostal, Resort, Apartamento            |
| **Servicios**               | WiFi, Desayuno, Piscina, Estacionamiento, Gym |
| **Política de cancelación** | Gratuita, Parcial, No reembolsable            |
| **Zona/Ubicación**          | Barrios o áreas de la ciudad                  |

#### **Ordenamiento**

- Precio menor a mayor
- Calificación mayor a menor
- Distancia al centro
- Categoría (estrellas)
- Nombre alfabéticamente

### **Escenarios Posibles**

#### **✅ Resultados Encontrados**

- Mostrar hoteles disponibles de HOTELBEDS
- Permitir selección de hotel y habitación

#### **⚠️ Sin Resultados**

- Mensaje claro: "No se encontraron hoteles para tu búsqueda"
- Sugerencias: Modificar fechas, destino, criterios
- Botón "Nueva búsqueda"

#### **❌ Error de Proveedor**

- Mensaje genérico de error
- Opción de reintentar
- No exponer detalles técnicos

### **Selección de Hotel**

#### **Paso 1: Ver Detalles del Hotel**

Al hacer clic en un hotel, mostrar:

- Galería de fotos
- Descripción completa
- Ubicación en mapa
- Servicios completos
- Políticas del hotel
- Calificaciones y reseñas

#### **Paso 2: Seleccionar Habitación**

Mostrar habitaciones disponibles:

| Campo                   | Descripción                                              |
| ----------------------- | -------------------------------------------------------- |
| **Tipo de habitación**  | Simple, Doble, Suite, etc.                               |
| **Capacidad**           | Adultos + niños permitidos                               |
| **Régimen alimenticio** | Solo alojamiento, Desayuno, Media pensión, Todo incluido |
| **Precio en Millas**    | Por noche o total                                        |
| **Copago**              | Si aplica                                                |
| **Cancelación**         | Política específica                                      |
| **Disponibilidad**      | Cuántas habitaciones quedan                              |

#### **Paso 3: Confirmar Selección**

1. Usuario selecciona habitación(es) deseada(s)
2. Sistema valida disponibilidad
3. Resumen de selección se muestra
4. Botón "Continuar a checkout" se activa

---

## 📋 MÓDULO 3: CHECKOUT

### **Objetivo**

Capturar datos de huéspedes, información de contacto y procesar el pago para confirmar la reserva de hotel.

### **Descripción**

Módulo de finalización de compra para hoteles donde se capturan los datos de huéspedes, información de contacto, se procesan métodos de pago y se genera la confirmación de reserva. Incluye validaciones específicas de alojamiento, políticas de cancelación y métodos de pago.

### **URL**

```
https://demotravel-puntospe.smartlinks.dev/hotels/checkout
```

### **Precondiciones**

- ✅ Hotel y habitación seleccionados desde módulo de Disponibilidad
- ✅ Usuario autenticado
- ✅ Sesión activa

---

### **🔹 Resumen de Reserva**

**Descripción:** Pantalla que consolida la información del hotel seleccionado antes de proceder al checkout, permitiendo revisar y editar la búsqueda.

**Componentes:**

- **Información del hotel:**
  - Nombre completo del hotel
  - Categoría (estrellas: 1-5)
  - Dirección completa
  - Ubicación (zona/barrio)
  - Foto principal del hotel
  - Servicios destacados (WiFi, Piscina, Desayuno, etc.)

- **Fechas de estadía:**
  - Fecha de check-in (formato: Día, DD de Mes de AAAA)
  - Fecha de check-out (formato: Día, DD de Mes de AAAA)
  - Número total de noches

- **Detalles de habitaciones:**
  - Tipo de habitación seleccionada (Simple, Doble, Suite, etc.)
  - Número de habitaciones
  - Cantidad de huéspedes por habitación (adultos + niños + infantes)
  - Régimen alimenticio (Solo alojamiento, Desayuno, Media pensión, Todo incluido)

- **Desglose de precios:**
  - Precio por noche
  - Total de noches
  - Subtotal
  - Impuestos (si aplican)
  - Fee de servicio
  - **Total en millas**

- **Políticas:**
  - Políticas de cancelación del hotel seleccionado
  - Hora de check-in y check-out
  - Restricciones o condiciones especiales

- **Botones de acción:**
  - **"Editar búsqueda":** Vuelve a disponibilidad para modificar parámetros
  - **"Continuar":** Avanza al formulario de huéspedes

**Comportamiento esperado:**

1. Muestra toda la información de la selección de manera clara y estructurada
2. Permite editar búsqueda y volver a disponibilidad sin perder contexto
3. Calcula correctamente el total basado en noches y tarifas
4. Número de noches se calcula automáticamente entre check-in y check-out
5. Valida disponibilidad antes de permitir continuar
6. Muestra políticas de cancelación claras y visibles
7. Impuestos se desglosan separadamente si no están incluidos
8. Información es consistente con la selección de disponibilidad

---

### **🔹 Datos de Contacto**

**Descripción:** Sección del checkout que captura la información de contacto del responsable de la reserva para notificaciones y confirmaciones.

**Componentes:**

- **Email\*** (campo de texto con validación)
- **Teléfono\*** (campo numérico con código de país)
- Indicadores de campo obligatorio (\*)
- Validaciones en tiempo real
- Mensajes de error específicos

**Comportamiento esperado:**

1. Ambos campos son obligatorios
2. Email debe tener formato válido (incluir @ y dominio válido: .com, .co, .net, etc.)
3. Teléfono debe contener solo números con longitud válida
4. Código de país se selecciona correctamente desde dropdown
5. Validaciones funcionan en tiempo real al escribir
6. No permite continuar sin datos completos y válidos
7. Información se usa para envío de confirmaciones y comunicación con el hotel
8. Muestra mensajes de error específicos por campo

---

### **🔹 Formulario de Huéspedes**

**Descripción:** Formulario obligatorio en el checkout donde se capturan los datos personales de todos los huéspedes para la reserva de hotel.

**Componentes:**

**Sección por cada huésped:**

- Encabezado: "Huésped 1 (Principal)", "Huésped 2", etc.

**Campos del huésped principal:**

- **Nombre\*** (campo de texto)
- **Apellido\*** (campo de texto)
- **Tipo de documento\*** (dropdown: DNI, CE, Pasaporte)
- **Número de documento\*** (campo alfanumérico)
- **Email\*** (campo de texto con validación)
- **Teléfono de contacto\*** (campo numérico con código de país)

**Campos de huéspedes adicionales:**

- **Nombre\*** (campo de texto)
- **Apellido\*** (campo de texto)
- **Tipo de documento\*** (dropdown: DNI, CE, Pasaporte)
- **Número de documento\*** (campo alfanumérico)

**Funcionalidades:**

- Precarga automática de datos del usuario logueado en huésped principal (titular)
- Sistema genera formularios según cantidad de huéspedes en búsqueda original
- Indicadores de campo obligatorio (\*)
- Validaciones en tiempo real
- Mensajes de error específicos por campo
- Usuario puede editar datos precargados

**Comportamiento esperado:**

1. Sistema genera formulario por cada huésped según búsqueda original
2. Datos del usuario logueado se precargan automáticamente en huésped principal
3. Validación de formato de email con @ y dominio válido
4. Solo permite letras y espacios en nombre/apellido (permite tildes y ñ)
5. Teléfono solo acepta números con código de país
6. No permite continuar sin completar campos obligatorios
7. Muestra mensajes de error claros y específicos por campo
8. Usuario puede editar datos precargados si es necesario
9. Validaciones funcionan en tiempo real
10. Formato de documento valida según tipo seleccionado

---

### **🔹 Solicitudes Especiales** (opcional)

**Descripción:** Sección opcional que permite al usuario agregar solicitudes o preferencias especiales para la reserva.

**Componentes:**

- **Hora estimada de llegada** (selector de hora)
- **Cama extra** (checkbox)
- **Preferencias de habitación** (campo de texto libre)
- **Comentarios adicionales** (campo de texto libre, área de texto)
- Indicación: "Estas solicitudes están sujetas a disponibilidad del hotel"

**Comportamiento esperado:**

1. Todos los campos son opcionales
2. Permite escribir solicitudes en texto libre
3. Hora de llegada ayuda al hotel a preparar la habitación
4. Sistema envía solicitudes al hotel con la confirmación
5. Muestra mensaje claro indicando que solicitudes están sujetas a disponibilidad
6. No bloquea el proceso de compra si no se completan
7. Información se incluye en correo de confirmación

---

### **🔹 Métodos de Pago**

**Descripción:** Sección del checkout que permite seleccionar la forma de pago para la reserva de hotel, incluyendo Solo Puntos, copago (Puntos + Cash), PSE y métodos de pago con tarjetas por país.

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

**Comportamiento esperado:**

1. **Selección de "Solo Puntos":**
   - Sistema bloquea cantidad exacta de puntos de la cuenta del usuario
   - No solicita información de tarjeta de crédito
   - Fee de procesamiento se aplica correctamente
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

**Descripción:** Conjunto de validaciones complementarias que garantizan la seguridad, integridad y optimización del proceso de checkout de hoteles.

**Componentes:**

- Encriptación de datos sensibles (tarjetas)
- Manejo de errores del servicio de pagos
- Checkbox "Requiero Factura" con campos de empresa y NIT/RFC/RUC
- Checkbox de términos y condiciones con link a políticas completas
- Validación de llamados de servicio (evitar duplicados)
- Políticas de cancelación del hotel visibles
- Políticas de no-show (no presentarse)
- Información sobre garantía de pago si es requerida
- Impuestos locales incluidos/excluidos claramente indicados

**Comportamiento esperado:**

1. Datos de tarjeta se envían encriptados (validable en Network → Request Payload)
2. Errores de pago muestran mensajes claros al usuario con opción de reintentar
3. Puntos no quedan bloqueados si la transacción falla
4. Campo de factura aparece solo si se activa el checkbox
5. Campos de empresa y NIT/RFC/RUC validan formato correcto
6. No permite continuar sin aceptar términos y condiciones
7. Link a términos completos funciona y muestra políticas del hotel
8. Servicio Create se invoca una única vez al cargar checkout (validar en Network)
9. Performance optimizada eliminando llamados duplicados
10. Políticas de cancelación son claras y visibles antes de confirmar
11. Política de no-show es comunicada al usuario
12. Si requiere garantía de pago, es informado claramente
13. Impuestos locales se muestran desglosados si no están incluidos

---

## 📋 MÓDULO 4: CONFIRMACIÓN

### **Objetivo**

Mostrar resumen completo de la reserva de hotel confirmada exitosamente después de procesar el pago.

### **Descripción**

Pantalla final que muestra la confirmación de la reserva de hotel con todos los detalles, envío de correo de confirmación y canales de soporte.

### **URL**

```
https://demotravel-puntospe.smartlinks.dev/hotels/confirmation
```

### **Precondiciones**

- ✅ Pago procesado exitosamente
- ✅ Reserva confirmada
- ✅ Puntos debitados

---

### **🔹 Código de Reserva / Voucher**

**Descripción:** Código único de la reserva que identifica la transacción.

**Componentes:**

- Código de reserva/voucher visible y destacado
- Formato alfanumérico único
- Texto explicativo: "Tu código de reserva es:" o "Número de confirmación:"
- Opción de copiar código fácilmente

**Comportamiento esperado:**

1. Código se muestra inmediatamente después de pago exitoso
2. Código es único para cada reserva
3. Formato es claro y legible
4. Usuario puede copiar código fácilmente
5. Código aparece en el correo de confirmación
6. Sistema registra código en Admin para seguimiento

---

### **🔹 Información del Hotel Confirmado**

**Descripción:** Sección que muestra el resumen del hotel reservado.

**Componentes:**

- Nombre completo del hotel
- Categoría (estrellas: 1-5)
- Dirección completa del hotel
- Ubicación (zona/barrio de la ciudad)
- Teléfono de contacto del hotel
- Foto principal del hotel
- Servicios incluidos (WiFi, Piscina, Desayuno, etc.)

**Comportamiento esperado:**

1. Información coincide exactamente con el hotel seleccionado
2. Dirección es completa y útil para localización
3. Teléfono de contacto del hotel es funcional
4. Imagen del hotel se muestra correctamente
5. Servicios listados son los incluidos en la reserva
6. Datos son consistentes con disponibilidad y checkout

---

### **🔹 Fechas y Detalles de Estadía**

**Descripción:** Sección que muestra las fechas y detalles de la estadía.

**Componentes:**

**Check-in:**

- Fecha de check-in (formato: Día de la semana, DD de Mes de AAAA)
- Hora de check-in (formato: HH:MM o "A partir de las HH:MM")

**Check-out:**

- Fecha de check-out (formato: Día de la semana, DD de Mes de AAAA)
- Hora de check-out (formato: HH:MM o "Hasta las HH:MM")

**Detalles de la reserva:**

- Número total de noches
- Tipo de habitación reservada (Simple, Doble, Suite, etc.)
- Número de habitaciones
- Régimen alimenticio (Solo alojamiento, Desayuno, Media pensión, Todo incluido)
- Cantidad de huéspedes (adultos, niños, infantes)

**Comportamiento esperado:**

1. Fechas se muestran en formato largo en español
2. Horarios de check-in y check-out son claros
3. Número de noches calculado correctamente
4. Tipo de habitación coincide con la selección original
5. Régimen alimenticio es visible y claro
6. Cantidad de huéspedes coincide con la búsqueda original

---

### **🔹 Datos de Huéspedes**

**Descripción:** Sección que muestra la información de los huéspedes registrados en la reserva.

**Componentes:**

**Huésped Principal:**

- Nombre completo
- Tipo y número de documento
- Email de contacto
- Teléfono de contacto

**Huéspedes Adicionales:**

- Nombre completo de cada huésped
- Tipo y número de documento

**Solicitudes Especiales** (si aplica):

- Hora estimada de llegada
- Solicitudes o comentarios adicionales

**Comportamiento esperado:**

1. Todos los datos coinciden con los ingresados en el checkout
2. Información es legible y correctamente organizada
3. Datos sensibles pueden estar parcialmente enmascarados si aplica
4. Lista todos los huéspedes de la reserva
5. Solicitudes especiales son visibles si fueron ingresadas

---

### **🔹 Desglose de Pago**

**Descripción:** Sección que muestra el desglose completo del pago realizado.

**Componentes:**

- Precio base de la habitación
- Precio por noche
- Número de noches
- Subtotal
- Impuestos (si aplican)
- Fee de servicio
- **Total pagado en millas**
- Método de pago usado (Solo Puntos / Copago)
- Puntos debitados de la cuenta

**Comportamiento esperado:**

1. Cantidades muestran separador de miles (punto)
2. Total de Millas debitadas refleja el débito de la cuenta del usuario
3. Valores son consistentes con el precio mostrado en disponibilidad y checkout
4. Impuestos se muestran desglosados si no estaban incluidos
5. Desglose es claro y fácil de entender
6. Método de pago utilizado es visible
7. Cálculo de precio por noche × número de noches es correcto

---

### **🔹 Políticas y Condiciones**

**Descripción:** Sección con información importante sobre políticas del hotel.

**Componentes:**

**Políticas de cancelación:**

- Descripción de política aplicable (Gratuita hasta X / Parcial / No reembolsable)
- Fechas límite para cancelación sin cargo
- Cargos por cancelación si aplican

**Políticas del hotel:**

- Política de no-show (no presentarse)
- Modificaciones de reserva permitidas
- Garantía de pago requerida (si aplica)
- Check-in temprano / Check-out tardío (disponibilidad y costos)

**Instrucciones importantes:**

- Documentos requeridos al hacer check-in
- Restricciones de edad si aplican
- Políticas de mascotas (si aplican)
- Formas de pago aceptadas en el hotel

**Comportamiento esperado:**

1. Políticas son claras y comprensibles
2. Fechas límite de cancelación son específicas
3. Condiciones importantes están destacadas
4. Información ayuda al huésped a prepararse para el check-in
5. Políticas coinciden con las mostradas en disponibilidad y checkout

---

### **🔹 Confirmación por Correo y Canales de Soporte**

**Descripción:** Sección que notifica sobre el envío del correo de confirmación y proporciona canales de comunicación.

**Componentes:**

**Banner de correo:**

- Ícono de sobre/correo
- Mensaje principal: "La confirmación de tu reserva ha sido enviada a [email] y al hotel."
- Mensaje secundario: "En caso de no recibirla, revise la bandeja de Correo no deseado."

**Canales de soporte:**

- WhatsApp con número de contacto
- Teléfono de atención al cliente
- Email de contacto
- Horarios de atención

**Botones de acción:**

- **"Ver Resumen":** Muestra detalle completo de la reserva
- **"Descargar Voucher":** Genera PDF con todos los detalles
- **"Imprimir":** Abre diálogo de impresión
- **"Regresar al Home":** Vuelve al widget de búsqueda

**Comportamiento esperado:**

1. Correo de confirmación se envía automáticamente
2. Correo se envía tanto al usuario como al hotel
3. Correo incluye todos los detalles: código de reserva, hotel, fechas, habitación, huéspedes
4. Formato del correo es correcto y profesional
5. Banner de notificación es visible y claro
6. Canales de soporte (WhatsApp, teléfono) son funcionales y visibles
7. Números de contacto y horarios son correctos
8. Botón "Ver Resumen" muestra información consistente
9. Botón "Descargar Voucher" genera PDF correctamente
10. PDF incluye: código de reserva, hotel, fechas, habitación, huéspedes, políticas
11. Botón "Imprimir" abre diálogo de impresión del navegador
12. Botón "Regresar al Home" limpia el flujo y vuelve al inicio
13. Eventos de conversión (Meta Ads Pixel, Google Ads) se disparan correctamente
14. Voucher es presentable y contiene toda la información necesaria para el hotel

---

## 🧪 Casos de Prueba Recomendados

### **Prioridad 1 (Crítica)**

| ID          | Título                                                        | Escenario                   |
| ----------- | ------------------------------------------------------------- | --------------------------- |
| CMP-HOT-001 | [CMP] Hoteles - 3 noches - HotelBeds - 1 habitación 2 adultos | Flujo completo exitoso      |
| CMP-HOT-002 | [CMP] Hoteles - 5 noches - HotelBeds - Cancelación gratuita   | Flujo completo exitoso      |
| CMP-HOT-003 | [CMP] Hoteles - Sesión cross-domain - Validar persistencia    | Navegación PPM → Angular    |
| CMP-HOT-004 | [CMP] Hoteles - Sin resultados - Mensaje error                | Búsqueda sin disponibilidad |
| CMP-HOT-005 | [CMP] Hoteles - Check-out <= Check-in - Validación            | Error de validación         |

### **Prioridad 2 (Alta)**

| ID          | Título                                                            | Escenario           |
| ----------- | ----------------------------------------------------------------- | ------------------- |
| CMP-HOT-006 | [CMP] Hoteles - 2 habitaciones - 2 adultos + 1 niño c/u           | Flujo completo      |
| CMP-HOT-007 | [CMP] Hoteles - Filtros múltiples - 4 estrellas + WiFi + Desayuno | Validar filtrado    |
| CMP-HOT-008 | [CMP] Hoteles - Modificar búsqueda - Precarga criterios           | Edición de búsqueda |
| CMP-HOT-009 | [CMP] Hoteles - Ver detalles - Galería y mapa                     | Validar información |
| CMP-HOT-010 | [CMP] Hoteles - Seleccionar Suite - Todo incluido                 | Flujo completo      |

### **Prioridad 3 (Media)**

| ID          | Título                                   | Escenario                   |
| ----------- | ---------------------------------------- | --------------------------- |
| CMP-HOT-011 | [CMP] Hoteles - Ordenar por calificación | Validar ordenamiento        |
| CMP-HOT-012 | [CMP] Hoteles - Filtrar por zona         | Validar filtrado geográfico |
| CMP-HOT-013 | [CMP] Hoteles - Volver a Home PPM        | Navegación inversa          |
| CMP-HOT-014 | [CMP] Hoteles - Timeout de búsqueda      | Manejo de error             |
| CMP-HOT-015 | [CMP] Hoteles - Error de proveedor       | Manejo de error             |

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

### **Emisión**

- ✅ Sistema procesa automáticamente la reserva al confirmar compra
- ✅ Genera código de confirmación/voucher único
- ✅ Débito de millas se efectúa al confirmar
- ✅ Envío automático de confirmación al usuario y hotel

### **Checkout**

- ✅ Campos completos de datos de contacto y huéspedes documentados
- ✅ Precarga automática de datos del usuario logueado (titular)
- ✅ Validaciones de documentos (DNI, CE, Pasaporte)
- ✅ Pasarelas de pago por país (Colombia, Perú, Ecuador, México, Chile)
- ✅ Solicitudes especiales disponibles (opcional)
- ✅ Flujo completo: Resumen → Datos → Pago → Confirmación

### **Políticas**

- ✅ Políticas de cancelación visibles y claras
- ✅ Política de no-show comunicada
- ✅ Modificaciones de reserva según política del hotel
- ✅ Garantía de pago informada si es requerida
- ✅ Impuestos locales desglosados si no están incluidos

### **Funcionalidades Adicionales**

- ✅ Configuración flexible de habitaciones (1 o múltiples)
- ✅ Configuración flexible de pasajeros (ADT, CHL con edad, INF con edad)
- ✅ Campos de edad autogenerados para niños e infantes
- ✅ Modificación de cantidad directa o con botones +/-
- ✅ Autocompletado de destino con sugerencias
- ✅ Validaciones en tiempo real en todos los formularios
- ✅ Voucher descargable en PDF
- ✅ Email de confirmación automático con voucher
- ✅ Canales de soporte (WhatsApp, teléfono, email) funcionales

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
