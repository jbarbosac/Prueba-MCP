# 🚗 CMP - Flujo E2E de Autos

> **Club Miles Perú** - Documentación completa del flujo End-to-End de Renta de Autos

---

## 📌 Información General

| Campo           | Valor                                 |
| --------------- | ------------------------------------- |
| **Marketplace** | Club Miles Perú (CMP)                 |
| **Producto**    | Autos 🚗                              |
| **Tecnología**  | Meteor                                |
| **URL**         | https://demo-puntospe.smartlinks.dev/ |
| **Prefijo**     | `[CMP]`                               |
| **Estado**      | ✅ Activo                             |

---

## 🔌 Proveedor de Autos

| Proveedor | Tipo    | Marcas Disponibles     | Estado    |
| --------- | ------- | ---------------------- | --------- |
| **SABRE** | Directo | Hertz, Dollar, Thrifty | ✅ Activo |

**Características:**

- Proveedor único: SABRE
- Múltiples marcas de renta de autos
- Cobertura internacional
- Sistema de búsqueda y reserva directo

---

## 🏗️ Arquitectura

```
┌─────────────────────────────────────────────────────┐
│           FLUJO E2E AUTOS - CLUB MILES PERÚ         │
└─────────────────────────────────────────────────────┘

1️⃣ LOGIN (PPM)
   └─ https://clubmilesperu.preprodppm.com/
      ├─ Ingresar credenciales
      ├─ Validar OTP
      └─ Sesión establecida

2️⃣ HOME (PPM)
   └─ Dashboard Club Miles Perú
      ├─ Ver saldo de millas
      └─ Clic en "Autos" → Redirección cross-domain

3️⃣ MÓDULO AUTOS - HOME (Meteor)
   └─ https://demo-puntospe.smartlinks.dev/cars
      ├─ Verificar sesión activa
      ├─ Formulario de búsqueda
      └─ Enviar búsqueda

4️⃣ DISPONIBILIDAD (Meteor)
   └─ Resultados de búsqueda
      ├─ Listar autos SABRE disponibles
      ├─ Filtros por marca, tipo, precio
      └─ Seleccionar auto

5️⃣ CHECKOUT (Meteor)
   └─ Confirmar reserva
      ├─ Datos del conductor
      ├─ ⚠️ Modelo de pago (pendiente confirmar)
      └─ Confirmación

6️⃣ CONFIRMACIÓN (Meteor)
   └─ Resumen de reserva
      ├─ Código de confirmación
      ├─ Débito de millas
      └─ Email confirmación
```

---

## 📋 MÓDULO 1: HOME DE AUTOS

### **Objetivo**

Capturar criterios de búsqueda de renta de autos

### **URL**

```
https://demo-puntospe.smartlinks.dev/cars
```

### **Precondiciones**

- ✅ Usuario autenticado en PPM
- ✅ Sesión activa transferida desde PPM
- ✅ VPN activa

### **Campos del Formulario de Búsqueda**

#### **1️⃣ Lugar de Recogida (Pickup)**

- **Tipo:** Autocomplete / Selección desde lista desplegable
- **Validación:** Ciudad o aeropuerto válido
- **Formato:** Nombre ciudad (Código)
- **Ejemplo:** Lima (LIM), Cusco (CUZ)
- **Búsqueda:** Permite búsqueda con nombre completo o tres primeras letras
- **Autocompletado:** Sugerencias dinámicas según entrada del usuario
- **Diferenciación:** Indica si es aeropuerto u oficina (tarifas pueden variar)

#### **2️⃣ Checkbox "Devolver en otro lugar" (DropOff)**

- **Tipo:** Checkbox clickeable
- **Función:** Al activarse, habilita campo adicional de ciudad de devolución
- **Comportamiento:**
  - Desmarcado por defecto: devolución en mismo lugar de recogida
  - Marcado: permite seleccionar ubicación diferente para devolución
  - Al desactivarse, oculta campo de ciudad de devolución
- **Advertencia:** Muestra indicador de cargo adicional si aplica DropOff

#### **3️⃣ Lugar de Devolución (Dropoff)**

- **Tipo:** Autocomplete (solo visible si checkbox está activado)
- **Validación:** Ciudad o aeropuerto válido, puede ser diferente al origen
- **Formato:** Nombre ciudad (Código)
- **Cargo adicional:** Sistema calcula y muestra cargo extra por DropOff si aplica

#### **4️⃣ Fecha y Hora de Recogida**

- **Fecha:** Date picker con calendario
- **Hora:** Time picker / Selector de hora específica
- **Validación:** Fecha y hora futura (mínimo 3 horas desde ahora según restricciones configuradas)
- **Formato:** DD/MM/YYYY HH:MM
- **Restricciones:** Sistema aplica restricciones de días mínimos/máximos adelante

#### **5️⃣ Fecha y Hora de Devolución**

- **Fecha:** Date picker con calendario
- **Hora:** Time picker / Selector de hora específica
- **Validación:**
  - Debe ser igual o posterior a fecha/hora de recogida
  - Permite búsqueda con 1 día de intervalo mínimo
  - Permite búsqueda con más de 1 día de intervalo
- **Formato:** DD/MM/YYYY HH:MM

#### **6️⃣ Campo CDP (Código de Descuento)**

- **Tipo:** Campo de texto
- **Valor:** Código de descuento aplicado por defecto
- **Función:** Descuento exclusivo preconfigurado
- **Editable:** Usuario puede modificar o eliminar el código
- **Validación:** Sistema valida código CDP si es modificado

### **Validaciones Críticas**

| Validación                | Comportamiento Esperado                           |
| ------------------------- | ------------------------------------------------- |
| **Fecha/hora pasada**     | Mensaje de error, bloquear búsqueda               |
| **Devolución < Recogida** | Mensaje de error, ajustar automáticamente         |
| **Edad insuficiente**     | Mensaje de error o advertencia de costo adicional |
| **Campos vacíos**         | Mensaje de error, resaltar campos requeridos      |
| **Dropoff diferente**     | Advertencia de posible cargo adicional            |

### **Acciones Disponibles**

- **Buscar:** Envía búsqueda a módulo de disponibilidad
- **Limpiar:** Resetea formulario a valores por defecto
- **Volver:** Regresa a dashboard PPM

---

## 📋 MÓDULO 2: DISPONIBILIDAD DE AUTOS

### **Objetivo**

Mostrar autos disponibles del proveedor SABRE

### **Descripción**

Módulo que muestra los resultados de búsqueda de vehículos disponibles desde SABRE (Hertz, Dollar, Thrifty) con información detallada, filtros de refinamiento y opciones de selección.

### **URL**

```
https://demo-puntospe.smartlinks.dev/cars/results
```

### **Precondiciones**

- ✅ Búsqueda enviada desde Home
- ✅ Criterios de búsqueda válidos
- ✅ Usuario autenticado
- ✅ Sesión activa

### **Estructura de Resultados**

#### **Sección Superior: Resumen de Búsqueda**

- Lugar de recogida y devolución
- Fechas y horas seleccionadas
- Duración total (días)
- **Botón "Modificar búsqueda"** → Regresa a Home con criterios precargados

#### **Sección Principal: Listado de Autos**

**Información por Auto:**

| Campo                       | Descripción                          |
| --------------------------- | ------------------------------------ |
| **Marca**                   | Hertz / Dollar / Thrifty             |
| **Modelo**                  | Nombre del vehículo o similar        |
| **Tipo**                    | Económico, Compacto, SUV, Lujo, etc. |
| **Pasajeros**               | Capacidad de personas                |
| **Equipaje**                | Maletas grandes + pequeñas           |
| **Transmisión**             | Manual / Automática                  |
| **Aire Acondicionado**      | Sí / No                              |
| **Precio en Millas**        | ⚠️ Modelo pendiente confirmar        |
| **Copago**                  | ⚠️ Si aplica Slider                  |
| **Política de combustible** | Lleno/Lleno típicamente              |

#### **Filtros Disponibles**

| Filtro               | Opciones                                     |
| -------------------- | -------------------------------------------- |
| **Marca**            | Hertz, Dollar, Thrifty                       |
| **Tipo de vehículo** | Económico, Compacto, Mediano, SUV, Lujo, Van |
| **Transmisión**      | Manual, Automática                           |
| **Pasajeros**        | 2, 4, 5, 7+                                  |
| **Precio**           | Rango de millas                              |
| **Equipaje**         | Mínimo de maletas                            |

#### **Ordenamiento**

- Precio menor a mayor
- Marca alfabéticamente
- Capacidad de pasajeros
- Tipo de vehículo

### **Escenarios Posibles**

#### **✅ Resultados Encontrados**

- Mostrar autos disponibles de SABRE (Hertz, Dollar, Thrifty)
- Permitir selección y continuar a checkout

#### **⚠️ Sin Resultados**

- Mensaje claro: "No se encontraron autos para tu búsqueda"
- Sugerencias: Modificar fechas, lugar, criterios
- Botón "Nueva búsqueda"

#### **❌ Error de Proveedor**

- Mensaje genérico de error
- Opción de reintentar
- No exponer detalles técnicos

### **Selección de Auto**

1. Usuario revisa opciones disponibles
2. Usuario selecciona auto deseado
3. Sistema muestra resumen de selección
4. Botón "Continuar a checkout" se activa

### **Información Adicional por Auto**

**Al hacer clic en "Ver detalles":**

- Foto del vehículo (o similar)
- Especificaciones completas
- Política de combustible
- Seguro incluido (si aplica)
- Restricciones de edad
- Cargos adicionales (dropoff diferente, conductor adicional, etc.)
- Términos y condiciones

---

## 📋 MÓDULO 3: CHECKOUT

### **Objetivo**

Capturar datos del conductor, información de contacto, servicios adicionales y procesar el pago para confirmar la reserva de auto.

### **Descripción**

Módulo de finalización de compra para renta de vehículos donde se capturan los datos del conductor principal, información de contacto, se procesan métodos de pago y se genera la confirmación de reserva. Incluye validaciones específicas de licencia de conducir, edad mínima y métodos de pago.

### **URL**

```
https://demo-puntospe.smartlinks.dev/cars/checkout
```

### **Precondiciones**

- ✅ Vehículo seleccionado desde módulo de Disponibilidad
- ✅ Usuario autenticado
- ✅ Sesión activa

---

### **🔹 Resumen de Reserva**

**Descripción:** Pantalla inicial del checkout que consolida la información del vehículo seleccionado antes de capturar datos del conductor, permitiendo verificar detalles, fechas y aplicación de puntos.

**Componentes:**

- **Información del vehículo:**
  - Nombre completo (marca/modelo o similar)
  - Categoría del vehículo
  - Imagen del vehículo
  - Capacidad de pasajeros
  - Número de maletas
  - Tipo de transmisión (Manual/Automática)

- **Ubicaciones y fechas:**
  - Ubicación de recogida (con indicación de aeropuerto u oficina)
  - Ubicación de devolución (con indicación de DropOff si aplica)
  - Fecha y hora de recogida
  - Fecha y hora de devolución
  - Duración total del alquiler (días)

- **Desglose de precios:**
  - Precio base del vehículo
  - Cargo DropOff (si aplica, cuando devolución es en lugar diferente)
  - Fee de servicio
  - Total en millas

- **Desglose de puntos:**
  - Puntos requeridos para la reserva
  - Saldo disponible en cuenta
  - Valor de canje

- **Distribución para copago (si aplica):**
  - Slider de puntos vs cash
  - Cálculo dinámico de monto

- **Políticas:**
  - Políticas de cancelación
  - Restricciones de edad
  - Política de combustible

- **Botón "Continuar":** Avanza al formulario de datos

**Comportamiento esperado:**

1. Muestra toda la información del vehículo seleccionado de manera clara
2. Indica claramente si aplica cargo por DropOff
3. Calcula correctamente puntos requeridos y saldo disponible
4. Para copago, permite distribuir entre puntos y dinero con slider
5. Valida saldo suficiente de puntos antes de continuar
6. Duración del alquiler se calcula correctamente en días
7. Políticas de cancelación son visibles y claras
8. Información es consistente con la selección de disponibilidad
9. Diferencia visualmente recogida en aeropuerto vs oficina si aplica

---

### **🔹 Datos de Contacto**

**Descripción:** Sección del checkout que captura la información de contacto del responsable de la reserva para notificaciones y confirmaciones.

**Componentes:**

- **Nombre** (campo de texto)
- **Apellido** (campo de texto)
- **Email\*** (campo de texto con validación)
- **Teléfono\*** (campo numérico con código de país)
- Indicadores de campo obligatorio (\*)
- Mensajes de error inline en color rojo

**Comportamiento esperado:**

1. Todos los campos son obligatorios
2. Solo permite letras y espacios en nombre/apellido (permite tildes y ñ)
3. Email debe incluir @ y dominio válido (.com, .co, .net, etc.)
4. Teléfono valida longitud según código de país seleccionado
5. Validaciones en tiempo real
6. No permite continuar sin datos completos y válidos
7. Información se usa para envío de confirmaciones y notificaciones
8. Muestra mensaje de error específico cuando falta campo obligatorio

---

### **🔹 Formulario de Datos del Conductor**

**Descripción:** Formulario obligatorio en el checkout donde se capturan los datos personales del conductor principal y licencia de conducir para la renta del vehículo.

**Componentes:**

**Campos del conductor:**

- **Nombre\*** (máximo 2 nombres)
- **Apellido\*** (máximo 2 apellidos)
- **Tipo de documento\*** (dropdown: DNI, CE, Pasaporte)
- **Número de documento\*** (campo alfanumérico)
- **Fecha de nacimiento\*** (datepicker con validación de edad)
- **Género\*** (dropdown: Masculino/Femenino)

**Campos de licencia de conducir:**

- **Número de licencia\*** (campo alfanumérico)
- **País de emisión\*** (dropdown con lista de países)
- **Fecha de emisión\*** (datepicker)
- **Fecha de vencimiento\*** (datepicker con validación de vigencia)

**Validaciones:**

- Validación de edad mínima (generalmente 21-25 años según país/rentadora)
- Validación de vigencia de licencia
- Validación de antigüedad mínima de licencia (típicamente 1-2 años)
- Indicadores de campo obligatorio (\*)
- Validaciones en tiempo real
- Mensajes de error específicos por campo
- Autocompletado si usuario tiene perfil registrado

**Comportamiento esperado:**

1. Sistema valida edad mínima requerida según país y rentadora (típicamente 21-25 años)
2. Muestra mensaje claro si conductor no cumple edad mínima
3. Solo permite letras y espacios en nombres/apellidos (permite tildes y ñ)
4. Máximo 2 nombres y 2 apellidos
5. Valida que licencia de conducir esté vigente (fecha de vencimiento futura)
6. Valida antigüedad mínima de licencia según políticas de rentadora
7. Fecha de emisión de licencia debe ser anterior a fecha actual
8. Fecha de vencimiento de licencia debe ser posterior a fecha de devolución del auto
9. No permite fechas de nacimiento que resulten en edad menor a la requerida
10. No permite caracteres especiales en documentos (excepto guiones)
11. Muestra mensajes de error claros por cada validación
12. Si aplica cargo por conductor joven, se muestra en desglose de precio

---

### **🔹 Servicios Adicionales (Upsell)**

**Descripción:** Sección opcional del checkout que permite agregar servicios extras a la renta del vehículo (seguros adicionales, GPS, silla de bebé, conductor adicional).

**Componentes:**

- Cards de servicios disponibles con descripción detallada
- Precio en puntos o moneda por servicio (diario o total)
- Checkboxes para selección de servicios
- Descripción clara de coberturas de seguros:
  - Seguro de colisión (CDW/LDW)
  - Seguro de responsabilidad civil
  - Seguro de efectos personales
- Extras de conveniencia:
  - GPS / Sistema de navegación
  - Silla de bebé / Silla infantil
  - Conductor adicional
- Resumen de total actualizado al seleccionar
- Servicios varían según rentadora (Hertz, Dollar, Thrifty) y destino

**Comportamiento esperado:**

1. Muestra solo servicios activos y disponibles para el vehículo/destino seleccionado
2. Cada servicio tiene descripción clara y precio visible
3. Indica claramente si precio es por día o total
4. Checkboxes funcionan correctamente
5. Total se actualiza automáticamente al seleccionar/deseleccionar
6. Precio de servicios se calcula correctamente (diario o total según aplique)
7. Admin refleja los servicios contratados en la reserva
8. Permite continuar sin seleccionar servicios (son opcionales)
9. Coberturas de seguros son claras y comprensibles

---

### **🔹 Métodos de Pago**

**Descripción:** Sección del checkout que permite seleccionar la forma de pago para la reserva de auto, incluyendo Solo Puntos, copago (Puntos + Cash), PSE y métodos de pago con tarjetas por país.

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

**Descripción:** Conjunto de validaciones complementarias que garantizan la seguridad, integridad y optimización del proceso de checkout de autos.

**Componentes:**

- Validación de edad mínima del conductor (típicamente 21-25 años)
- Validación de vigencia de licencia de conducir
- Validación de antigüedad mínima de licencia
- Encriptación de datos sensibles (tarjetas)
- Manejo de errores del servicio de pagos
- Checkbox "Requiero Factura" con campos de empresa y NIT/RFC/RUC
- Checkbox de términos y condiciones con link a políticas completas
- Validación de llamados de servicio (evitar duplicados)
- Políticas de combustible claras (lleno a lleno, lleno a vacío, etc.)
- Restricciones de edad por categoría de vehículo
- Validación de cargo adicional por conductor joven (si aplica)
- Tooltip de ayuda para licencia de conducir

**Comportamiento esperado:**

1. Sistema valida edad mínima antes de permitir continuar
2. Muestra mensaje claro si conductor no cumple edad mínima
3. Valida que licencia esté vigente al momento de recogida y durante toda la renta
4. Valida antigüedad mínima de licencia según políticas de rentadora
5. Datos de tarjeta se envían encriptados (validable en Network → Request Payload)
6. Errores de pago muestran mensajes claros con opción de reintentar
7. Puntos no quedan bloqueados si la transacción falla
8. Campo de factura aparece solo si se activa el checkbox
9. Campos de empresa y NIT/RFC/RUC validan formato correcto
10. No permite continuar sin aceptar términos y condiciones
11. Link a términos completos funciona y muestra políticas de renta
12. Servicio Create se invoca una única vez al cargar checkout (validar en Network)
13. Políticas de combustible son claras y visibles
14. Si aplica cargo por conductor joven, se muestra claramente en desglose
15. Restricciones de categoría por edad son validadas y comunicadas

---

## 📋 MÓDULO 4: CONFIRMACIÓN

### **Objetivo**

Mostrar resumen completo de la reserva de auto confirmada exitosamente después de procesar el pago.

### **Descripción**

Pantalla final que muestra la confirmación de la reserva de auto con todos los detalles, envío de correo de confirmación y canales de soporte.

### **URL**

```
https://demo-puntospe.smartlinks.dev/cars/confirmation
```

### **Precondiciones**

- ✅ Pago procesado exitosamente
- ✅ Reserva confirmada
- ✅ Puntos debitados

---

### **🔹 Código de Reserva / Localizador**

**Descripción:** Código único de la reserva que identifica la transacción.

**Componentes:**

- Código de reserva/localizador visible y destacado
- Formato alfanumérico único
- Texto explicativo: "Tu código de reserva es:"
- Opción de copiar código fácilmente

**Comportamiento esperado:**

1. Código se muestra inmediatamente después de pago exitoso
2. Código es único para cada reserva
3. Formato es claro y legible
4. Usuario puede copiar código fácilmente
5. Código aparece en el correo de confirmación

---

### **🔹 Información del Vehículo Confirmado**

**Descripción:** Sección que muestra el resumen del vehículo reservado.

**Componentes:**

- Nombre completo del vehículo (marca/modelo o similar)
- Categoría del vehículo
- Imagen del vehículo
- Capacidad de pasajeros
- Número de maletas
- Tipo de transmisión (Manual/Automática)
- Aire acondicionado (Sí/No)

**Comportamiento esperado:**

1. Información coincide exactamente con el vehículo seleccionado
2. Imagen del vehículo se muestra correctamente
3. Todas las características son visibles y legibles
4. Datos son consistentes con disponibilidad y checkout

---

### **🔹 Ubicaciones y Horarios**

**Descripción:** Sección que muestra las ubicaciones y horarios de recogida y devolución.

**Componentes:**

**Recogida:**

- Ubicación completa (ciudad, aeropuerto/oficina)
- Dirección exacta
- Fecha de recogida (formato: Día de la semana, DD de Mes de AAAA)
- Hora de recogida (formato: HH:MM)

**Devolución:**

- Ubicación completa (ciudad, aeropuerto/oficina)
- Dirección exacta
- Indicación clara si es DropOff (devolución en lugar diferente)
- Fecha de devolución (formato: Día de la semana, DD de Mes de AAAA)
- Hora de devolución (formato: HH:MM)

**Duración:**

- Duración total del alquiler en días
- Cálculo correcto desde recogida hasta devolución

**Comportamiento esperado:**

1. Fechas se muestran en formato largo en español
2. Horarios son precisos y coinciden con la reserva
3. Direcciones son completas y útiles para localización
4. Información de DropOff es clara si aplica
5. Duración calculada correctamente
6. Diferencia visualmente si es aeropuerto u oficina

---

### **🔹 Datos del Conductor**

**Descripción:** Sección que muestra la información del conductor registrado en la reserva.

**Componentes:**

- Nombre completo del conductor principal
- Tipo y número de documento
- Número de licencia de conducir
- Edad o fecha de nacimiento

**Comportamiento esperado:**

1. Todos los datos coinciden con los ingresados en el checkout
2. Información es legible y correctamente alineada
3. Datos sensibles pueden estar parcialmente enmascarados si aplica

---

### **🔹 Desglose de Pago**

**Descripción:** Sección que muestra el desglose completo del pago realizado.

**Componentes:**

- Precio base del vehículo
- Cargo por DropOff (si aplica)
- Servicios adicionales contratados con precios:
  - GPS
  - Silla de bebé
  - Conductor adicional
  - Seguros adicionales
- Fee de servicio
- **Total pagado en millas**
- Método de pago usado (Solo Puntos / Copago)
- Puntos debitados de la cuenta

**Comportamiento esperado:**

1. Cantidades muestran separador de miles (punto)
2. Total de Millas debitadas refleja el débito de la cuenta del usuario
3. Valores son consistentes con el precio mostrado en disponibilidad y checkout
4. Servicios adicionales se listan individualmente con sus precios
5. Cargo por DropOff se muestra solo si aplica
6. Desglose es claro y fácil de entender

---

### **🔹 Instrucciones y Políticas**

**Descripción:** Sección con información importante sobre la recogida del vehículo y políticas aplicables.

**Componentes:**

- **Instrucciones de recogida:**
  - Dirección exacta de la ubicación
  - Horarios de atención
  - Documentos requeridos (licencia, documento de identidad, tarjeta de crédito)
  - Proceso de recogida paso a paso

- **Políticas importantes:**
  - Política de combustible (lleno a lleno, lleno a vacío, etc.)
  - Política de cancelación
  - Restricciones de edad
  - Depósito o garantía requerida
  - Cobertura de seguro incluida

**Comportamiento esperado:**

1. Instrucciones son claras y completas
2. Dirección es exacta y útil para navegación
3. Horarios de atención son correctos
4. Lista de documentos requeridos es completa
5. Políticas son visibles y comprensibles
6. Política de combustible es clara

---

### **🔹 Confirmación por Correo y Canales de Soporte**

**Descripción:** Sección que notifica sobre el envío del correo de confirmación y proporciona canales de comunicación.

**Componentes:**

**Banner de correo:**

- Ícono de sobre/correo
- Mensaje principal: "La confirmación de tu reserva ha sido enviada al correo registrado."
- Mensaje secundario: "En caso de no recibirla, revise la bandeja de Correo no deseado."

**Canales de soporte:**

- WhatsApp con número de contacto
- Teléfono de soporte
- Email de contacto
- Horarios de atención

**Botones de acción:**

- **"Ver Resumen":** Muestra detalle completo de la reserva
- **"Descargar Voucher":** Genera PDF con todos los detalles
- **"Regresar al Home":** Vuelve al widget de búsqueda

**Comportamiento esperado:**

1. Correo de confirmación se envía automáticamente
2. Correo incluye todos los detalles: código de reserva, vehículo, fechas, ubicaciones, conductor
3. Formato del correo es correcto y profesional
4. Banner de notificación es visible y claro
5. Canales de soporte (WhatsApp, teléfono) son funcionales
6. Números de contacto y horarios son correctos
7. Botón "Ver Resumen" muestra información consistente
8. Botón "Descargar Voucher" genera PDF correctamente
9. PDF incluye: código de reserva, vehículo, ubicaciones, fechas, conductor, instrucciones
10. Botón "Regresar al Home" limpia el flujo y vuelve al inicio
11. Eventos de conversión (Meta Ads Pixel, Google Ads) se disparan correctamente

---

## 🧪 Casos de Prueba Recomendados

### **Prioridad 1 (Crítica)**

| ID          | Título                                                   | Escenario                   |
| ----------- | -------------------------------------------------------- | --------------------------- |
| CMP-AUT-001 | [CMP] Autos - 5 días - SABRE Hertz - Mismo lugar         | Flujo completo exitoso      |
| CMP-AUT-002 | [CMP] Autos - 3 días - SABRE Dollar - Dropoff diferente  | Flujo completo exitoso      |
| CMP-AUT-003 | [CMP] Autos - Sesión cross-domain - Validar persistencia | Navegación PPM → Meteor     |
| CMP-AUT-004 | [CMP] Autos - Sin resultados - Mensaje error             | Búsqueda sin disponibilidad |
| CMP-AUT-005 | [CMP] Autos - Devolución < Recogida - Validación         | Error de validación         |

### **Prioridad 2 (Alta)**

| ID          | Título                                                | Escenario           |
| ----------- | ----------------------------------------------------- | ------------------- |
| CMP-AUT-006 | [CMP] Autos - 7 días - SABRE Thrifty - SUV            | Flujo completo      |
| CMP-AUT-007 | [CMP] Autos - Filtros múltiples - Marca + Tipo        | Validar filtrado    |
| CMP-AUT-008 | [CMP] Autos - Modificar búsqueda - Precarga criterios | Edición de búsqueda |
| CMP-AUT-009 | [CMP] Autos - Edad conductor < mínimo                 | Validar restricción |
| CMP-AUT-010 | [CMP] Autos - Fecha pasada - Validación               | Error de validación |

### **Prioridad 3 (Media)**

| ID          | Título                                         | Escenario            |
| ----------- | ---------------------------------------------- | -------------------- |
| CMP-AUT-011 | [CMP] Autos - Ordenar por precio               | Validar ordenamiento |
| CMP-AUT-012 | [CMP] Autos - Ver detalles - Modal información | Validar popup        |
| CMP-AUT-013 | [CMP] Autos - Volver a Home PPM                | Navegación inversa   |
| CMP-AUT-014 | [CMP] Autos - Timeout de búsqueda              | Manejo de error      |
| CMP-AUT-015 | [CMP] Autos - Error de proveedor               | Manejo de error      |

---

## 📊 Comparación con Otros Modelos Kepler

| Aspecto          | PM                     | BGR                    | CME                    | PROM                   | **CMP**                    |
| ---------------- | ---------------------- | ---------------------- | ---------------------- | ---------------------- | -------------------------- |
| **Proveedor**    | SABRE                  | SABRE                  | SABRE                  | SABRE                  | **SABRE**                  |
| **Marcas**       | Hertz, Dollar, Thrifty | Hertz, Dollar, Thrifty | Hertz, Dollar, Thrifty | Hertz, Dollar, Thrifty | **Hertz, Dollar, Thrifty** |
| **Tecnología**   | N/A                    | N/A                    | N/A                    | N/A                    | **Meteor**                 |
| **Arquitectura** | Monolítica             | Monolítica             | Monolítica             | Monolítica             | **Multi-dominio**          |
| **Emisión**      | ⚠️ Pendiente           | ⚠️ Pendiente           | ⚠️ Pendiente           | ⚠️ Pendiente           | **⚠️ Pendiente**           |

---

## ✅ Información Validada

### **Modelo de Pago**

- ✅ Soporta Solo Puntos y Copago (Slider Millas + Cash)
- ✅ Fee de procesamiento se aplica y se refleja en Admin
- ✅ Cálculo dinámico en tiempo real para copago

### **Emisión**

- ✅ Sistema procesa automáticamente la reserva al confirmar compra
- ✅ Genera código de confirmación/localizador único
- ✅ Débito de millas se efectúa al confirmar

### **Checkout**

- ✅ Campos completos de datos de contacto y conductor documentados
- ✅ Validaciones de licencia de conducir (vigencia, antigüedad)
- ✅ Validaciones de documentos (DNI, CE, Pasaporte)
- ✅ Pasarelas de pago por país (Colombia, Perú, Ecuador, México, Chile)
- ✅ Extras opcionales: GPS, silla de bebé, conductor adicional, seguros
- ✅ Flujo completo: Resumen → Datos → Pago → Confirmación

### **Políticas y Restricciones**

- ✅ Edad mínima validada (típicamente 21-25 años según rentadora)
- ✅ Cargos por conductor joven se muestran en desglose si aplican
- ✅ Política de combustible clara (lleno a lleno, etc.)
- ✅ Cargo por DropOff calculado y mostrado cuando aplica
- ✅ Seguros opcionales disponibles en upsell
- ✅ Depósito/garantía informado en políticas

### **Funcionalidades Adicionales**

- ✅ DropOff funcional (devolución en ubicación diferente)
- ✅ Diferenciación entre recogida en aeropuerto vs oficina
- ✅ Código CDP (descuento) aplicado por defecto y editable
- ✅ Validaciones en tiempo real en todos los formularios
- ✅ Comprobante descargable en PDF
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
