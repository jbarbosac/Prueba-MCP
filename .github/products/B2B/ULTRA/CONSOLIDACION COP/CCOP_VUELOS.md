# 📋 [CCOP] VUELOS - Consolidación COP

> Documentación específica para el producto VUELOS en Consolidación COP (Colombia).

---

## 🎯 IDENTIFICACIÓN

**Producto:** Vuelos  
**Portal:** Consolidación COP  
**País:** Colombia  
**Prefijo:** [CCOP]  
**Framework:** Angular  
**Estado:** ✅ EN CONFIGURACIÓN  

---

## 📦 PROVEEDORES

### **Proveedor 1: AGGREGATOR NETACTICA**
- **Nombre:** Netactica Aggregator
- **Tecnología:** API REST
- **Características:**
  - Múltiples aerolíneas disponibles
  - Búsqueda en tiempo real
  - Consolidador de contenido aéreo
  - Soporte para vuelos nacionales e internacionales

### **Proveedor 2: AGGREGATOR SABRE**
- **Nombre:** Sabre Aggregator
- **Tecnología:** API REST
- **Características:**
  - GDS global con amplia cobertura
  - Múltiples aerolíneas disponibles
  - Búsqueda en tiempo real
  - Soporte para vuelos nacionales e internacionales

### **Proveedor 3: SABRE EDIFACT**
- **Nombre:** Sabre EDIFACT
- **Tecnología:** EDIFACT
- **Características:**
  - Sistema tradicional de GDS
  - Formato EDIFACT estándar
  - Amplia cobertura de aerolíneas
  - Requiere procesamiento EDIFACT

---

## 💰 MODELO DE NEGOCIO

### **ECUACIÓN DE PAGO:**

**DOS MÉTODOS DE PAGO DISPONIBLES:**

```
MÉTODO 1: Tarjeta de Crédito/Débito
   → Pago: 100% TARJETA DE CRÉDITO/DÉBITO
   → Emisión: AUTOMÁTICA
   → Estado final: EMITIDA (si aprobada) o PENDIENTE (si rechazada)

MÉTODO 2: Pago en Agencia
   → Pago: 100% EFECTIVO O TARJETA EN AGENCIA
   → Emisión: MANUAL (requiere confirmación de pago)
   → Estado final: PENDIENTE → EMITIDA (tras confirmación en Admin)
```

### **CARGOS ADICIONALES (FEES):**

```
1. Tarifa Administrativa (TA) - Visible
   → Tipo: Fija o Porcentual (configurable en Admin)
   → Visibilidad: Cliente ve el cargo desglosado
   → Se suma al precio final
   → Es opcional (se configura por marketplace)
   → Configuración: Según configuración en el Admin

2. Fee Oculto (No Visible)
   → Tipo: Fijo o Porcentual (configurable en Admin)
   → Visibilidad: Cliente NO lo ve desglosado
   → Incluido en precio final
   → REGLA: Solo se activa si la TA está configurada
   → NO existe escenario donde Fee Oculto activo + TA inactiva
   → Configuración: Según configuración en el Admin
```

**Componentes:**
- **Producto:** 100% Efectivo (Tarjeta de Crédito/Débito o Efectivo en Agencia)
- **Fee Visible:** Sí - Tarifa Administrativa (fija o porcentual)
- **Fee Oculto:** Sí - No desglosado al cliente
- **Slider:** NO aplica (no hay millas/puntos)
- **Tarjeta requerida:** Opcional (depende del método de pago seleccionado)

**Validaciones de pago:**
- ❌ NO aplica validación de saldo (no usa millas/puntos)
- ✅ Validar datos de tarjeta si selecciona pago con tarjeta
- ✅ Validar selección de método de pago
- ✅ Validar monto total incluyendo fees

---

## 🔄 FLUJO DE COMPRA

**Estructura de pantallas:**
1. **Home** - Página principal del portal
2. **Disponibilidad** - Resultados de búsqueda con filtros
3. **Resumen de disponibilidad** - Detalle del vuelo seleccionado
4. **Checkout** - Formulario de datos y pago
5. **Confirmación** - Confirmación de reserva emitida

---

### **1. BÚSQUEDA**

**Campos obligatorios:**
- Origen (ciudad/aeropuerto)
- Destino (ciudad/aeropuerto)
- Fecha de ida
- Tipo de viaje (ida/ida y vuelta)
- Número de pasajeros (adultos/niños/infantes)

**Validaciones:**
- Fecha de ida no puede ser anterior a hoy
- Fecha de vuelta debe ser posterior a fecha de ida
- Origen y destino no pueden ser iguales
- **Validaciones de pasajeros:**
  - Adultos: Mayores de 12 años
  - Niños: De 2 a 11 años
  - Infantes: Menores de 2 años
  - Un niño NO puede viajar solo (requiere mínimo 1 adulto)
  - 1 adulto puede viajar máximo con 2 niños y 1 infante
  - Máximo por reserva: 5 adultos + 4 niños y/o infantes

### **2. DISPONIBILIDAD (Resultados de Búsqueda)**

**Información mostrada:**
- Aerolínea
- Número de vuelo
- Horarios (salida/llegada)
- Duración
- Escalas
- Precio en COP
- Clase de servicio

**Filtros disponibles:**
- Precio
- Escala
- Equipaje
- Horario de regreso
- Horario de salida
- Carrousel de aerolíneas

**Filtros Inspiracionales:**
- Fechas Flexibles
- Tendencia de precios
- Explorar Destinos

**Nueva búsqueda desde disponibilidad:**
- Ida y vuelta
- Solo ida
- Multidestino
- Solo vuelos directos

**Opciones avanzadas:**
- Hora de salida
- Hora de regreso
- Clase
- Aerolínea

**Funcionalidades adicionales:**
- Aplicar código promocional (promocode)

### **3. RESUMEN DE DISPONIBILIDAD (Detalle del Vuelo)**

**Información del vuelo:**
- Detalles completos del itinerario
- Política de equipaje (según información del proveedor)
- Términos y condiciones
- Política de cambios/cancelación
- Servicios incluidos

**Política de Equipaje:**
- Se muestra la información de equipaje que retorna el proveedor
- NO hay opción de agregar equipaje adicional en checkout
- El cliente NO puede pagar por equipaje extra
- La reserva se realiza con el equipaje incluido por el proveedor
- Puede variar según aerolínea y proveedor

**Validaciones:**
- Disponibilidad confirmada antes de continuar
- Precio bloqueado temporalmente
- [OTRAS - A DEFINIR]

### **4. CHECKOUT**

**Campos del formulario:**

**1. Datos de Pasajeros:**
- Nombre completo - Obligatorio
- Apellido - Obligatorio
- Tipo de documento (Cédula/Pasaporte) - Obligatorio
- Número de documento - Obligatorio
- Fecha de nacimiento - Obligatorio
- Nacionalidad - Obligatorio (para vuelos internacionales)
- **Para vuelos internacionales:**
  - Fecha de expiración del pasaporte - Obligatorio

**Categorías de pasajeros:**
- Adultos: Mayores de 12 años
- Niños: De 2 a 11 años
- Infantes: Menores de 2 años
- **Nota:** No hay restricciones especiales para infantes
- **Nota:** No hay validaciones adicionales para infantes en checkout

**2. Datos de Contacto:**
- Email - Obligatorio
- Teléfono - Obligatorio

**3. Datos de Facturación:**
- Tipo de persona: Natural o Jurídica - Obligatorio
- **Persona Natural:**
  - Nombres
  - Apellidos
  - Tipo de documento
  - Número de documento
- **Persona Jurídica:**
  - Razón social
  - Tipo de documento
  - Número de documento (NIT)
- Dirección - Obligatorio
- Ciudad - Obligatorio
- Teléfono - Obligatorio

**4. Método de Pago:**
- Selección: Tarjeta de Crédito/Débito o Pago en Agencia - Obligatorio
- **Si Tarjeta:**
  - Nombre del titular
  - Apellido del titular
  - Tipo de documento del titular
  - Número de documento del titular
  - Número de tarjeta
  - Mes de expiración
  - Año de expiración
  - CVV (3 o 4 dígitos)
- **Si Pago en Agencia:**
  - Solo confirmación (sin datos adicionales)

**5. Seguro de Cancelación - ILS (Opcional):**
- **Proveedor:** AssistViaje
- **Aplica solo para:** Vuelos internacionales
- **Se aplica:** Por cada pasajero
- **Restricción:** No aplica para personas mayores a 74 años
- **Costo:** El proveedor AssistViaje retorna la tarifa específica para el vuelo
- **Pantalla de confirmación:** Si se agrega seguro ILS, se muestra pantalla especial de confirmación (NO la estándar de marketplace)

**6. Habeas Data:**
- Aceptación obligatoria

**7. Términos y Condiciones:**
- Aceptación obligatoria

**Validaciones críticas:**
- Formato de documento válido (Cédula: 10 dígitos; Pasaporte: alfanumérico)
- Edad del pasajero válida según categoría (adulto/niño/infante)
- Email válido
- Teléfono válido
- Tarjeta válida (si aplica)
- Términos y condiciones aceptados

### **5. CONFIRMACIÓN**

**Tipo de emisión:** Automática (pago tarjeta) / Manual (pago agencia)

**Flujo Emisión Automática (Pago Tarjeta):**
```
Usuario confirma compra con tarjeta
       ↓
Sistema procesa pago en pasarela PlacetoPay
       ↓
¿Pago APROBADO?
   SÍ → Sistema emite ticket automáticamente
         ↓
         ¿Emisión exitosa con proveedor?
            SÍ → Estado: EMITIDA + Email automático
            NO → Estado: PENDIENTE (sin notificación a agente)
   NO → Estado: PENDIENTE + Requiere gestión del agente
```

**Flujo Emisión Manual (Pago Agencia):**
```
Usuario selecciona "Pago en Agencia"
       ↓
Reserva creada en estado: PENDIENTE
       ↓
Cliente recibe instrucciones para pagar en agencia
       ↓
Cliente acude a agencia física y paga (efectivo, datafono o transferencia)
       ↓
Agente NO recibe notificación automática
       ↓
Agente consulta reserva PENDIENTE en Admin (ve: vuelo, pasajeros, facturación, valor, proveedor, etc.)
       ↓
Agente confirma pago recibido
       ↓
Agente emite la reserva desde Admin
       ↓
Estado: EMITIDA + Email automático
```

**Estados posibles:**
- **EMITIDA** - Ticket emitido exitosamente con proveedor
- **PENDIENTE** - Requiere acción del agente (pago agencia, pago rechazado o emisión fallida)
- **CANCELADA** - Reserva cancelada por agente desde Admin

---

## ✅ VALIDACIONES CRÍTICAS

### **Validación 1: Autenticación (LOGIN)**
- **Cuándo:** Al intentar avanzar al checkout
- **Qué valida:** Usuario debe tener sesión activa para reservar
- **Mensaje de error:** Redirección automática a login
- **Comportamiento esperado:** 
  - 🔓 Sin login permitido: Home, Búsqueda, Disponibilidad
  - 🔒 Login obligatorio: Al seleccionar producto para checkout
  - 🔄 Post-login: Regresa al checkout manteniendo la selección previa

### **Validación 2: Disponibilidad del Vuelo**
- **Cuándo:** Al seleccionar vuelo y antes de checkout
- **Qué valida:** Vuelo sigue disponible al precio cotizado
- **Mensaje de error:** "Lo sentimos, este vuelo ya no está disponible. Por favor realiza una nueva búsqueda."
- **Comportamiento esperado:** Redirigir a resultados o búsqueda

### **Validación 3: Datos del Pasajero**
- **Cuándo:** En checkout
- **Qué valida:** Nombres coinciden con formato pasaporte/documento, edad coherente
- **Mensaje de error:** Específico por campo (ej: "El formato del nombre no es válido")
- **Comportamiento esperado:** Resaltar campo con error, no permitir continuar

### **Validación 4: Método de Pago**
- **Cuándo:** En checkout
- **Qué valida:** Usuario selecciona un método de pago válido
- **Mensaje de error:** "Debes seleccionar un método de pago"
- **Comportamiento esperado:** 
  - Si selecciona Tarjeta: Validar datos de tarjeta (número, CVV, fecha expiración)
  - Si selecciona Pago en Agencia: Mostrar instrucciones

### **Validación 5: Datos de Facturación**
- **Cuándo:** En checkout
- **Qué valida:** Datos completos de persona Natural o Jurídica
- **Mensaje de error:** Específico por campo faltante
- **Comportamiento esperado:** 
  - Persona Natural: Nombres, Apellidos, Tipo documento, Número documento
  - Persona Jurídica: Razón social, Tipo documento, NIT
  - Ambos: Dirección, Ciudad, Teléfono

### **Validación 6: Política de Equipaje**
- **Cuándo:** En disponibilidad, resumen y checkout
- **Qué valida:** Usuario está informado de la política de equipaje incluida (según proveedor)
- **Mensaje de error:** N/A (informativo)
- **Comportamiento esperado:** 
  - Mostrar claramente equipaje incluido según información del proveedor
  - NO permitir agregar equipaje adicional
  - Información puede variar según aerolínea y proveedor

---

## 🎯 CASOS DE PRUEBA TIPO

### **Formato de título:**
```
[CCOP] Vuelos - {Escenario} - {Proveedor} - {Variante}
```

### **Ejemplos:**

**Caso positivo básico:**
```
[CCOP] Vuelos - Compra exitosa ida - Netactica - 1 adulto nacional - Pago Tarjeta
[CCOP] Vuelos - Compra exitosa ida y vuelta - Sabre Aggregator - 2 adultos internacional - Pago Tarjeta
[CCOP] Vuelos - Compra exitosa ida - Netactica - 1 adulto nacional - Pago Agencia
```

**Caso con variantes:**
```
[CCOP] Vuelos - Compra con seguro cancelación - Netactica - 1 adulto - Pago Tarjeta
[CCOP] Vuelos - Compra múltiples pasajeros - Sabre Aggregator - 2 adultos + 1 niño - Pago Tarjeta
[CCOP] Vuelos - Emisión manual agente - Netactica - 1 adulto - Pago Agencia
```

**Caso negativo:**
```
[CCOP] Vuelos - Validación pago tarjeta rechazado - Netactica
[CCOP] Vuelos - Validación emisión fallida - Sabre Aggregator
[CCOP] Vuelos - Validación autenticación sin login - Cualquier proveedor
[CCOP] Vuelos - Validación vuelo no disponible - Netactica
```

---

## 📝 TEMPLATE DE CASO DE PRUEBA

### **Título:**
```
[CCOP] Vuelos - Compra exitosa ida y vuelta - Netactica - 1 adulto nacional - Pago Tarjeta
```

### **Pasos:**
```
1. **PRECONDICIONES:**
   - Usuario registrado en portal Consolidación COP
   - Tarjeta de crédito válida disponible (o preparado para pago en agencia)
   - Framework: Angular
   - **NOTA QA:** Reservas en ambiente test/demo deben cancelarse el mismo día antes de las 12 de la noche para evitar emisión oficial ante aerolínea y costos asociados

2. **PASO:** Ingresar a Home de Consolidación COP
   - **RESULTADO ESPERADO:** Se muestra Home del portal

3. **PASO:** [OPCIONAL] Iniciar sesión desde el Home:
   - Usuario: usuario@test.com
   - Contraseña: ********
   - **RESULTADO ESPERADO:** Login exitoso, usuario autenticado (NO pedirá login nuevamente en checkout)

4. **PASO:** Ingresar a sección Vuelos
   - **RESULTADO ESPERADO:** Se muestra formulario de búsqueda con campos obligatorios (NO requiere login)

5. **PASO:** Completar búsqueda con:
   - Origen: Bogotá (BOG)
   - Destino: Miami (MIA) [VUELO INTERNACIONAL para ILS]
   - Fecha ida: [Fecha +7 días]
   - Fecha vuelta: [Fecha +14 días]
   - Pasajeros: 1 adulto
   - **RESULTADO ESPERADO:** Se muestran resultados de vuelos disponibles (Aggregator Netactica, Aggregator Sabre/Sabre NDC, Sabre EDIFACT)

6. **PASO:** Seleccionar vuelo de ida:
   - Aerolínea: [Aerolínea disponible]
   - Horario: [Horario disponible]
   - Precio: [X] COP (incluyendo fees si aplican)
   - **RESULTADO ESPERADO:** Vuelo de ida se agrega al itinerario

7. **PASO:** Seleccionar vuelo de vuelta:
   - Aerolínea: [Aerolínea disponible]
   - Horario: [Horario disponible]
   - Precio: [Y] COP (incluyendo fees si aplican)
   - **RESULTADO ESPERADO:** Se muestra resumen completo del itinerario (ida + vuelta) con desglose de tarifas y fees (si aplican)

8. **PASO:** Hacer clic en "Continuar" o "Reservar"
   - **RESULTADO ESPERADO:** 
     - Si NO está autenticado: Sistema redirige a LOGIN
     - Si YA está autenticado (login desde home): Ir directamente a checkout

9. **PASO:** [SI NO ESTÁ AUTENTICADO] Iniciar sesión:
   - Usuario: usuario@test.com
   - Contraseña: ********
   - **RESULTADO ESPERADO:** Login exitoso, sistema regresa al checkout manteniendo la selección de vuelos previa

10. **PASO:** En checkout, completar datos del pasajero:
    - Nombre: Juan
    - Apellido: Pérez
    - Tipo de documento: Pasaporte
    - Documento: AB123456
    - Fecha nacimiento: 01/01/1990
    - Nacionalidad: Colombiana
    - Email: juan.perez@email.com
    - Teléfono: +57 300 1234567
    - **RESULTADO ESPERADO:** Todos los campos se validan correctamente

11. **PASO:** Completar datos de facturación (Persona Natural):
    - Nombres: Juan
    - Apellidos: Pérez García
    - Tipo de documento: Cédula de Ciudadanía
    - Número de documento: 1234567890
    - Dirección: Calle 123 #45-67
    - Ciudad: Bogotá
    - Teléfono: +57 300 1234567
    - **RESULTADO ESPERADO:** Datos de facturación validados

12. **PASO:** [VUELO INTERNACIONAL] Agregar seguro de cancelación ILS (AssistViaje):
    - Verificar que el pasajero tiene menos de 74 años
    - Seleccionar checkbox "Agregar seguro ILS"
    - **RESULTADO ESPERADO:** 
      - Precio total se actualiza con el costo del seguro (por pasajero)
      - Sistema valida edad del pasajero (<74 años)

13. **PASO:** Seleccionar método de pago "Tarjeta de Crédito/Débito"
    - **RESULTADO ESPERADO:** Se muestra formulario de datos de tarjeta

14. **PASO:** Ingresar datos completos de tarjeta de crédito:
    - Nombre del titular: Juan
    - Apellido del titular: Pérez
    - Tipo de documento del titular: Cédula de Ciudadanía
    - Número de documento del titular: 1234567890
    - Número de tarjeta: 4111111111111111
    - Mes de expiración: 12
    - Año de expiración: 27
    - CVV: 123
    - **RESULTADO ESPERADO:** Datos se validan correctamente

15. **PASO:** Aceptar Habeas Data
    - **RESULTADO ESPERADO:** Checkbox Habeas Data marcado

16. **PASO:** Aceptar Términos y Condiciones
    - **RESULTADO ESPERADO:** Checkbox T&C marcado

17. **PASO:** Confirmar compra
    - **RESULTADO ESPERADO:** 
      - Se procesa pago en pasarela PlacetoPay
      - Pago APROBADO
      - Sistema emite ticket automáticamente
      - Estado de reserva: EMITIDA
      - Se muestra pantalla de confirmación:
        - **SI tiene seguro ILS:** Pantalla especial de confirmación con información del seguro
        - **SI NO tiene seguro ILS:** Pantalla estándar de confirmación de marketplace
      - PNR generado
      - Se envía email de confirmación a juan.perez@email.com
      - Reserva visible en "Mis Reservas"

18. **PASO:** Validar en Admin Consolidación COP que la reserva:
    - Estado: EMITIDA
    - Proveedor: [Aggregator Netactica / Aggregator Sabre (Sabre NDC) / Sabre EDIFACT]
    - Itinerario: BOG-MIA (ida) / MIA-BOG (vuelta)
    - Pasajero: Juan Pérez - Doc AB123456
    - Monto: [CANTIDAD] COP (incluyendo fees si aplican)
    - PNR generado correctamente
    - Método de pago: Tarjeta de Crédito
    - Seguro ILS (AssistViaje): Sí
    - **RESULTADO ESPERADO:** Toda la información es correcta y trazable

19. **PASO:** [OBLIGATORIO QA] Cancelar reserva antes de las 12 de la noche:
    - **Para Sabre EDIFACT:**
      1. Cancelar tiquetes primero
      2. Luego cancelar la reserva
      3. Admin se sincroniza con Sabre según credenciales configuradas:
         - Credenciales de test → Sabre Red 360 CERT
         - Credenciales productivas → Sabre Red 360
    - **Para Aggregator Sabre (Sabre NDC):**
      1. Cancelar desde Admin
      2. Admin se sincroniza con Sabre según credenciales configuradas:
         - Credenciales de test → Sabre Red 360 CERT
         - Credenciales productivas → Sabre Red 360
    - **Para Aggregator Netactica:**
      1. Cancelar desde Admin
      2. Admin se sincroniza con Netactica
    - **RESULTADO ESPERADO:** 
      - Reserva cancelada en Admin
      - Reserva cancelada en proveedor correspondiente
      - Estado: CANCELADA
    - **NOTA:** 
      - Si no se cancela antes de las 12 de la noche, se emite oficialmente ante la aerolínea y genera costos
      - En ambientes test/demo: La sincronización con Sabre depende de las credenciales configuradas en el ambiente
```

---

## 🚨 CASOS EDGE Y ERRORES COMUNES

### **Error 1: Pago con Tarjeta Rechazado**
- **Escenario:** Banco rechaza la transacción con tarjeta
- **Causa:** Fondos insuficientes, tarjeta bloqueada, datos incorrectos
- **Estado resultante:** PENDIENTE
- **Mensaje esperado:** "Transacción rechazada. Por favor verifica los datos de tu tarjeta o selecciona otro método de pago."
- **Acción QA:** 
  - Validar que reserva queda en estado PENDIENTE
  - Validar que NO se permite reintento de pago
  - Validar que NO se notifica al agente

### **Error 2: Vuelo No Disponible**
- **Escenario:** Vuelo cotizado se agota antes de confirmar compra
- **Causa:** Otro usuario compró el último asiento
- **Mensaje esperado:** "Lo sentimos, este vuelo ya no está disponible. Por favor realiza una nueva búsqueda."
- **Acción QA:** Validar que redirige a resultados y no pierde filtros aplicados

### **Error 3: Datos del Pasajero Inválidos**
- **Escenario:** Usuario ingresa documento con formato incorrecto
- **Causa:** Formato no cumple validación (letras en campo numérico, etc.)
- **Mensaje esperado:** "El formato del documento no es válido"
- **Acción QA:** Validar que resalta el campo en rojo y muestra mensaje específico

### **Error 4: Emisión Fallida con Proveedor**
- **Escenario:** Pago aprobado pero endpoint del proveedor falla al emitir
- **Causa:** Problema de conectividad, timeout, error del proveedor
- **Estado resultante:** PENDIENTE
- **Mensaje esperado:** "Tu pago fue procesado exitosamente. Tu reserva está en proceso de emisión. Recibirás un email cuando esté confirmada."
- **Acción QA:** 
  - Validar que reserva queda en estado PENDIENTE
  - Validar que NO se notifica al agente
  - Validar que NO hay reintento automático
  - Validar que agente puede reintentar emisión desde Admin

### **Error 5: Pago en Agencia Pendiente**
- **Escenario:** Cliente selecciona pago en agencia pero no acude a pagar
- **Causa:** Cliente cambia de opinión o no puede acudir
- **Estado resultante:** PENDIENTE
- **Mensaje esperado:** Instrucciones para acudir a agencia física
- **Acción QA:** 
  - Validar que reserva queda en estado PENDIENTE
  - Validar que NO hay expiración automática
  - Validar que agente debe cancelar manualmente si cliente no paga

---

## 🔍 PARTICULARIDADES POR PROVEEDOR

### **AGGREGATOR NETACTICA**
- **Tecnología:** API REST
- **Particularidad 1:** Consolidador de múltiples aerolíneas
- **Particularidad 2:** Búsqueda en tiempo real
- **Particularidad 3:** [PENDIENTE VALIDAR - ej: Tiempos de respuesta, formatos específicos, políticas de equipaje]

### **AGGREGATOR SABRE**
- **Tecnología:** API REST - GDS Global
- **Particularidad 1:** Sistema GDS con amplia cobertura internacional
- **Particularidad 2:** Múltiples aerolíneas disponibles
- **Particularidad 3:** [PENDIENTE VALIDAR - ej: Validaciones adicionales para vuelos internacionales]

### **SABRE EDIFACT**
- **Tecnología:** EDIFACT (Sistema tradicional)
- **Particularidad 1:** Requiere procesamiento de mensajes EDIFACT
- **Particularidad 2:** Formato estándar de la industria
- **Particularidad 3:** [PENDIENTE VALIDAR - ej: Tiempos de emisión, particularidades de formato]

**NOTA:** Las particularidades específicas de cada proveedor deben ser validadas con el equipo de desarrollo y documentadas antes de crear los casos de prueba detallados.

---

## 📊 MATRIZ DE CASOS RECOMENDADA

| Escenario | Proveedor | Variante | Método Pago | Prioridad | Complejidad |
|-----------|-----------|----------|--------------|-----------|-------------|
| Compra exitosa ida - Pago Tarjeta | Netactica | 1 adulto nacional | Tarjeta | Alta | Baja |
| Compra exitosa ida y vuelta - Pago Tarjeta | Sabre Aggregator | 1 adulto nacional | Tarjeta | Alta | Media |
| Compra exitosa - Pago Agencia | Netactica | 1 adulto nacional | Agencia | Alta | Media |
| Compra con múltiples pasajeros | Netactica | 2 adultos + 1 niño | Tarjeta | Alta | Media |
| Compra vuelo internacional | Sabre Aggregator | 1 adulto | Tarjeta | Alta | Media |
| Compra con seguro de cancelación ILS | Netactica | 1 adulto internacional | Tarjeta | Alta | Media |
| Validación autenticación (sin login) | Cualquier proveedor | Cualquiera | N/A | Alta | Baja |
| Validación pago tarjeta rechazado | Netactica | 1 adulto | Tarjeta | Alta | Media |
| Validación emisión fallida | Sabre Aggregator | 1 adulto | Tarjeta | Alta | Alta |
| Validación vuelo no disponible | Netactica | Cualquiera | Tarjeta | Media | Media |
| Validación datos facturación - Persona Natural | Netactica | 1 adulto | Tarjeta | Alta | Baja |
| Validación datos facturación - Persona Jurídica | Netactica | 1 adulto | Tarjeta | Alta | Baja |
| Validación reglas de pasajeros (niño solo) | Cualquier proveedor | 1 niño sin adulto | N/A | Alta | Baja |
| Validación máximo pasajeros por reserva | Cualquier proveedor | 6 adultos (excede límite) | N/A | Media | Baja |
| Vuelo con múltiples escalas | Sabre EDIFACT | 2+ escalas | Tarjeta | Media | Media |
| Cancelación por agente | Cualquier proveedor | Cualquier estado | N/A | Media | Media |
| Emisión manual desde Admin (pago agencia) | Netactica | 1 adulto | Agencia | Alta | Alta |

**Total casos recomendados:** 17 casos mínimos

---

## 🔗 REFERENCIAS

**Reglas comunes:**
- [CCOP_COMMON_RULES.md](../../../shared/Reglas Marketplace/CCOP_COMMON_RULES.md)
- [SHARED_QA_RULES.md](../../../shared/SHARED_QA_RULES.md)

**Agente especializado:**
- [CCOP_QA_Assistant.agent.md](../../../agents/CCOP_QA_Assistant.agent.md)

**Azure DevOps:**
- NO hay suite específica de "Vuelos" para CCOP
- Test Plan ID: Será proporcionado por QA cuando se requiera

---

## 📝 NOTAS DE IMPLEMENTACIÓN

**Estado:** ✅ EN CONFIGURACIÓN

**Información Confirmada:**
- ✅ Framework: Angular
- ✅ Proveedores: Aggregator Netactica, Aggregator Sabre (Sabre NDC), Sabre EDIFACT
- ✅ Modelo de pago: 100% Efectivo (Tarjeta o Agencia)
- ✅ Emisión: Automática (tarjeta) / Manual (agencia)
- ✅ Estados: EMITIDA, PENDIENTE, CANCELADA
- ✅ Fees: TA visible (opcional, configurable en Admin: fija o porcentual) + Fee Oculto (configurable en Admin: fijo o porcentual, solo si TA está activa)
- ✅ Seguro ILS (AssistViaje): Solo vuelos internacionales, por pasajero, no >74 años, tarifa retornada por AssistViaje según vuelo
- ✅ Pantalla confirmación con ILS: Reemplaza completamente la estándar (es otra plantilla)
- ✅ Pasarela de pago: PlacetoPay
- ✅ Datos tarjeta: Nombre, apellido, tipo doc, número doc, tarjeta, mes, año, CVV
- ✅ Habeas Data y Términos: Obligatorios antes de ejecutar reserva
- ✅ Login: Puede ser desde home (no pide login en checkout si ya está autenticado)
- ✅ Notificaciones: NO se notifica al agente (ni pagos fallidos, ni rechazados, ni emitidos, ni reservas pendientes)
- ✅ Pagos rechazados: NO permiten reintentos
- ✅ Emisión fallida: NO notifica al agente
- ✅ Admin - Emisión manual:
  - Agente NO recibe notificación de reservas pendientes
  - Cliente paga en agencia (efectivo, datafono, transferencia)
  - Agente ve toda la info: vuelo, pasajeros, facturación, valor, proveedor
  - Agente confirma pago y emite desde Admin
- ✅ Vuelos internacionales: Nacionalidad y Fecha expiración pasaporte obligatorios
- ✅ Azure DevOps: NO hay suite específica de Vuelos, NO hay planId predefinido (QA lo proporciona cuando lo requiera)
- ✅ Cancelación QA: Obligatoria antes de las 12 de la noche en test/demo
- ✅ Sincronización Admin:
  - Sabre EDIFACT/Aggregator Sabre:
    - Credenciales de test → Sabre Red 360 CERT
    - Credenciales productivas → Sabre Red 360
  - Aggregator Netactica → Netactica
- ✅ Pantallas del flujo: Home → Disponibilidad → Resumen de disponibilidad → Checkout → Confirmación
- ✅ Reglas de pasajeros:
  - Adultos: >12 años | Niños: 2-11 años | Infantes: <2 años
  - Niño NO puede viajar solo (requiere mínimo 1 adulto)
  - 1 adulto máximo con 2 niños y 1 infante
  - Máximo por reserva: 5 adultos + 4 niños y/o infantes
  - No hay restricciones especiales para infantes
  - No hay validaciones adicionales para infantes en checkout
- ✅ Equipaje:
  - Se muestra información según proveedor
  - NO hay opción de agregar equipaje adicional
  - Varía según aerolínea y proveedor
- ✅ Filtros disponibles: Precio, Escala, Equipaje, Horarios, Carrousel aerolíneas, Fechas Flexibles, Tendencia precios, Explorar Destinos
- ✅ Funcionalidades: Nueva búsqueda desde disponibilidad, Opciones avanzadas, Código promocional


**Última actualización:** 2026-02-03  
**Responsable:** QA Team CCOP
