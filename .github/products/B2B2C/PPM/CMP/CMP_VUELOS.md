# 🛫 CMP - Flujo E2E de Vuelos

> **Club Miles Perú** - Documentación completa del flujo End-to-End de Vuelos

---

## 📌 Información General

| Campo           | Valor                                       |
| --------------- | ------------------------------------------- |
| **Marketplace** | Club Miles Perú (CMP)                       |
| **Producto**    | Vuelos ✈️                                   |
| **Tecnología**  | Angular                                     |
| **URL**         | https://demotravel-puntospe.smartlinks.dev/ |
| **Prefijo**     | `[CMP]`                                     |
| **Estado**      | ✅ Activo                                   |

---

## 🔌 Proveedores de Vuelos

| Proveedor                | Tipo      | Estado    |
| ------------------------ | --------- | --------- |
| **AGGREGATOR NETACTICA** | Agregador | ✅ Activo |
| **AGGREGATOR SABRE**     | Agregador | ✅ Activo |
| **SABRE EDIFACT**        | Directo   | ✅ Activo |

**Características:**

- **3 proveedores agregadores** que consolidan múltiples aerolíneas
- Sistema busca en paralelo y consolida resultados
- Cada proveedor puede tener disponibilidad diferente

---

## 🏗️ Arquitectura

```
┌─────────────────────────────────────────────────────┐
│           FLUJO E2E VUELOS - CLUB MILES PERÚ        │
└─────────────────────────────────────────────────────┘

1️⃣ LOGIN (PPM)
   └─ https://clubmilesperu.preprodppm.com/
      ├─ Ingresar credenciales
      ├─ Validar OTP
      └─ Sesión establecida

2️⃣ HOME (PPM)
   └─ Dashboard Club Miles Perú
      ├─ Ver saldo de millas
      └─ Clic en "Vuelos" → Redirección cross-domain

3️⃣ MÓDULO VUELOS - HOME (Angular)
   └─ https://demotravel-puntospe.smartlinks.dev/flights
      ├─ Verificar sesión activa
      ├─ Formulario de búsqueda
      └─ Enviar búsqueda

4️⃣ DISPONIBILIDAD (Angular)
   └─ Resultados de búsqueda
      ├─ Listar vuelos de 3 proveedores
      ├─ Filtros y ordenamiento
      └─ Seleccionar vuelo(s)

5️⃣ CHECKOUT (Angular)
   └─ Confirmar reserva
      ├─ Datos de pasajeros
      ├─ ⚠️ Modelo de pago (pendiente confirmar)
      └─ Confirmación

6️⃣ CONFIRMACIÓN (Angular)
   └─ Resumen de reserva
      ├─ PNR generado
      ├─ Débito de millas
      └─ Email confirmación
```

---

## 📋 MÓDULO 1: HOME DE VUELOS

### **Objetivo**

Capturar criterios de búsqueda de vuelos del usuario

### **URL**

```
https://demotravel-puntospe.smartlinks.dev/flights
```

### **Precondiciones**

- ✅ Usuario autenticado en PPM
- ✅ Sesión activa transferida desde PPM
- ✅ VPN activa

### **Campos del Formulario de Búsqueda**

#### **1️⃣ Tipo de Viaje**

| Opción           | Descripción                     |
| ---------------- | ------------------------------- |
| **Ida y vuelta** | Vuelo de ida + vuelo de regreso |
| **Solo ida**     | Vuelo de ida únicamente         |
| **Multidestino** | Varios tramos de vuelo          |

#### **2️⃣ Origen**

- **Tipo:** Autocomplete
- **Validación:** Ciudad o aeropuerto válido
- **Formato:** Nombre ciudad (Código IATA)
- **Ejemplo:** Lima (LIM), Cusco (CUZ)

#### **3️⃣ Destino**

- **Tipo:** Autocomplete
- **Validación:** Ciudad o aeropuerto válido, diferente al origen
- **Formato:** Nombre ciudad (Código IATA)
- **Ejemplo:** Buenos Aires (EZE), Santiago (SCL)

#### **4️⃣ Fecha de Salida**

- **Tipo:** Date picker
- **Validación:** Fecha futura (hoy + 1 día mínimo típicamente)
- **Formato:** DD/MM/YYYY

#### **5️⃣ Fecha de Regreso** (solo Ida y vuelta)

- **Tipo:** Date picker
- **Validación:** Mayor a fecha de salida
- **Formato:** DD/MM/YYYY

#### **6️⃣ Pasajeros**

| Tipo        | Edad       | Límite |
| ----------- | ---------- | ------ |
| **Adultos** | 12+ años   | 1-9    |
| **Niños**   | 2-11 años  | 0-8    |
| **Bebés**   | 0-23 meses | 0-4    |

**Reglas:**

- Mínimo 1 adulto
- Máximo 9 pasajeros total
- Bebés no pueden exceder adultos

#### **7️⃣ Clase de Cabina**

- Económica
- Ejecutiva / Business
- Primera Clase

### **Validaciones Críticas**

| Validación                 | Comportamiento Esperado                      |
| -------------------------- | -------------------------------------------- |
| **Origen = Destino**       | Mensaje de error, bloquear búsqueda          |
| **Fecha pasada**           | Mensaje de error, bloquear búsqueda          |
| **Fecha regreso < salida** | Mensaje de error, ajustar automáticamente    |
| **Sin pasajeros**          | Mensaje de error, requerir al menos 1 adulto |
| **Campos vacíos**          | Mensaje de error, resaltar campos requeridos |

### **Acciones Disponibles**

- **Buscar:** Envía búsqueda a módulo de disponibilidad
- **Limpiar:** Resetea formulario a valores por defecto
- **Volver:** Regresa a dashboard PPM

---

## 📋 MÓDULO 2: DISPONIBILIDAD DE VUELOS

### **Objetivo**

Mostrar resultados de vuelos disponibles de los 3 proveedores

### **URL**

```
https://demotravel-puntospe.smartlinks.dev/flights/results
```

### **Precondiciones**

- ✅ Búsqueda enviada desde Home
- ✅ Criterios de búsqueda válidos

### **Estructura de Resultados**

#### **Sección Superior: Resumen de Búsqueda**

- Origen - Destino
- Fechas seleccionadas
- Pasajeros y clase
- **Botón "Modificar búsqueda"** → Regresa a Home con criterios precargados

#### **Sección Principal: Listado de Vuelos**

**Información por Vuelo:**

| Campo                | Descripción                       |
| -------------------- | --------------------------------- |
| **Aerolínea**        | Logo + nombre                     |
| **Proveedor**        | NETACTICA / SABRE / SABRE EDIFACT |
| **Hora salida**      | HH:MM                             |
| **Hora llegada**     | HH:MM                             |
| **Duración**         | Horas y minutos totales           |
| **Escalas**          | Directo / 1+ escalas              |
| **Precio en Millas** | ⚠️ Modelo pendiente confirmar     |
| **Copago**           | ⚠️ Si aplica Slider               |
| **Equipaje**         | Permitido (bodega + mano)         |

#### **Filtros Disponibles**

| Filtro        | Opciones                        |
| ------------- | ------------------------------- |
| **Aerolínea** | Checkboxes múltiples            |
| **Proveedor** | NETACTICA, SABRE, SABRE EDIFACT |
| **Escalas**   | Directo, 1 escala, 2+ escalas   |
| **Precio**    | Rango de millas                 |
| **Horarios**  | Mañana, tarde, noche            |
| **Duración**  | Rango en horas                  |

#### **Ordenamiento**

- Precio menor a mayor
- Duración menor a mayor
- Salida temprana a tardía
- Llegada temprana a tardía

### **Escenarios Posibles**

#### **✅ Resultados Encontrados**

- Mostrar vuelos disponibles de los 3 proveedores
- Permitir selección y continuar a checkout

#### **⚠️ Sin Resultados**

- Mensaje claro: "No se encontraron vuelos para tu búsqueda"
- Sugerencias: Modificar fechas, destinos, criterios
- Botón "Nueva búsqueda"

#### **❌ Error de Proveedores**

- Mensaje genérico de error
- Opción de reintentar
- No exponer detalles técnicos

### **Selección de Vuelo**

**Para Ida y Vuelta:**

1. Usuario selecciona vuelo de IDA
2. Usuario selecciona vuelo de REGRESO
3. Sistema valida compatibilidad de fechas/horarios
4. Botón "Continuar a checkout" se activa

**Para Solo Ida:**

1. Usuario selecciona vuelo
2. Botón "Continuar a checkout" se activa

---

## 📋 MÓDULO 3: CHECKOUT

### **Objetivo**

Capturar datos de pasajeros, información de contacto, servicios adicionales y procesar el pago para confirmar la reserva de vuelo.

### **Descripción**

Módulo de finalización de compra para vuelos donde se capturan los datos de pasajeros, información de contacto, se seleccionan servicios adicionales y se procesa el pago. Incluye validaciones de formularios, métodos de pago (Solo Puntos, Copago, Tarjetas), y generación de confirmación de reserva.

### **URL**

```
https://demotravel-puntospe.smartlinks.dev/flights/checkout
```

### **Precondiciones**

- ✅ Vuelo seleccionado desde módulo de Disponibilidad
- ✅ Usuario autenticado
- ✅ Sesión activa

---

### **🔹 Resumen de Reserva**

**Descripción:** Pantalla inicial del checkout que consolida la información del vuelo seleccionado antes de capturar datos de pasajeros, permitiendo verificar detalles y aplicación de puntos.

**Componentes:**

- **Banner informativo:**
  - Ícono de alerta (⚠)
  - Texto: "Conoce los cambios y cancelaciones que aplican es este vuelo."
  - Link: "Ver condiciones"

- **Área principal izquierda - Detalle de vuelos:**
  - **Sección SALIDA:**
    - Encabezado: "[ORIGEN] A [DESTINO]" - "día de la semana, DD de mes de AAAA"
    - Logo de aerolínea
    - Nombre de aerolínea
    - Tipo de vuelo: "Directo" o "[N] Escalas"
    - Horarios: "HH:MM (Día, DD Mes.) - HH:MM (Día, DD Mes.)"
    - Ruta: "Ciudad Origen → Ciudad Destino (Número de vuelo: XXX)"
    - Duración total: "XXhYYm"
    - Iconos de servicio (equipaje: V)
    - Tipo de tarifa: Badge "BÁSICA"
  - **Sección REGRESO:**
    - Misma estructura que SALIDA
    - Para vuelos con escalas, muestra cada segmento:
      - Segmento 1: Horarios, ruta, número de vuelo, iconos
      - Segmento 2: Horarios, ruta, número de vuelo, iconos
      - Segmento N: Horarios, ruta, número de vuelo, iconos
    - Duración total incluye todas las escalas

- **Panel lateral derecho - "Resumen de compra":**
  - Encabezado: "Resumen de compra" con fondo rojo
  - **Salida:**
    - Fecha completa: "Día de la semana, DD De Mes De AAAA"
    - Ruta con horarios: "[Ciudad] ([CÓDIGO]) HH:MM - [Ciudad] ([CÓDIGO]) HH:MM"
    - Aerolínea y número(s) de vuelo: "Aerolínea - XXX"
  - **Regreso:**
    - Fecha completa: "Día de la semana, DD De Mes De AAAA"
    - Ruta con horarios: "[Ciudad] ([CÓDIGO]) HH:MM - [Ciudad] ([CÓDIGO]) HH:MM"
    - Aerolínea y número(s) de vuelo: "Aerolínea - XXX, YYY, ZZZ" (múltiples números si hay escalas)
  - **Pasajeros:**
    - Desglose por tipo: "Adultos (N)", "Niños (N)", "Bebés (N)"
  - **Clases:**
    - Tipo de cabina seleccionada: "Todas las clases" o clase específica
  - **Subtotal:**
    - Precio total destacado: "XX.XXX Millas"
  - **Botón "Continuar":** Botón rojo para avanzar al formulario de pasajeros

**Comportamiento esperado:**

1. Muestra toda la información del vuelo seleccionado de manera clara y estructurada
2. Banner informativo es visible y el link "Ver condiciones" abre modal/página con T&C
3. Para vuelos directos, muestra "Directo" en tipo de vuelo
4. Para vuelos con escalas, muestra cantidad ("2 Escalas") y lista cada segmento con detalles completos
5. Fechas se muestran en formato largo en español
6. Códigos de aeropuerto (IATA) se muestran junto a nombres de ciudad
7. En panel "Resumen de compra", números de vuelo se concatenan con comas cuando hay múltiples segmentos
8. Duración total incluye tiempo de vuelo y escalas
9. Subtotal muestra precio en millas con separador de miles (punto)
10. Botón "Continuar" está habilitado y navega a formulario de pasajeros
11. Iconos de equipaje (V) y badges de tarifa ("BÁSICA") se muestran correctamente
12. Layout responsivo: en desktop, detalle a la izquierda y resumen a la derecha

---

### **🔹 Datos de Contacto del Comprador**

**Descripción:** Sección ubicada en la parte superior del checkout que captura la información del responsable de la compra antes de solicitar los datos de los pasajeros.

**Componentes:**

- **Nombres \*** (campo de texto)
- **Apellidos \*** (campo de texto)
- **Tipo de documento \*** (dropdown)
- **Número de documento \*** (campo numérico)
- **Email \*** (campo de texto)
- **Teléfono \*** (campo numérico)
- **Ciudad \*** (campo de texto con autocompletado)
- **Dirección \*** (campo de texto con autocompletado inteligente)
- Indicadores de campo obligatorio (\*)
- Mensajes de error inline en color rojo
- Sistema de sugerencias para dirección (dropdown con opciones)

**Comportamiento esperado:**

1. Todos los campos son obligatorios
2. Solo permite letras y espacios en nombres/apellidos (permite tildes y ñ)
3. Email valida formato con @ y dominio válido
4. Teléfono solo acepta números
5. Ciudad puede autocompletar según entrada del usuario
6. Dirección muestra sugerencias de autocompletado al escribir
7. Muestra mensaje de error específico cuando falta campo obligatorio
8. Validaciones en tiempo real
9. No permite avanzar sin completar correctamente todos los campos

---

### **🔹 Información de Pasajeros**

**Descripción:** Formulario obligatorio en el checkout donde se capturan los datos personales de cada pasajero (ADT, CHL, INF) para la emisión del boleto aéreo.

**Componentes:**

- **Título de sección:** "Información de pasajeros"
- **Subsección por pasajero:** "Adulto 1 ( +2 Años o más )", "Niño 1 ( 2-11 años )", "Bebé 1 ( 0-23 meses )"

**Campos principales del pasajero:**

- **Género \*** (dropdown: Masculino/Femenino)
- **Nombres \*** (campo de texto con placeholder)
- **Apellidos \*** (campo de texto con placeholder)
- **Tipo de documento \*** (dropdown)
- **Número de documento \*** (campo numérico/alfanumérico)
- **Fecha de nacimiento \*** (datepicker con ícono de calendario)
- **Nacionalidad \*** (dropdown con lista de países)

**Subsección: "Datos del pasaporte" (texto en rojo):**

- **Pasaporte \*** (campo de texto)
- **Fecha de expiración \*** (datepicker con ícono de calendario)

**Subsección: "Datos del viajero frecuente" (texto en rojo):**

- **Aerolínea de viajero frecuente** (dropdown con lista de aerolíneas)
- **Viajero frecuente** (campo de texto)

- Indicadores de campo obligatorio (\*)
- Validaciones en tiempo real
- Mensajes de error inline específicos por campo
- Placeholders descriptivos en cada campo

**Comportamiento esperado:**

1. Sistema genera formulario por cada pasajero según búsqueda original
2. Título de subsección indica tipo y rango de edad del pasajero
3. Solo permite letras y espacios en nombres/apellidos (permite tildes y ñ)
4. Valida edad calculada coincida con tipo de pasajero según fecha de nacimiento
5. No permite fechas de nacimiento futuras
6. Datepicker muestra formato AAAA-MM-DD
7. Dropdown de nacionalidad permite búsqueda de países
8. Sección "Datos del pasaporte" en rojo para destacar importancia
9. Campos de viajero frecuente son opcionales
10. No permite caracteres especiales en documentos (excepto guiones)
11. Muestra mensajes de error claros por cada validación
12. Para INF: valida asociación con adulto acompañante

---

### **🔹 Panel de Resumen y Finalización de Compra**

**Descripción:** Panel lateral persistente que muestra el resumen consolidado de la reserva, checkbox de términos y condiciones, y botón de compra que se habilita al completar correctamente todos los campos.

**Componentes:**

**Panel lateral derecho:**

- **Salida:** Fecha, ruta con códigos IATA y horarios, números de vuelo
- **Regreso:** Fecha, ruta con códigos IATA y horarios, números de vuelo
- **Pasajeros:** Desglose por tipo con cantidad
- **Clases:** Tipo de cabina seleccionada
- **Total:** Precio en millas con separador de miles

**Sección de términos:**

- **Checkbox:** "Declaro conocer los Términos & condiciones del producto/servicio" (con link azul clickeable)

**Botón de compra:**

- **Botón "Comprar":** Color rojo/óxido, texto centrado en blanco

**Mensaje de validación:**

- Texto en rojo: "Para reservar, completa correctamente todos los datos del formulario."

**Comportamiento esperado:**

1. Panel permanece visible y fijo durante scroll del formulario
2. Total en millas se muestra con formato de separador de miles (punto)
3. Números de vuelo se concatenan con comas cuando hay múltiples segmentos
4. Link "Términos & condiciones del producto/servicio" abre modal o nueva pestaña con T&C
5. Checkbox debe marcarse manualmente por el usuario
6. Botón "Comprar" inicia deshabilitado (color gris)
7. Mensaje de validación en rojo es visible cuando formulario está incompleto
8. Al completar todos los campos obligatorios correctamente:
   - Mensaje de validación desaparece
   - Botón "Comprar" se habilita (color rojo activo)
   - Checkbox de términos debe estar marcado
9. Al hacer clic en "Comprar" con formulario completo y checkbox marcado, abre modal de confirmación
10. Panel muestra información consistente con la selección de vuelo original
11. Si intenta comprar sin marcar términos, muestra mensaje de error

---

### **🔹 Modal de Confirmación de Reserva**

**Descripción:** Modal que aparece al hacer clic en el botón "Comprar" para que el usuario revise el resumen final de su reserva antes de procesarla.

**Componentes:**

**Título del modal:**

- "Resumen de la reserva"

**Sección Pasajeros:**

- Lista de pasajeros con formato: "Nombre Apellido - (Número de documento)"

**Sección Ruta:**

- **Para cada vuelo (ida/regreso):**
  - Logo y nombre de aerolínea
  - Tipo de vuelo: "Directo" o "N Escalas"
  - Duración total (formato: "XXhYYm") con ícono de reloj
  - Horarios y fechas: "HH:MM (día, DD mes.) HH:MM (día, DD mes.)"
  - Ruta con flecha: "Ciudad Origen → Ciudad Destino"
- **Para vuelos con escalas, muestra cada segmento:**
  - Horario de salida y llegada de cada tramo
  - Ruta de cada segmento con flecha: "Ciudad → Ciudad"

**Sección Total:**

- Texto "Total:" en color turquesa
- Precio destacado en color rojo/vino: "XX.XXX Millas"

**Botones de acción:**

- **Botón "VOLVER":** Estilo outlined, alineado a la izquierda
- **Botón "COMPRAR":** Estilo filled, color azul, alineado a la derecha

**Comportamiento esperado:**

1. Modal se abre automáticamente al hacer clic en botón "Comprar" del panel lateral
2. Modal tiene overlay oscuro sobre el formulario de checkout
3. Muestra resumen consolidado de todos los pasajeros ingresados
4. Para cada vuelo, muestra información completa y legible
5. Vuelos directos muestran solo un tramo con horarios de salida y llegada
6. Vuelos con escalas listan cada segmento con sus respectivos horarios y rutas
7. Duración incluye tiempo total del viaje (vuelo + escalas)
8. Total en millas muestra separador de miles (punto)
9. Botón "VOLVER" cierra el modal y regresa al checkout sin procesar
10. Botón "COMPRAR" procesa la reserva, bloquea puntos y navega a confirmación
11. Modal es responsive y centrado en pantalla
12. No permite cerrar modal haciendo clic fuera (debe usar botones)
13. Al confirmar compra, muestra loader/indicador de procesamiento

---

### **🔹 Servicios Adicionales (Upsell)**

**Descripción:** Sección opcional del checkout que permite agregar servicios extras a la reserva de vuelo (equipaje adicional, asientos preferenciales, seguros de viaje).

**Componentes:**

- Cards de servicios disponibles con descripción y precio
- Checkboxes para selección de servicios
- Precio en puntos o moneda por servicio
- Resumen de total actualizado al seleccionar
- Servicios varían según aerolínea y destino
- Disponibilidad para clientes de diferentes programas (CMP, Banamex)

**Comportamiento esperado:**

1. Muestra solo servicios activos y disponibles para el vuelo seleccionado
2. Cada servicio tiene descripción clara y precio visible
3. Checkboxes funcionan correctamente
4. Total se actualiza automáticamente al seleccionar/deseleccionar
5. Servicios en USD y COP se manejan correctamente
6. Admin refleja los servicios contratados en la reserva
7. Permite continuar sin seleccionar servicios (son opcionales)

---

### **🔹 Métodos de Pago**

**Descripción:** Sección del checkout que permite seleccionar la forma de pago para la reserva, incluyendo Solo Puntos, copago (Puntos + Cash), PSE y métodos de pago con tarjetas por país.

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
   - Método de pago en sistema externo (Sabre, Netactica) debe registrarse como "Cash"

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
11. Fee aprobado (Fee approved) debe reflejarse en Admin

---

### **🔹 Validaciones y Elementos Complementarios**

**Descripción:** Conjunto de validaciones complementarias que garantizan la seguridad, integridad y optimización del proceso de checkout de vuelos.

**Componentes:**

- Desglose de tarifa de servicios (fee de checkout)
- Encriptación de datos sensibles (tarjetas)
- Manejo de errores del servicio de pagos
- Checkbox "Requiero Factura" con campos de empresa y NIT/RFC/RUC
- Checkbox de términos y condiciones con link a políticas completas
- Tooltip de ayuda para documento de viaje
- reCAPTCHA para validación de seguridad
- Mensaje informativo para menores de 2 años
- Selector de fecha de nacimiento (datepicker)
- Validación de llamados de servicio (evitar duplicados)
- Opción de editar número de pasajeros

**Comportamiento esperado:**

1. Fee de servicio se muestra en desglose de precio (base + fee + total)
2. Datos de tarjeta se envían encriptados (validable en Network → Request Payload)
3. Errores de pago muestran mensajes claros con opción de reintentar
4. Puntos no quedan bloqueados si la transacción falla
5. Campo de factura aparece solo si se activa el checkbox
6. Campos de empresa y NIT/RFC/RUC validan formato correcto
7. No permite continuar sin aceptar términos y condiciones
8. Link a términos completos funciona y muestra políticas
9. Tooltip de documento de viaje muestra información clara sobre tipo requerido
10. reCAPTCHA valida correctamente antes de acceder a checkout
11. Mensaje aparece cuando hay INF: "Menores de 2 años deben viajar con padre/madre/tutor"
12. Datepicker permite seleccionar fecha de nacimiento fácilmente
13. Servicio Create se invoca una única vez al cargar checkout (validar en Network)
14. Opción de editar pasajeros vuelve a disponibilidad sin perder selección si hay stock

---

## 📋 MÓDULO 4: CONFIRMACIÓN

### **Objetivo**

Mostrar resumen completo de la reserva confirmada exitosamente después de procesar el pago.

### **Descripción**

Pantalla final que muestra la confirmación exitosa de la reserva de vuelo después de procesar el pago. Incluye resumen de la transacción, información del pasajero, detalles del pago en millas, comprobante de transacción y notificación de envío de confirmación por correo.

### **URL**

```
https://demotravel-puntospe.smartlinks.dev/flights/confirmation
```

### **Precondiciones**

- ✅ Pago procesado exitosamente
- ✅ Reserva confirmada
- ✅ Puntos debitados

---

### **🔹 Información del Vuelo Confirmado**

**Descripción:** Sección que muestra el resumen del itinerario del vuelo reservado.

**Componentes:**

- Logo de aerolínea
- Nombre de aerolínea
- Tipo de vuelo: "Directo" o "N Escalas"
- Rutas del vuelo con ciudades origen y destino
- Para vuelos con escalas: lista de todos los segmentos

**Comportamiento esperado:**

1. Muestra logo de aerolínea correctamente
2. Indica claramente si es vuelo directo o con escalas
3. Para vuelos con escalas, lista cada segmento en orden
4. Información coincide exactamente con el vuelo seleccionado

---

### **🔹 Datos del Pasajero**

**Descripción:** Sección que muestra la información del pasajero registrado en la reserva.

**Componentes:**

- **Nombre:** Nombre completo del pasajero
- **Email:** Correo electrónico registrado
- **Género:** Masculino/Femenino
- **Fecha de nacimiento:** Formato "mes, DD set. AAAA"

**Comportamiento esperado:**

1. Todos los datos coinciden con los ingresados en el checkout
2. Formato de fecha en español
3. Datos son legibles y correctamente alineados
4. Si hay múltiples pasajeros, se listan todos

---

### **🔹 Resumen de Pago en Millas**

**Descripción:** Sección que muestra el desglose del pago realizado en millas.

**Componentes:**

- **Total de Millas redimidas:** Cantidad de millas utilizadas
- **Total Pagado:** Cantidad total pagada en millas

**Comportamiento esperado:**

1. Cantidades muestran separador de miles (punto)
2. Total de Millas redimidas refleja el débito de la cuenta del usuario
3. Total Pagado puede incluir copago si aplica
4. Valores son consistentes con el precio mostrado en disponibilidad y checkout

---

### **🔹 Banner de Notificación de Correo**

**Descripción:** Banner informativo que notifica al usuario sobre el envío de la confirmación por email.

**Componentes:**

- Ícono de sobre/correo en color rojo
- Mensaje principal: "La confirmación de su canje y su reserva han sido enviadas al correo registrado."
- Mensaje secundario destacado: "En caso de no recibirlas, revise la bandeja de Correo no deseado." (en negrita y rojo)

**Comportamiento esperado:**

1. Banner es prominente y visible en la pantalla
2. Ícono de correo se muestra correctamente
3. Texto secundario sobre correo no deseado está en negrita y color rojo
4. Mensaje es claro y ayuda al usuario a encontrar el email
5. Banner se muestra inmediatamente al cargar la confirmación

---

### **🔹 Comprobante de Transacción**

**Descripción:** Panel lateral que muestra el detalle completo de la transacción realizada con toda la información necesaria para auditoría y seguimiento.

**Componentes:**

**Encabezado:**

- Badge verde: "Transacción aprobada"

**Campos del comprobante:**

- **Referencia:** Código único alfanumérico de la transacción
- **Autorización/CUS:** Código numérico de autorización
- **Cliente:** Nombre completo del cliente
- **Email:** Correo electrónico del cliente
- **Razón social:** Nombre de la agencia/programa (ej: "ClubMiles PE")
- **Nit:** Número de identificación tributaria
- **Fecha y hora:** Timestamp en formato "AAAA-MM-DD HH:MM"
- **Estado:** "Transacción aprobada"
- **Motivo:** "Transacción con MILLAS"
- **Valor:** Cantidad en millas con link azul clickeable

**Pie de sección:**

- Texto de contacto: "Para mayor información comunicarse con [Agencia] al teléfono [número] o escribirnos al correo [email]"

**Botones de acción:**

- Descargar comprobante (PDF)
- Imprimir comprobante
- Regresar al Home

**Comportamiento esperado:**

1. Badge verde "Transacción aprobada" es prominente y visible
2. Código de referencia es único para cada transacción
3. Fecha y hora corresponden al momento exacto de la confirmación
4. Email y cliente coinciden con datos ingresados
5. Razón social y Nit corresponden a ClubMiles PE
6. Estado siempre muestra "Transacción aprobada" en pantalla de éxito
7. Link en "Valor" permite ver detalle adicional o descargar comprobante
8. Información de contacto es específica de la agencia
9. Usuario puede imprimir o guardar comprobante
10. Todos los campos son de solo lectura
11. Comprobante permanece fijo durante scroll si hay contenido extenso
12. PNR / Código de reserva es visible y copiable
13. Botones de descarga e impresión funcionan correctamente

---

## 🧪 Casos de Prueba Recomendados

### **Prioridad 1 (Crítica)**

| ID          | Título                                                    | Escenario                   |
| ----------- | --------------------------------------------------------- | --------------------------- |
| CMP-VUE-001 | [CMP] Vuelos - Ida y vuelta - SABRE - 1 adulto            | Flujo completo exitoso      |
| CMP-VUE-002 | [CMP] Vuelos - Solo ida - NETACTICA - 2 adultos           | Flujo completo exitoso      |
| CMP-VUE-003 | [CMP] Vuelos - Sesión cross-domain - Validar persistencia | Navegación PPM → Angular    |
| CMP-VUE-004 | [CMP] Vuelos - Sin resultados - Mensaje error             | Búsqueda sin disponibilidad |
| CMP-VUE-005 | [CMP] Vuelos - Origen = Destino - Validación              | Error de validación         |

### **Prioridad 2 (Alta)**

| ID          | Título                                                 | Escenario           |
| ----------- | ------------------------------------------------------ | ------------------- |
| CMP-VUE-006 | [CMP] Vuelos - Multidestino - 3 tramos                 | Flujo completo      |
| CMP-VUE-007 | [CMP] Vuelos - Filtros múltiples - Aerolínea + Escalas | Validar filtrado    |
| CMP-VUE-008 | [CMP] Vuelos - Modificar búsqueda - Precarga criterios | Edición de búsqueda |
| CMP-VUE-009 | [CMP] Vuelos - 1 adulto + 2 niños + 1 bebé             | Validar pasajeros   |
| CMP-VUE-010 | [CMP] Vuelos - Fecha regreso < salida                  | Error de validación |

### **Prioridad 3 (Media)**

| ID          | Título                             | Escenario            |
| ----------- | ---------------------------------- | -------------------- |
| CMP-VUE-011 | [CMP] Vuelos - Ordenar por precio  | Validar ordenamiento |
| CMP-VUE-012 | [CMP] Vuelos - Limpiar filtros     | Resetear criterios   |
| CMP-VUE-013 | [CMP] Vuelos - Volver a Home PPM   | Navegación inversa   |
| CMP-VUE-014 | [CMP] Vuelos - Timeout de búsqueda | Manejo de error      |
| CMP-VUE-015 | [CMP] Vuelos - Error de proveedor  | Manejo de error      |

---

## 📊 Comparación con Otros Modelos Kepler

| Aspecto          | PM            | BGR           | CME           | PROM         | **CMP**           |
| ---------------- | ------------- | ------------- | ------------- | ------------ | ----------------- |
| **Proveedores**  | 3 agregadores | 3 agregadores | 3 agregadores | ⚠️ Pendiente | **3 agregadores** |
| **Tecnología**   | N/A           | N/A           | N/A           | N/A          | **Angular**       |
| **Arquitectura** | Monolítica    | Monolítica    | Monolítica    | Monolítica   | **Multi-dominio** |
| **Emisión**      | Automática    | Auto/Manual   | Auto/Manual   | ⚠️ Pendiente | **⚠️ Pendiente**  |
| **Fees**         | Sí            | No            | ⚠️ Pendiente  | ⚠️ Pendiente | **⚠️ Pendiente**  |

---

## ✅ Información Validada

### **Modelo de Pago**

- ✅ Soporta Solo Puntos y Copago (Slider Millas + Cash)
- ✅ Fee de procesamiento se aplica y se refleja en Admin
- ✅ Método de pago en proveedores externos se registra como "Cash"

### **Emisión**

- ✅ Sistema procesa automáticamente la reserva al confirmar compra
- ✅ Genera PNR/Código de reserva único
- ✅ Débito de millas se efectúa al confirmar

### **Checkout**

- ✅ Campos completos de datos de contacto y pasajeros documentados
- ✅ Validaciones de documentos (DNI, pasaporte, etc.)
- ✅ Pasarelas de pago por país (Colombia, Perú, Ecuador, México, Chile)
- ✅ Flujo completo: Resumen → Datos → Pago → Confirmación
- ✅ Servicios adicionales (Upsell) disponibles

### **Funcionalidades Adicionales**

- ✅ Multidestino disponible en búsqueda
- ✅ Validaciones en tiempo real
- ✅ Modal de confirmación antes de procesar
- ✅ Comprobante de transacción descargable
- ✅ Email de confirmación automático

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

- **2026-02-02 (v1.1):** Actualización completa de Módulos 3 y 4 con información del Knowledge_Base_CMP.md
  - ✅ Módulo 3 (Checkout): Agregada URL y Precondiciones
  - ✅ Módulo 4 (Confirmación): Agregada URL y Precondiciones
  - ✅ Todas las funcionalidades documentadas con componentes completos y comportamientos esperados
- **2026-01-26 (v1.0):** Documentación inicial completa de todos los módulos
