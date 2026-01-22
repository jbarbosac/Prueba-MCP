# 🛫 CORPORATIVO USD - VUELOS

> Flujo End-to-End completo para reserva de vuelos corporativos en USD

---

## 📋 INFORMACIÓN GENERAL

**Portal:** CORPORATIVO USD  
**URL:** https://demo-corporativousd.smartlinks.dev  
**Producto:** Vuelos  
**Modelo:** B2B (Business to Business) - **SEMIAUTOMÁTICO**  
**Moneda:** USD (Dólares)  
**Prefijo:** `[CORP-USD]`  
**Cliente:** Empresas corporativas  
**Tipo de operación:** Transacciones manuales por asesor  

**Tecnología:**  
- Aggregators (NETACTICA, SABRE)
- SABRE EDIFACT

**Proveedores:**  
- **AGGREGATOR - NETACTICA** (sin dispersión de fondos)
- **AGGREGATOR - SABRE** (sin dispersión de fondos)
- **SABRE EDIFACT** (sin dispersión de fondos)

**⚠️ IMPORTANTE:** Todos los proveedores operan **SIN dispersión de fondos**

---

## 🎯 CARACTERÍSTICAS DEL PRODUCTO

### **Modelo de Negocio**

**CORPORATIVO USD es un modelo B2B SEMIAUTOMÁTICO enfocado en clientes corporativos:**

**⚠️ MODELO SEMIAUTOMÁTICO:**
- El **asesor/agente realiza las transacciones de manera MANUAL**
- No hay emisión automática de boletos
- Requiere intervención humana en todo el proceso

**FLUJO DE NEGOCIO:**

1. **Autenticación:** Login corporativo con credenciales empresariales
2. **Búsqueda:** Precios en USD, políticas corporativas aplicadas
3. **Selección:** Vuelos disponibles según acuerdos corporativos
4. **Checkout:** Facturación empresarial, centro de costos
5. **Pago:** Pago corporativo procesado (sin dispersión de fondos)
6. **Aprobación:** ⚠️ **OBLIGATORIO** - Aprobador asignado debe aprobar la reserva
7. **Emisión:** 👤 **MANUAL** - Asesor/Agente realiza la transacción manualmente después de aprobación
8. **Confirmación:** PNR generado, notificaciones enviadas

**DIFERENCIADORES DEL MODELO:**
- Modelo B2B para empresas corporativas
- Transacciones en USD exclusivamente
- Facturación empresarial con centro de costos
- Flujo de aprobación obligatorio (Simple o Serial)
- Emisión manual por Agente después de aprobación
- **RESTRICCIÓN:** Solo se permiten reservas para pasajeros **ADULTOS** (NO se aceptan niños ni infantes)
- Sin dispersión de fondos en todos los proveedores

---

## 🔄 FLUJO END-TO-END COMPLETO

### **PASO 1: LOGIN CORPORATIVO**

**Acción:**
```
1. Ingresar a la URL: https://demo-corporativousd.smartlinks.dev
2. Hacer clic en botón "Acceso Corporativo"
3. Ingresar credenciales corporativas:
   - Usuario corporativo
   - Contraseña
   - [Código de empresa si aplica]
4. Hacer clic en "Iniciar Sesión"
```

**Validaciones:**
- ✅ Redirección a página de inicio corporativa
- ✅ Nombre de empresa visible en header
- ✅ Permisos corporativos activos
- ✅ Centro de costos disponible (si aplica)

**Resultado Esperado:**
```html
<p>Usuario autenticado correctamente en portal corporativo</p>
<p>Empresa: [NOMBRE_EMPRESA]</p>
<p>Usuario: [NOMBRE_USUARIO]</p>
```

**Imágenes de referencia:**
```html
<img src="https://[DOMINIO]/images/CORPORATIVO/Login-CORP.png" alt="Login Corporativo" />
```

---

### **PASO 2: HOME - INICIAR BÚSQUEDA DE VUELOS**

**Acción:**
```
1. En el home, localizar el widget de "Vuelos Corporativos"
2. Completar formulario de búsqueda:
   - Origen: [CIUDAD_ORIGEN]
   - Destino: [CIUDAD_DESTINO]
   - Fecha ida: [FECHA_IDA]
   - Fecha regreso: [FECHA_REGRESO] (si aplica)
   - Pasajeros: [CANTIDAD] adultos
   - Clase: Económica/Ejecutiva
   - Centro de costos: [SELECCIONAR] (si aplica)
3. Hacer clic en "Buscar Vuelos"
```

**Validaciones:**
- ✅ Autocompletado de ciudades funciona
- ✅ Calendario permite seleccionar fechas futuras
- ✅ Contador de pasajeros funciona (1-9)
- ✅ Centro de costos se carga correctamente (si aplica)
- ✅ Validación de campos obligatorios

**Resultado Esperado:**
```html
<p>Búsqueda iniciada correctamente</p>
<p>Parámetros capturados:</p>
<ul>
  <li>Ruta: [ORIGEN] → [DESTINO]</li>
  <li>Fechas: [IDA] - [REGRESO]</li>
  <li>Pasajeros: [CANTIDAD]</li>
  <li>Clase: [CLASE]</li>
</ul>
```

**Imágenes de referencia:**
```html
<img src="https://[DOMINIO]/images/CORPORATIVO/Home-CORP.png" alt="Home Corporativo" />
<img src="https://[DOMINIO]/images/CORPORATIVO/Home-vuelos-CORP.png" alt="Widget Vuelos" />
```

---

### **PASO 3: DISPONIBILIDAD - RESULTADOS DE BÚSQUEDA**

**Acción:**
```
1. Esperar carga de resultados (loading)
2. Revisar lista de vuelos disponibles
3. Validar información de cada vuelo:
   - Aerolínea y número de vuelo
   - Horarios (salida/llegada)
   - Escalas
   - Precio en USD
   - Políticas corporativas aplicables
4. Aplicar filtros (si aplica):
   - Aerolínea preferida
   - Escalas
   - Rango de precio
   - Horarios
5. Seleccionar vuelo deseado
6. Hacer clic en "Seleccionar" o "Continuar"
```

**Validaciones:**
- ✅ Resultados se muestran correctamente
- ✅ Precios en USD
- ✅ Políticas corporativas visibles (si aplica)
- ✅ Filtros funcionan correctamente
- ✅ Información completa de cada vuelo
- ✅ No hay errores 500 o timeouts
- ✅ Manejo correcto si no hay resultados

**Resultado Esperado:**
```html
<p>Vuelo seleccionado correctamente:</p>
<ul>
  <li>Aerolínea: [NOMBRE]</li>
  <li>Vuelo: [NÚMERO]</li>
  <li>Precio: USD [MONTO]</li>
  <li>Escalas: [CANTIDAD]</li>
</ul>
```

**Imágenes de referencia:**
```html
<img src="https://[DOMINIO]/images/CORPORATIVO/Disponibilidad-vuelos-CORP.png" alt="Resultados de búsqueda" />
```

---

### **PASO 4: UPSELLING (SI APLICA)**

**Acción:**
```
1. Revisar opciones de upselling disponibles:
   - Equipaje adicional
   - Asientos preferenciales
   - Seguro de viaje
   - Asistencia al viajero
2. Seleccionar o rechazar opciones
3. Hacer clic en "Continuar"
```

**Validaciones:**
- ✅ Opciones de upselling se muestran correctamente
- ✅ Precios adicionales en USD
- ✅ Selección/deselección funciona
- ✅ Precio total se actualiza dinámicamente
- ✅ Políticas corporativas aplicables (si hay restricciones)

**Resultado Esperado:**
```html
<p>Opciones de upselling procesadas:</p>
<ul>
  <li>Equipaje adicional: [SÍ/NO]</li>
  <li>Asientos: [SÍ/NO]</li>
  <li>Seguro: [SÍ/NO]</li>
  <li>Precio adicional: USD [MONTO]</li>
</ul>
```

**Imágenes de referencia:**
```html
<img src="https://[DOMINIO]/images/CORPORATIVO/upsell-vuelos-CORP.png" alt="Opciones de upselling" />
```

---

### **PASO 5: RESUMEN DE RESERVA**

**Acción:**
```
1. Revisar resumen completo de la reserva:
   - Información del vuelo (ida/regreso)
   - Pasajeros
   - Precio total en USD
   - Centro de costos asignado
   - Políticas aplicables
2. Validar que toda la información es correcta
3. Hacer clic en "Continuar al Checkout"
```

**Validaciones:**
- ✅ Información de vuelos completa y correcta
- ✅ Precio total coincide (vuelo + upselling)
- ✅ Centro de costos correcto
- ✅ Desglose de precios visible
- ✅ Políticas corporativas aplicadas

**Resultado Esperado:**
```html
<p>Resumen validado correctamente:</p>
<ul>
  <li>Vuelo ida: [DETALLE]</li>
  <li>Vuelo regreso: [DETALLE]</li>
  <li>Precio total: USD [MONTO]</li>
  <li>Centro de costos: [CÓDIGO]</li>
</ul>
```

**Imágenes de referencia:**
```html
<img src="https://[DOMINIO]/images/CORPORATIVO/Resumen-vuelos-CORP.png" alt="Resumen de reserva" />
```

---

### **PASO 6: CHECKOUT - DATOS DE PASAJEROS**

**Acción:**
```
1. Completar datos de pasajeros:
   - **Si usuario es ORGANIZADOR:**
     - Opción "Invitar pasajero externo" (si configuración está ACTIVA)
     - Lista desplegable de empleados de la empresa (siempre disponible)
   - Nombre completo (según pasaporte)
   - Tipo y número de documento
   - Fecha de nacimiento
   - Nacionalidad
   - Género
   - [Programa de viajero frecuente si aplica]
2. Completar datos de contacto:
   - Email corporativo
   - Teléfono de contacto
3. Completar datos de facturación:
   - Nombre/Razón social de la empresa
   - RUC/NIT/Tax ID
   - Dirección fiscal
   - Centro de costos:
     - Si configuración "Restringir cambio" ACTIVA: Solo lectura (centro asignado)
     - Si configuración "Restringir cambio" INACTIVA: Lista desplegable de centros disponibles
4. **Si NO cumple con Políticas de Reservas configuradas:**
   - Campo obligatorio "Justificación de excepción" aparece
   - Usuario DEBE escribir razón/argumento de por qué reserva sin cumplir políticas
   - Campo de texto con validación (mínimo de caracteres)
5. Aceptar términos y condiciones
6. Hacer clic en "Proceder al Pago"
```

**Validaciones:**
- ✅ Campos obligatorios validados
- ✅ Formato de documento correcto
- ✅ Fechas válidas (mayoría de edad para conductor, etc.)
- ✅ Email con formato válido
- ✅ Datos de facturación corporativa completos
- ✅ Centro de costos válido
- ✅ **Configuración "Restringir cambio de centros de costo":**
  - **Si ACTIVA:** Campo solo lectura, muestra centro de costos asignado, usuario NO puede cambiar
  - **Si INACTIVA:** Lista desplegable funcional, usuario puede seleccionar otro centro de costos autorizado
- ✅ **Política de Reservas (si configurada por la empresa):**
  - Sistema valida si la reserva cumple con las políticas definidas
  - **Si NO CUMPLE políticas:** Campo "Justificación de excepción" es OBLIGATORIO
  - Usuario debe escribir razón/argumento válido (mínimo de caracteres configurado)
  - Sistema NO permite continuar sin justificación completa
  - Justificación queda registrada en trazabilidad para auditoría
- ✅ Términos aceptados
- ✅ **Si usuario es ORGANIZADOR:**
  - **Configuración "Permitir invitar viajeros externos" ACTIVA:** Puede invitar pasajeros externos (ingresar datos manualmente) O seleccionar de lista de empleados
  - **Configuración "Permitir invitar viajeros externos" INACTIVA:** SOLO puede seleccionar pasajeros de lista desplegable de empleados de la empresa
- ✅ **Aprobador(es) asignado(s) visible(s)** en el formulario:
  - **Si "Restringir cambio" ACTIVO:** Solo lectura, muestra aprobador(es) asignado(s)
  - **Si "Restringir cambio" INACTIVO:** Lista desplegable con aprobadores disponibles para seleccionar

**Resultado Esperado:**
```html
<p>Datos de pasajeros capturados correctamente:</p>
<ul>
  <li>Pasajero 1: [NOMBRE]</li>
  <li>Documento: [TIPO] [NÚMERO]</li>
  <li>Email: [EMAIL_CORPORATIVO]</li>
  <li>Facturación: [EMPRESA]</li>
  <li>Centro costos: [CÓDIGO]</li>
</ul>
```

**Imágenes de referencia:**
```html
<img src="https://[DOMINIO]/images/CORPORATIVO/Checkout-vuelos-CORP.png" alt="Checkout" />
```

---

### **PASO 7: PAGO CORPORATIVO**

**Configuración de Pago:**
- **Tarjetas aceptadas:** Todas las franquicias (Visa, Mastercard, American Express, Diners, etc.)
- **Límite de monto:** Sin límite de monto por transacción
- **Autorización especial:** NO requerida para montos altos
- **Validación CVV:** NO obligatoria (opcional)

**Acción:**
```
1. Revisar método de pago corporativo:
   - Tarjeta corporativa (todas las franquicias aceptadas)
   - Sin restricción de monto
   - Sin autorización adicional requerida
2. Completar datos de pago:
   - Número de tarjeta corporativa
   - Fecha de vencimiento
   - CVV (opcional, no obligatorio)
   - Nombre del titular
3. Revisar precio final en USD (sin límite)
4. Hacer clic en "Confirmar Pago"
5. Esperar procesamiento de pago
```

**Validaciones:**
- ✅ Todas las franquicias de tarjetas aceptadas
- ✅ Sin límite de monto de transacción
- ✅ NO requiere autorización especial para montos altos
- ✅ CVV opcional (no bloqueante si no se proporciona)
- ✅ Datos de tarjeta válidos (número, vencimiento, titular)
- ✅ Precio final correcto en USD
- ✅ Proceso de pago seguro (HTTPS)
- ✅ Feedback de procesamiento (loading, progress)

**Resultado Esperado:**
```html
<p>Pago procesado exitosamente:</p>
<ul>
  <li>Método: Tarjeta Corporativa [FRANQUICIA]</li>
  <li>Monto: USD [TOTAL] (sin límite)</li>
  <li>Estado: APROBADO</li>
  <li>Código transacción: [CÓDIGO]</li>
</ul>
```

**Imágenes de referencia:**
```html
<img src="https://[DOMINIO]/images/CORPORATIVO/Pago-CORP.png" alt="Proceso de pago" />
```

---

### **PASO 8: CONFIRMACIÓN DE RESERVA**

**Acción:**
```
1. Esperar redirección a página de confirmación
2. Validar información mostrada:
   - PNR (Código de reserva)
   - Datos del vuelo
   - Pasajeros
   - Precio pagado en USD
   - Centro de costos
   - Estado de la reserva
3. Validar notificaciones enviadas:
   - Email al viajero
   - Email al aprobador corporativo (si aplica)
   - Email de facturación
4. [OPCIONAL] Descargar/imprimir comprobante
```

**Validaciones:**
- ✅ PNR generado correctamente
- ✅ Información de vuelo completa
- ✅ Estado de reserva: CONFIRMADA
- ✅ Email de confirmación recibido (viajero)
- ✅ Email de notificación recibido (aprobador)
- ✅ Email de facturación recibido (empresa)
- ✅ Comprobante descargable (PDF)

**Resultado Esperado:**
```html
<p>✅ RESERVA CONFIRMADA EXITOSAMENTE</p>
<ul>
  <li>PNR: [CÓDIGO_PNR]</li>
  <li>Estado: CONFIRMADA</li>
  <li>Vuelo: [DETALLE_COMPLETO]</li>
  <li>Pasajero: [NOMBRE]</li>
  <li>Total pagado: USD [MONTO]</li>
  <li>Centro costos: [CÓDIGO]</li>
  <li>Fecha de reserva: [FECHA_HORA]</li>
</ul>
```

**Imágenes de referencia:**
```html
<img src="https://[DOMINIO]/images/CORPORATIVO/Confirmacion-vuelos-CORP.png" alt="Confirmación" />
```

---

### **PASO 9: VALIDACIÓN EN ADMIN (SI APLICA)**

**Acción:**
```
1. Ingresar al panel de administración corporativa
2. Buscar reserva por PNR o centro de costos
3. Validar estado de la reserva
4. Validar información completa
5. Validar trazabilidad de aprobaciones (si aplica)
```

**Validaciones:**
- ✅ Reserva visible en admin
- ✅ Estado correcto
- ✅ Información completa y correcta
- ✅ Centro de costos asociado
- ✅ Historial de aprobaciones (si aplica)
- ✅ Facturación correcta

**Resultado Esperado:**
```html
<p>Reserva encontrada en panel admin:</p>
<ul>
  <li>PNR: [CÓDIGO]</li>
  <li>Estado: CONFIRMADA</li>
  <li>Centro costos: [CÓDIGO]</li>
  <li>Aprobador: [NOMBRE] (si aplica)</li>
  <li>Factura: [NÚMERO]</li>
</ul>
```

**Imágenes de referencia:**
```html
<img src="https://[DOMINIO]/images/CORPORATIVO/Admin-CORP.png" alt="Panel Admin" />
<img src="https://[DOMINIO]/images/CORPORATIVO/Reserva-CORP.png" alt="Detalle Reserva" />
```

---

## 📊 ESCENARIOS DE PRUEBA

### **ESCENARIOS BÁSICOS**

#### **✈️ Vuelo Ida y Vuelta - 1 Adulto**
```
[CORP-USD] Vuelos - Ida y vuelta - [Proveedor] - 1 adulto
```
- Ruta nacional o internacional
- Fechas futuras
- 1 pasajero adulto
- Clase económica
- Sin escalas preferido

#### **✈️ Vuelo Solo Ida - 1 Adulto**
```
[CORP-USD] Vuelos - Solo ida - [Proveedor] - 1 adulto
```
- Ruta nacional o internacional
- Fecha futura
- 1 pasajero adulto
- Clase económica

#### **✈️ Vuelo Multidestino - 1 Adulto**
```
[CORP-USD] Vuelos - Multidestino - [Proveedor] - 1 adulto
```
- 3 o más tramos
- Fechas secuenciales
- 1 pasajero adulto

---

### **ESCENARIOS CON VARIANTES**

#### **✈️ Múltiples Pasajeros**
```
[CORP-USD] Vuelos - Ida y vuelta - [Proveedor] - 2 adultos
[CORP-USD] Vuelos - Ida y vuelta - [Proveedor] - 3 adultos
[CORP-USD] Vuelos - Ida y vuelta - [Proveedor] - 5 adultos
```

#### **✈️ Diferentes Clases**
```
[CORP-USD] Vuelos - Ida y vuelta - [Proveedor] - Clase ejecutiva
[CORP-USD] Vuelos - Ida y vuelta - [Proveedor] - Clase premium
```

#### **✈️ Con Equipaje Adicional**
```
[CORP-USD] Vuelos - Ida y vuelta - [Proveedor] - 1 adulto + equipaje
```

#### **✈️ Con Escalas**
```
[CORP-USD] Vuelos - Ida y vuelta - [Proveedor] - 1 escala
[CORP-USD] Vuelos - Ida y vuelta - [Proveedor] - 2 escalas
```

---

### **ESCENARIOS POR PROVEEDOR**

**Proveedores disponibles en CORPORATIVO USD:**

#### **AGGREGATOR - NETACTICA**
```
[CORP-USD] Vuelos - Ida y vuelta - AGGREGATOR-NETACTICA - 1 adulto
[CORP-USD] Vuelos - Ida y vuelta - AGGREGATOR-NETACTICA - 2 adultos
[CORP-USD] Vuelos - Solo ida - AGGREGATOR-NETACTICA - 1 adulto
```

#### **AGGREGATOR - SABRE**
```
[CORP-USD] Vuelos - Ida y vuelta - AGGREGATOR-SABRE - 1 adulto
[CORP-USD] Vuelos - Ida y vuelta - AGGREGATOR-SABRE - 2 adultos
[CORP-USD] Vuelos - Multidestino - AGGREGATOR-SABRE - 1 adulto
```

#### **SABRE EDIFACT**
```
[CORP-USD] Vuelos - Ida y vuelta - SABRE-EDIFACT - 1 adulto
[CORP-USD] Vuelos - Ida y vuelta - SABRE-EDIFACT - 3 adultos
[CORP-USD] Vuelos - Clase ejecutiva - SABRE-EDIFACT - 1 adulto
```

**⚠️ NOTA IMPORTANTE:**
- Todos los proveedores operan **sin dispersión de fondos**
- Emisión es **siempre manual** por agente después de aprobación
- Proceso de aprobación es **obligatorio** para todos los proveedores

---

## 🚨 VALIDACIONES CRÍTICAS

### **1. AUTENTICACIÓN CORPORATIVA**
- ✅ Solo usuarios corporativos autorizados
- ✅ Permisos según rol (viajero, aprobador, admin)
- ✅ Centro de costos válido para el usuario
- ✅ Políticas corporativas activas
- ✅ Flujo de aprobación asignado correctamente al usuario (Simple O Serial, no ambos)

### **2. BÚSQUEDA Y DISPONIBILIDAD**
- ✅ Precios SIEMPRE en USD
- ✅ Políticas corporativas aplicadas (restricciones de aerolíneas, clases, etc.)
- ✅ Solo vuelos corporativos disponibles
- ✅ Manejo correcto de errores (sin resultados, timeout)

### **3. CHECKOUT Y PAGO**
- ✅ Datos de pasajeros completos y válidos
- ✅ Facturación a nombre de la empresa
- ✅ Centro de costos obligatorio
- ✅ **Política de Reservas:** Si NO cumple políticas corporativas, justificación obligatoria y válida
- ✅ Método de pago corporativo funcional
- ✅ Términos y condiciones corporativos aceptados

### **4. APROBACIÓN (CRÍTICO - OBLIGATORIO)**

**⚠️ TIPOS DE APROBACIÓN (UN SOLO TIPO POR USUARIO):**

**Validaciones comunes para ambos tipos:**
- ✅ Estado PENDIENTE DE APROBACIÓN después del pago
- ✅ Notificación inmediata al(los) aprobador(es) asignado(s)
- ✅ Aprobador puede ver todos los detalles de la reserva
- ✅ Botones APROBAR/RECHAZAR funcionales
- ✅ Motivo obligatorio si rechaza
- ✅ Cambio de estado correcto según decisión
- ✅ Notificaciones enviadas según resultado
- ✅ Usuario NO puede cancelar reserva pendiente
- ✅ Emisión BLOQUEADA hasta aprobación completa

**⚠️ APROBACIÓN SERIAL (Múltiples Aprobadores):**

- ✅ **NO hay límite** de cantidad de aprobadores en la cadena
- ✅ TODOS los aprobadores deben aprobar (orden secuencial)
- ✅ UN SOLO RECHAZO bloquea emisión inmediatamente
- ✅ Estado muestra progreso: "PARCIALMENTE APROBADA (X de N)"
- ✅ Trazabilidad completa de cada aprobador (orden, fecha, comentario)
- ✅ Aprobador siguiente recibe notificación solo si anterior aprobó
- ✅ Si uno rechaza: proceso se detiene, NO se notifica a siguientes
- ✅ Solo después de TODAS las aprobaciones → AGENTE puede emitir
- ✅ Cada aprobador **NO puede delegar** su aprobación
- ✅ Cada aprobador **NO puede solicitar cambios** sin rechazar
- ✅ Solo dos acciones posibles por aprobador: **APROBAR** o **RECHAZAR**

**⚠️ APROBACIÓN SIMPLE (Un Aprobador):**

- ✅ Una aprobación suficiente para proceder con emisión
- ✅ Proceso directo sin cadena de aprobadores
- ✅ Decisión inmediata (aprobar/rechazar)
- ✅ Trazabilidad del aprobador único
- ✅ Aprobador **NO puede delegar** a otro
- ✅ Aprobador **NO puede solicitar cambios** sin rechazar
- ✅ Solo dos acciones posibles: **APROBAR** o **RECHAZAR**

### **5. EMISIÓN (CRÍTICO - MANUAL - MODELO SEMIAUTOMÁTICO)**

**⚠️ PROCESO COMPLETAMENTE MANUAL POR AGENTE:**
- ✅ Emisión SOLO posible si estado es APROBADA (todos los aprobadores aprobaron)
- ✅ **Agente** recibe notificación de reservas aprobadas
- ✅ **Agente** ingresa al administrador y valida aprobaciones
- ✅ **Agente** hace clic en botón "Emitir"
- ✅ **Agente** selecciona "Tarjeta corporativa asociada a la empresa"
- ✅ **Agente** selecciona tarjeta específica de la empresa
- ✅ **Agente** hace clic en "Desencriptar tarjeta"
- ✅ Sistema muestra datos completos de tarjeta (número, vencimiento, CVV, titular)
- ✅ **Agente** ingresa a plataforma del proveedor
- ✅ **Agente** ingresa datos de tarjeta manualmente en plataforma del proveedor
- ✅ **Agente** envía pago a aerolínea/comercio
- ✅ **Agente** espera confirmación de pago exitoso
- ✅ **Sin dispersión de fondos:** Agente emite en CASH (CORPORATIVO USD)
- ✅ **Con dispersión de fondos:** Agente emite con TC (otros modelos)
- ✅ Número(s) de ticket generados correctamente
- ✅ Estado cambia a EMITIDA
- ✅ Trazabilidad completa: agente, fecha/hora, tarjeta utilizada
- ✅ Notificaciones enviadas: viajero, aprobador(es), contabilidad
- ✅ **NO hay emisión automática** - requiere intervención manual completa del agente

### **6. CONFIRMACIÓN FINAL Y NOTIFICACIONES**

- ✅ PNR generado correctamente
- ✅ Reserva visible en sistema con estado correcto
- ✅ Notificaciones enviadas en cada etapa:
  - ✉️ **Viajero:**
    * Creación: Template de Confirmación de Reserva (estado PENDIENTE)
    * Aprobación: Template de Confirmación de Reserva actualizado (estado APROBADA)
    * Emisión: **Template de Emisión de Reserva** con PNR y e-ticket
  - ✉️ **Aprobador(es):**
    * Solicitud de aprobación (con link para aprobar/rechazar)
    * Confirmación de emisión (notificación simple)
  - ✉️ **Agente:**
    * Autorización para emitir (después de aprobación completa)
  - ✉️ **Facturación/Contabilidad:**
    * Factura generada (registro de gasto corporativo)
- ✅ Comprobante descargable
- ✅ Trazabilidad completa en admin
- ✅ Historial de toda la operación

---

## 🎯 CRITERIOS DE ACEPTACIÓN ESTÁNDAR

**Template para Considerations:**

```html
<p><strong>Criterios de Aceptación:</strong></p>
<ul>
  <li><strong>Autenticación:</strong> Login corporativo exitoso con credenciales válidas</li>
  <li><strong>Búsqueda:</strong> Resultados se muestran correctamente en USD con políticas corporativas aplicadas</li>
  <li><strong>Disponibilidad:</strong> Vuelos corporativos disponibles, precios correctos, filtros funcionan</li>
  <li><strong>Selección:</strong> Vuelo seleccionado correctamente, información completa</li>
  <li><strong>Upselling:</strong> Opciones adicionales funcionan, precio se actualiza</li>
  <li><strong>Checkout:</strong> Datos completos según tipo de usuario, validaciones OK, centro de costos asignado. 
    <ul>
      <li>Si ORGANIZADOR: validar configuración "Permitir invitar viajeros externos" (activa → puede invitar externos O seleccionar empleados, inactiva → solo empleados de lista)</li>
      <li>Aprobador(es) visible(s) en formulario. Validar configuración "Restringir cambio de aprobador" (activa → solo lectura, inactiva → lista desplegable funcional)</li>
      <li>Centro de costos: Validar configuración "Restringir cambio de centros de costo" (activa → solo lectura con centro asignado, inactiva → lista desplegable con centros autorizados)</li>
      <li>Política de Reservas: Si NO cumple políticas → campo "Justificación de excepción" obligatorio, validar mínimo de caracteres y que sea específico</li>
    </ul>
  </li>
  <li><strong>Pago:</strong> Pago corporativo procesado exitosamente
    <ul>
      <li>Todas las franquicias de tarjetas aceptadas (Visa, Mastercard, Amex, Diners, etc.)</li>
      <li>Sin límite de monto por transacción</li>
      <li>NO requiere autorización especial para montos altos</li>
      <li>CVV opcional (no obligatorio)</li>
    </ul>
  </li>
  <li><strong>Estado Post-Pago:</strong> Reserva en PENDIENTE DE APROBACIÓN, notificación enviada al(los) aprobador(es)</li>
  <li><strong>Aprobación:</strong> Usuario tiene UN tipo de flujo (Simple O Serial):
    <ul>
      <li>Serial: Todos los aprobadores aprueban en orden, cualquier rechazo bloquea emisión</li>
      <li>Simple: Aprobador único aprueba, estado cambia a APROBADA</li>
    </ul>
  </li>
  <li><strong>Emisión:</strong> Agente emite boleto SOLO después de aprobación completa, ticket generado correctamente</li>
  <li><strong>Confirmación Final:</strong> Estado EMITIDA, notificaciones enviadas, comprobante disponible</li>
  <li><strong>Admin:</strong> Reserva visible en panel con trazabilidad completa (aprobación + emisión)</li>
</ul>
```

---

## 📧 SISTEMA DE NOTIFICACIONES

### **Configuración General**

**Destinatario principal:** Correo electrónico registrado en el perfil del viajero  
**Tipo de envío:** Automático (sin intervención manual)  
**Obligatoriedad:** El viajero DEBE tener email registrado en su perfil  
**Modificación:** Email NO puede cambiarse durante el proceso de reserva  

### **Templates de Notificación**

#### **Template 1: Confirmación de Reserva**

**Trigger de envío:**
- Reserva creada exitosamente después del checkout
- Estado: PENDIENTE DE APROBACIÓN o APROBADA

**Destinatarios:**
- ✉️ **Viajero:** Email registrado en perfil
- ✉️ **Aprobador(es):** Si aplica flujo de aprobación (Simple o Serial)

**Contenido del email:**
- Código de reserva interno del sistema
- Detalles del vuelo:
  * Origen y destino
  * Fechas y horarios
  * Aerolínea(s)
  * Número(s) de vuelo
- Información de pasajero(s)
- Estado actual: PENDIENTE DE APROBACIÓN o APROBADA
- Próximos pasos según estado:
  * Si PENDIENTE: "Su reserva está en espera de aprobación"
  * Si APROBADA: "Su reserva ha sido aprobada y será emitida por nuestro equipo"
- Monto total en USD
- Centro de costos asignado

**Momento de envío:**
- Inmediatamente después del checkout (estado PENDIENTE)
- Al cambiar a estado APROBADA (después de aprobación)

---

#### **Template 2: Emisión de Reserva (Boleto Electrónico)**

**Trigger de envío:**
- Reserva emitida exitosamente por el Agente
- Estado: EMITIDA

**Destinatario:**
- ✉️ **Viajero:** Email registrado en perfil (ÚNICO destinatario de este template)

**Contenido del email:**
- **PNR (Localizador):** Código de la aerolínea para gestionar la reserva
- **E-ticket (Boleto Electrónico):** Número(s) de boleto emitido(s)
- **Detalles completos del vuelo:**
  * Número de vuelo
  * Aerolínea
  * Origen y destino (aeropuertos completos con códigos IATA)
  * Fecha y horario de salida/llegada
  * Terminal
  * Duración del vuelo
  * Clase de servicio
- **Datos del pasajero:**
  * Nombre completo como aparece en boleto
  * Documento de identidad
  * Fecha de nacimiento (si aplica)
- **Código de barras / QR:** Para check-in
- **Información de check-in:**
  * Instrucciones para check-in online
  * Tiempos recomendados de llegada al aeropuerto
- **Políticas de equipaje:**
  * Equipaje de mano permitido
  * Equipaje documentado incluido
  * Costos adicionales por exceso
- **Instrucciones para cambios y cancelaciones:**
  * Políticas de la aerolínea
  * Contacto corporativo para gestionar cambios
- **Información adicional:**
  * Requisitos de viaje (visas, documentos, etc.)
  * Contacto de emergencia corporativo

**Momento de envío:**
- Inmediatamente después de emisión exitosa por el Agente
- Email contiene adjunto PDF con boleto electrónico completo

---

### **Notificaciones Adicionales (Automáticas)**

#### **Notificación de Cancelación por Proveedor**
- **Trigger:** Proveedor cancela reserva por pérdida de cupos
- **Destinatarios:** Viajero + Aprobador(es)
- **Contenido:** "Lo sentimos, la aerolínea canceló la disponibilidad. Debe realizar una nueva búsqueda."

#### **Notificación de Error de Emisión**
- **Trigger:** Agente intenta emitir pero proveedor no puede procesar
- **Destinatarios:** Viajero + Aprobador(es) + Contabilidad
- **Contenido:** "Su reserva no pudo ser emitida por problemas técnicos del proveedor"
- **Importante:** **Template de Emisión NO se envía** (solo se envía cuando emisión es exitosa)

#### **Notificación de Rechazo de Aprobación**
- **Trigger:** Aprobador rechaza la reserva
- **Destinatarios:** Viajero
- **Contenido:** "Su reserva ha sido rechazada por [Nombre Aprobador]" + razón de rechazo (si aplica)

#### **Notificación a Aprobador(es)**
- **Trigger:** Nueva reserva creada que requiere aprobación
- **Destinatarios:** Aprobador(es) asignado(s)
- **Contenido:** Link directo para aprobar/rechazar + detalles de reserva

#### **Notificación de Aprobación Exitosa**
- **Trigger:** Aprobación completada (Serial o Simple)
- **Destinatarios:** Viajero + Agente
- **Contenido:** "Su reserva ha sido aprobada y está lista para emisión"

---

### **Configuraciones y Restricciones**

**✅ Validaciones obligatorias:**
- Correo electrónico DEBE estar registrado en perfil del viajero
- Email debe estar validado previamente por administrador
- Sin correo válido → No se puede completar checkout

**❌ Restricciones:**
- Usuario NO puede cambiar email durante el proceso de reserva
- NO hay opción de agregar CC (copia) o CCO (copia oculta) en notificaciones
- NO se pueden deshabilitar notificaciones automáticas
- Templates son estándar del sistema (no personalizables por usuario)

**📊 Trazabilidad:**
- Sistema registra timestamp de cada email enviado
- Registro incluye:
  * Destinatario
  * Tipo de template
  * Fecha y hora de envío
  * Estado de entrega (enviado/fallido)
- Visible en panel de administración

---

## 📸 IMÁGENES DE REFERENCIA DEL FLUJO

**Ubicación de imágenes:**
```
https://[DOMINIO]/images/CORPORATIVO/
```

**Imágenes obligatorias para Descriptions:**

1. `Login-CORP.png` - Pantalla de login corporativo
2. `Home-CORP.png` - Home portal corporativo
3. `Home-vuelos-CORP.png` - Widget de vuelos
4. `Disponibilidad-vuelos-CORP.png` - Resultados de búsqueda
5. `upsell-vuelos-CORP.png` - Opciones de upselling
6. `Resumen-vuelos-CORP.png` - Resumen de reserva
7. `Checkout-vuelos-CORP.png` - Checkout
8. `Pago-CORP.png` - Proceso de pago
9. `Confirmacion-vuelos-CORP.png` - Confirmación
10. `Admin-CORP.png` - Panel admin
11. `Reserva-CORP.png` - Detalle de reserva

---

## 🔄 FLUJO DE APROBACIÓN Y EMISIÓN

**⚠️ PROCESO OBLIGATORIO EN CORPORATIVO USD**

### **Flujo Completo:**

```
┌─────────────────────────────────────────────────────────────────┐
│ 1. USUARIO VIAJERO / ORGANIZADOR                               │
│    - Busca vuelo                                               │
│    - Selecciona vuelo                                          │
│    - Completa checkout                                         │
│    - Procesa pago corporativo                                  │
│    ↓                                                           │
│    Estado: PENDIENTE DE APROBACIÓN                            │
│    Notificación → Aprobador(es) asignado(s)                   │
└─────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────┐
│ 2A. APROBACIÓN SERIAL (Múltiples Aprobadores)                 │
│    - Aprobador 1 recibe notificación                          │
│    - Aprobador 1 decide:                                      │
│      ✅ APRUEBA → Notifica Aprobador 2                       │
│      ❌ RECHAZA → Estado: RECHAZADA, FIN                     │
│    - Aprobador 2 decide:                                      │
│      ✅ APRUEBA → Notifica Aprobador 3 (o Agente si último) │
│      ❌ RECHAZA → Estado: RECHAZADA, FIN                     │
│    - Proceso continúa hasta último aprobador                  │
│    - Si TODOS aprueban → Estado: APROBADA                     │
│                                                               │
│ 2B. APROBACIÓN SIMPLE (Un Aprobador)                          │
│    - Aprobador recibe notificación                            │
│    - Aprobador decide:                                        │
│      ✅ APRUEBA → Estado: APROBADA                           │
│      ❌ RECHAZA → Estado: RECHAZADA, FIN                     │
└─────────────────────────────────────────────────────────────────┘
                              ↓
                         SI APROBADA
                              ↓
┌─────────────────────────────────────────────────────────────────┐
│ 3. AGENTE DE EMISIÓN (Manual - Modelo Semiautomático)         │
│    PASO 1: VALIDACIÓN                                         │
│    - Recibe notificación de reserva aprobada                  │
│    - Ingresa al panel administrador                           │
│    - Valida que TODOS los aprobadores aprobaron               │
│    - Verifica estado: APROBADA                                │
│                                                               │
│    PASO 2-3: SELECCIÓN DE TARJETA                             │
│    - Clic en botón "Emitir"                                   │
│    - Clic en "Tarjeta corporativa asociada a la empresa"      │
│    - Selecciona tarjeta específica de la empresa              │
│                                                               │
│    PASO 4: DESENCRIPTACIÓN                                    │
│    - Clic nuevamente en "Emisión"                             │
│    - Clic en "Desencriptar tarjeta"                           │
│    - Ve datos completos: número, vencimiento, CVV, titular    │
│                                                               │
│    PASO 5: PAGO MANUAL                                        │
│    - Ingresa a plataforma del proveedor/aerolínea             │
│    - Ingresa datos de tarjeta manualmente                     │
│    - Envía pago a aerolínea/comercio                          │
│    - Espera confirmación de pago exitoso                      │
│                                                               │
│    PASO 6: EMISIÓN SEGÚN DISPERSIÓN                           │
│    - **SIN dispersión (CORPORATIVO USD):** Emite en CASH      │
│    - **CON dispersión (otros):** Emite con TC                 │
│    - Registra número(s) de ticket en el sistema               │
│                                                               │
│    PASO 7: CONFIRMACIÓN Y TEMPLATE DE EMISIÓN                 │
│    - Sistema envía automáticamente Template de Emisión        │
│    - Destinatario: Correo del viajero registrado en perfil    │
│    - Contenido: PNR + e-ticket + código de barras + detalles │
│    - Timestamp registrado en trazabilidad                     │
│    ↓                                                           │
│    Estado: EMITIDA                                            │
│    Notificación → Viajero (e-ticket), Aprobador(es), Contabilidad │
│    Trazabilidad: Agente, fecha/hora, tarjeta, timestamp email│
│    ⚠️ NO HAY EMISIÓN AUTOMÁTICA - PROCESO 100% MANUAL        │
└─────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────┐
│ 4. CONFIRMACIÓN FINAL                                          │
│    - Viajero recibe ticket                                    │
│    - Comprobante descargable                                  │
│    - Factura a nombre de empresa                              │
│    - Trazabilidad completa en admin                           │
└─────────────────────────────────────────────────────────────────┘
```

### **Estados de Reserva:**

| Estado | Descripción | Actor responsable | Siguiente paso |
|--------|-------------|-------------------|----------------|
| **PENDIENTE DE APROBACIÓN** | Pago procesado, esperando decisión | Aprobador(es) | Aprobar o Rechazar |
| **PARCIALMENTE APROBADA** | (Solo Serial) Algunos aprobadores aprobaron, faltan otros | Siguiente aprobador | Aprobar o Rechazar |
| **APROBADA** | Todos los aprobadores requeridos aprobaron, lista para emitir | Agente | Emitir boleto |
| **RECHAZADA** | Al menos un aprobador rechazó, no se emite | - | Fin (cancelada) |
| **EMITIDA** | Agente emitió boleto exitosamente | - | Completada |

### **Validaciones del Flujo:**

**✅ OBLIGATORIAS (MODELO SEMIAUTOMÁTICO):**
1. Cada usuario DEBE tener UN flujo de aprobación asignado: **Simple** (un aprobador) **O** **Serial** (múltiples aprobadores), NO ambos
2. **Administrador crea el flujo de aprobación** y asigna aprobador(es) al usuario según el tipo elegido
3. Toda reserva DEBE pasar por aprobación (no hay excepción)
4. Aprobación DEBE completarse antes de que asesor pueda emitir:
   - **Serial:** TODOS deben aprobar, orden secuencial
   - **Simple:** UNO debe aprobar
5. UN SOLO RECHAZO bloquea emisión (ambos tipos)
6. **Emisión DEBE ser MANUAL por un asesor/agente humano**
7. **Asesor realiza la transacción manualmente** en el sistema del proveedor
8. Sistema DEBE bloquear emisión si no está aprobada
9. Sistema DEBE registrar trazabilidad completa
10. **NO existe emisión automática** - modelo semiautomático

**❌ RESTRICCIONES (MODELO SEMIAUTOMÁTICO):**
- Usuario NO puede emitir su propio boleto
- Usuario NO puede cambiar su flujo de aprobación asignado (Simple/Serial)
- Usuario NO puede cambiar aprobador SI configuración "Restringir cambio" está ACTIVA
- Usuario NO puede cambiar centro de costos SI configuración "Restringir cambio de centros de costo" está ACTIVA
- Usuario VIAJERO NO puede reservar para otros (solo para sí mismo)
- Usuario ORGANIZADOR NO puede invitar pasajeros externos SI configuración "Permitir invitar viajeros externos" está INACTIVA
- Usuario NO puede cambiar email durante el proceso de reserva
- Usuario NO puede completar checkout sin email válido registrado en perfil
- **Usuario SOLO puede reservar para pasajeros ADULTOS** (NO niños, NO infantes)
- **Usuario (Viajero u Organizador) NO puede cancelar sus propios boletos** - solo puede solicitar cancelación
- **Solo rol AGENTE puede ejecutar cancelaciones** (anular y cancelar boletos)
- Aprobador NO puede emitir boletos (solo aprobar/rechazar)
- Aprobador NO puede cancelar boletos directamente
- Aprobador NO puede solicitar cambios sin rechazar definitivamente
- **Solo rol AGENTE puede emitir boletos**
- Agente NO puede emitir sin aprobación previa completa
- Agente DEBE validar aprobaciones antes de emitir
- Agente DEBE seleccionar tarjeta corporativa de la empresa
- Agente DEBE desencriptar tarjeta para ver datos
- Agente DEBE ingresar datos manualmente en plataforma del proveedor
- Agente DEBE emitir en CASH (CORPORATIVO USD no tiene dispersión de fondos)
- **Sistema NO emite automáticamente** - modelo semiautomático
- **Agente debe realizar TODO el proceso manualmente**
- **Templates de notificación NO se pueden deshabilitar** - envío obligatorio y automático
- **Template de Emisión solo se envía al viajero** - aprobadores reciben notificación simple sin e-ticket
- NO hay opción de agregar CC o CCO en notificaciones
- NO hay bypass del flujo de aprobación
- NO hay timeout automático para aprobaciones pendientes
- NO existen criterios automáticos de asignación de aprobadores por monto
- En serial: NO se puede saltar aprobadores
- En serial: NO hay límite de cantidad de aprobadores
- En serial: Rechazo detiene proceso inmediatamente
- **NO existe emisión automática de boletos**
- **NO existe funcionalidad de modificar reservas** - una vez creada NO se puede modificar
- Única alternativa a modificación: cancelar y crear nueva reserva
- Cancelación ANTES de emisión: sin penalización
- Cancelación DESPUÉS de emisión: sujeta a políticas de aerolínea
- Solo rol AGENTE puede ejecutar cancelaciones
- Usuario/Organizador puede solicitar cancelación pero requiere Agente para ejecutar
- Aprobador NO puede cancelar directamente
- Solo UN agente puede emitir una reserva a la vez (lock de emisión)
- Si proveedor cancela reserva por falta de cupos: usuario debe comenzar de cero

---

## 📝 NOTAS IMPORTANTES

1. **Modelo de Operación:**
   - ⚠️ **MODELO SEMIAUTOMÁTICO**
   - **Asesor/Agente realiza las transacciones de manera MANUAL**
   - NO hay emisión automática de boletos
   - Requiere intervención humana del agente en todo momento
   - Proceso manual después de aprobación

   **Proceso detallado de Emisión Manual por Agente:**
   
   **Paso 1: Validación de Aprobaciones**
   - Agente ingresa al panel de administrador
   - Busca la reserva pendiente de emisión
   - **VALIDA que TODOS los aprobadores hayan aprobado el boleto**
   - Verifica estado: APROBADA (no PENDIENTE ni PARCIALMENTE APROBADA)
   - Revisa trazabilidad completa de aprobaciones
   
   **Paso 2: Iniciar Emisión**
   - Agente hace clic en botón **"Emitir"** en el administrador
   - Sistema despliega opciones de emisión
   
   **Paso 3: Selección de Tarjeta Corporativa**
   - Agente hace clic en opción **"Tarjeta corporativa asociada a la empresa"**
   - Sistema muestra lista de tarjetas corporativas disponibles de la empresa
   - Agente **selecciona la tarjeta** con la cual la empresa realizará el pago
   - Confirma selección
   
   **Paso 4: Desencriptación de Tarjeta**
   - Agente hace clic nuevamente en botón **"Emisión"**
   - Agente hace clic en opción **"Desencriptar tarjeta"**
   - Sistema muestra los datos completos de la tarjeta corporativa:
     - Número de tarjeta
     - Fecha de vencimiento
     - CVV/CVC
     - Nombre del titular
   - ⚠️ **CRÍTICO:** Datos sensibles visibles solo para rol Agente
   
   **Paso 5: Pago en Plataforma del Proveedor**
   - Agente ingresa a la **plataforma asignada para el pago** (sistema del proveedor/aerolínea)
   - Agente ingresa manualmente los datos de la tarjeta desencriptada
   - Agente envía el pago:
     - A la aerolínea directamente, O
     - Al comercio correspondiente (GDS, aggregator, etc.)
   - Agente espera confirmación de pago exitoso
   - Agente registra código de autorización/transacción
   
   **Paso 6: Emisión según Dispersión de Fondos**
   
   **A) Si NO tiene dispersión de fondos (CORPORATIVO USD):**
   - Agente procede a **emitir en CASH**
   - Emite boleto manualmente en el sistema del proveedor
   - Registra número(s) de ticket en el sistema
   - Estado cambia a EMITIDA
   
   **B) Si tiene dispersión de fondos (otros modelos):**
   - Agente procede a **emitir con TC** (tarjeta de crédito)
   - Sistema procesa emisión automática con dispersión
   - Registra número(s) de ticket
   - Estado cambia a EMITIDA
   
   ⚠️ **NOTA:** CORPORATIVO USD **NO tiene dispersión de fondos**, por lo tanto:
   - **SIEMPRE se emite en CASH**
   - Proceso completamente manual
   - Agente responsable de todo el flujo
   
   **Paso 7: Confirmación Final**
   - Sistema registra emisión exitosa
   - Estado de reserva: EMITIDA
   - **Envío automático de Template de Emisión:**
     * Destinatario: Correo registrado en perfil del viajero
     * Contenido: PNR, e-ticket, detalles completos del vuelo, código de barras, políticas de equipaje
     * Envío inmediato sin intervención manual
     * Template NO enviado a aprobadores (solo viajero recibe boleto electrónico)
   - Notificaciones adicionales enviadas:
     * Aprobador(es): "Boleto emitido correctamente" (notificación simple, sin e-ticket)
     * Contabilidad: "Registro de gasto corporativo" (factura con tarjeta utilizada)
   - Guarda trazabilidad completa:
     * Agente que emitió
     * Fecha y hora de emisión
     * Tarjeta corporativa utilizada
     * **Timestamp de envío de Template de Emisión al viajero**

2. **Asignación de Aprobadores:**
   - **Administrador** crea el flujo de aprobación en el sistema
   - Administrador asigna aprobador(es) a cada usuario al momento de crear el flujo
   - Cada usuario tiene **UN SOLO tipo** de flujo: **Simple** (un aprobador) **O** **Serial** (múltiples aprobadores)
   - **NO es posible** tener ambos tipos simultáneamente para el mismo usuario
   - Usuario NO puede cambiar su flujo de aprobación asignado
   - Flujo de aprobación es obligatorio para todos los usuarios

   **Configuración: "Restringir el cambio de aprobador en el formulario de reserva"**
   - Esta configuración determina si el usuario puede cambiar su aprobador durante el checkout
   - **Si está ACTIVA:** Usuario NO puede cambiar el aprobador, se muestra solo el/los aprobador(es) asignado(s) (sin opción de modificar)
   - **Si está INACTIVA:** Usuario SÍ puede seleccionar otro aprobador desde una lista desplegable de aprobadores disponibles
   - Configuración administrable por rol (puede aplicarse a usuarios específicos o grupos)
   - Útil para empresas con políticas de aprobación estrictas vs. flexibles

   **Configuración de aprobadores en Serial:**
   - **NO hay límite** de cantidad de aprobadores en cadena serial
   - Administrador define cuántos aprobadores según necesidad corporativa
   - **NO existen criterios automáticos** (ej: no hay regla de "reservas >$5000 requieren 2 aprobadores")
   - Toda configuración es manual por parte del administrador

   **Visibilidad del aprobador:**
   - Usuario **SÍ puede ver** quién es su aprobador asignado
   - Información visible **en el checkout**, en el formulario antes de proceder al pago
   - En flujo Serial: se muestra la cadena completa de aprobadores
   - **Cambio de aprobador:** Depende de configuración "Restringir el cambio de aprobador":
     - **Si configuración ACTIVA:** Solo lectura, usuario ve pero NO puede cambiar aprobador(es)
     - **Si configuración INACTIVA:** Usuario puede seleccionar otro aprobador de lista desplegable

   **Restricciones de aprobadores:**
   - Aprobador **NO puede delegar** su aprobación a otra persona
   - Aprobador **NO puede solicitar cambios** sin rechazar definitivamente
   - Solo dos opciones disponibles: **APROBAR** o **RECHAZAR** (con motivo obligatorio)

   **Timeouts y cancelaciones:**
   - **NO hay timeout automático** para aprobaciones pendientes
   - Aprobación puede quedar pendiente indefinidamente hasta decisión del aprobador
   - ⚠️ **CRÍTICO:** Si la reserva se cancela por parte del proveedor (pérdida de cupo de aerolínea), se debe comenzar de cero
   - Sin cupos disponibles = reserva inválida, requiere nueva búsqueda y nueva reserva

3. **Prioridad del Producto:**
   - Vuelos es el ÚNICO producto disponible en CORPORATIVO USD
   - No crear casos de Hoteles, Autos, Actividades o Disney

4. **Configuración para Usuarios Organizadores de Viaje:**
   - CORPORATIVO USD tiene dos tipos de usuarios: **Viajero** y **Organizador de viaje**
   - **Organizador de viaje:** Usuario que reserva vuelos para otros empleados/personas
   
   **Configuración: "Permitir que el usuario organizador de viajes invite a viajeros externos"**
   - Esta configuración determina si el organizador puede agregar pasajeros que NO están en la empresa
   - **Si está ACTIVA:** 
     - Organizador puede invitar pasajeros externos (ingresar datos manualmente)
     - También puede seleccionar pasajeros de la lista de empleados de la empresa
     - Útil para invitados, consultores, proveedores externos que viajan con la empresa
   - **Si está INACTIVA:**
     - Organizador SOLO puede seleccionar pasajeros de lista desplegable de empleados
     - NO puede ingresar datos de pasajeros externos manualmente
     - Lista desplegable muestra únicamente empleados asociados a la empresa
   - Configuración administrable a nivel de empresa o por grupos de organizadores
   - **Usuario tipo VIAJERO:** Esta configuración NO aplica, siempre reserva para sí mismo

5. **Configuración de Centros de Costo:**
   - **Centro de costos:** Campo obligatorio para facturación corporativa en todas las reservas
   - Usuario puede tener uno o varios centros de costo asignados por el administrador
   
   **Configuración: "Restringir el cambio de centros de costo en el formulario de reserva"**
   - Esta configuración determina si el usuario puede cambiar el centro de costos durante el checkout
   - **Si está ACTIVA:**
     - Usuario NO puede cambiar el centro de costos
     - Campo es SOLO LECTURA
     - Se muestra el centro de costos asignado por defecto
     - Útil para empresas con políticas estrictas de control presupuestario
   - **Si está INACTIVA:**
     - Usuario SÍ puede seleccionar entre los centros de costo que tiene autorizados
     - Lista desplegable muestra todos los centros de costo disponibles para el usuario
     - Útil para empleados que manejan múltiples proyectos o áreas
   - Configuración administrable por usuario o grupos de usuarios
   - Centro de costos seleccionado se refleja en la facturación y reportes

6. **Política de Reservas:**
   - **Política de Reservas:** Conjunto de reglas configuradas por la empresa para controlar el comportamiento de reservas
   - Administrador puede configurar políticas específicas por empresa/grupos de usuarios
   
   **Configuración: "Política de Reservas"**
   - Esta configuración establece reglas que los usuarios deben cumplir al reservar
   - Ejemplos de políticas comunes:
     - **Anticipación mínima:** Reservar con X días de anticipación
     - **Límite de precio:** No exceder USD X por pasajero
     - **Aerolíneas permitidas:** Solo reservar con aerolíneas específicas
     - **Clase de vuelo:** Restricción de clase (solo económica, etc.)
     - **Horarios permitidos:** Evitar vuelos nocturnos/madrugada
     - **Escalas máximas:** Limitar cantidad de escalas
   
   **Comportamiento cuando NO se cumple la política:**
   - Sistema detecta automáticamente si la reserva viola alguna política configurada
   - **Campo obligatorio aparece:** "Justificación de excepción"
   - Usuario DEBE escribir:
     - Por qué necesita hacer esta reserva
     - Razón de negocio que justifica no cumplir la política
     - Argumento válido con contexto empresarial
   - Validaciones del campo:
     - Mínimo de caracteres (configurable, ej: 50 caracteres)
     - No puede quedar vacío
     - No permite texto genérico (ej: "urgente", "necesario")
   - Sistema NO permite continuar sin justificación completa
   
   **Trazabilidad y Auditoría:**
   - Justificación queda registrada en la reserva
   - Aprobador puede ver la justificación al momento de aprobar
   - Panel admin muestra histórico de excepciones a políticas
   - Reportes pueden filtrar reservas con excepciones
   - Útil para análisis de cumplimiento corporativo
   
   **Si cumple todas las políticas:**
   - Campo de justificación NO aparece
   - Usuario continúa flujo normal sin interrupciones
   - Reserva se marca como "Cumple políticas corporativas"

7. **Moneda:**
   - TODOS los precios deben mostrarse en USD
   - No hay conversión de monedas

8. **Facturación:**
   - SIEMPRE a nombre de la empresa
   - Centro de costos OBLIGATORIO
   - RUC/NIT/Tax ID requerido

9. **Políticas Corporativas:**
   - Pueden limitar aerolíneas disponibles
   - Pueden limitar clases de vuelo
   - Pueden requerir aprobación para montos altos

10. **Proveedores:**
   - **AGGREGATOR - NETACTICA** (sin dispersión de fondos)
   - **AGGREGATOR - SABRE** (sin dispersión de fondos)
   - **SABRE EDIFACT** (sin dispersión de fondos)
   - ⚠️ Todos los proveedores operan sin dispersión de fondos
   - **Emisión manual por asesor** después de aprobación
   - Asesor realiza transacción manualmente en sistema del proveedor

11. **Modificación y Cancelación:**
   - ❌ **NO existe funcionalidad de modificar reservas** en el sistema
   - Una vez creada y confirmada, la reserva NO puede editarse
   - Alternativa: Cancelar reserva actual y crear nueva desde cero
   - **Cancelación antes de emisión:** Sin penalización, reembolso completo
   - **Cancelación después de emisión:** Sujeta a políticas de la aerolínea
     * Tarifa flexible: permite cancelación (puede haber cargo)
     * Tarifa no reembolsable: penalización alta o pérdida total
     * Tarifa promocional: restricciones estrictas
   - **IMPORTANTE:** Usuario (Viajero u Organizador) NO puede cancelar directamente
   - Usuario SOLO puede **solicitar** cancelación
   - Solo rol **AGENTE** puede **ejecutar** cancelaciones (anular y cancelar boletos) en el sistema
   - Proceso: Usuario solicita → Agente verifica políticas → Agente informa usuario → Usuario confirma → Agente ejecuta
   - Trazabilidad completa: quién solicitó, quién ejecutó (Agente), cuándo, política aplicada, montos

12. **Métodos de Pago:**
   - **Tarjetas corporativas aceptadas:** Todas las franquicias (Visa, Mastercard, American Express, Diners Club, Discover, JCB, etc.)
   - **Límite de monto:** Sin límite de monto por transacción
   - **Autorización especial:** NO requerida para montos altos (sin umbral de autorización)
   - **Validación CVV:** Opcional, NO obligatorio (sistema acepta transacciones sin CVV)
   - **Datos requeridos:**
     * Número de tarjeta corporativa (obligatorio)
     * Fecha de vencimiento (obligatorio)
     * Nombre del titular (obligatorio)
     * CVV (opcional)
   - **Procesamiento:** Inmediato, sin validaciones adicionales por monto
   - **Seguridad:** HTTPS, encriptación de datos sensibles
   - **Rechazo de pago:** NO es por límite de sistema, causas posibles: tarjeta inválida, fondos insuficientes, error procesador

13. **Restricción de Pasajeros:**
   - ❌ **SOLO se permiten reservas para pasajeros ADULTOS**
   - NO se aceptan niños (2-11 años)
   - NO se aceptan infantes/bebés (0-2 años)
   - Widget de búsqueda NO tiene opción de seleccionar niños o infantes
   - Contador de pasajeros solo cuenta adultos (1-9)
   - Todos los pasajeros deben tener edad adulta según políticas de aerolíneas
   - Si empresa requiere reservar para menores: debe usar otro canal o modelo

---

## 🆘 CASOS EDGE Y MANEJO DE ERRORES

### **Sin Resultados de Búsqueda**
```
Acción: Buscar ruta sin disponibilidad
Resultado: Mensaje "No hay vuelos disponibles para los criterios seleccionados"
Validar: Opciones para modificar búsqueda
```

### **Timeout en Búsqueda**
```
Acción: Timeout de proveedor
Resultado: Mensaje de error amigable, opción de reintentar
Validar: No crash, manejo graceful
```

### **Error en Pago**
```
Acción: Pago rechazado
Resultado: Mensaje de error específico, opción de reintentar con otro método
Validar: 
- Reserva NO confirmada, datos preservados
- NO es por límite de monto (sistema acepta cualquier monto)
- NO requiere autorización especial para montos altos
- Posibles causas del rechazo:
  * Tarjeta inválida o vencida
  * Fondos insuficientes en la cuenta corporativa
  * Error del procesador de pagos
  * Problema de conectividad
  * Datos de tarjeta incorrectos
- Opción de reintentar con misma tarjeta (si error fue temporal)
- Opción de cambiar a otra tarjeta corporativa
- Todas las franquicias aceptadas (Visa, Mastercard, Amex, Diners, etc.)
- Usuario no pierde información ingresada en checkout
```

### **Centro de Costos Inválido**
```
Acción: Ingresar centro de costos no autorizado
Resultado: Validación inmediata, mensaje de error claro
Validar: No permite continuar, sugerencias de centros válidos
```

### **Usuario Sin Permisos**
```
Acción: Usuario sin permisos intenta acceder
Resultado: Mensaje "No tiene permisos para realizar esta acción"
Validar: Redirección o bloqueo apropiado
```

### **Intento de Reservar Menores de Edad**
```
Acción: Usuario intenta buscar o reservar para niños o infantes
Resultado: Sistema NO permite seleccionar menores
Validar:
- Widget de búsqueda NO tiene opción de "Niños" o "Infantes"
- Contador de pasajeros solo muestra "Adultos" (1-9)
- Si usuario pregunta o busca opción: mensaje informativo visible
- Mensaje sugerido: "CORPORATIVO USD solo permite reservas para pasajeros adultos. Para viajes con menores, contacte con su administrador."
- NO hay workaround o forma alternativa de agregar menores
- Sistema valida que todos los pasajeros sean adultos
- Restricción aplica en todos los pasos (búsqueda, disponibilidad, checkout)
- Si se intenta ingresar fecha de nacimiento de menor en checkout: validación rechaza
```

### **Usuario Intenta Cancelar Reserva/Boleto Directamente**
```
Acción: Usuario (Viajero u Organizador) intenta cancelar su propia reserva o boleto
Resultado: Sistema NO permite cancelación directa por usuario
Validar:
- Usuario NO tiene botón "Cancelar" en panel de reservas
- Usuario NO tiene opción de "Anular boleto" en detalle de reserva
- Si usuario busca opción de cancelación: NO la encuentra
- Mensaje informativo: "Para cancelar esta reserva, contacte con el equipo de soporte" o "Solo los agentes pueden cancelar reservas"
- Usuario debe contactar Agente:
  * Por canal corporativo (email, chat, teléfono)
  * Explicar motivo de cancelación
  * Esperar que Agente ejecute la cancelación
- Sistema registra:
  * Usuario que solicitó cancelación (Viajero u Organizador)
  * Agente que ejecutó cancelación
  * Fecha/hora de solicitud y ejecución
- Trazabilidad diferencia entre "solicitante" y "ejecutor"
- Aprobador tampoco puede cancelar (ni solicitar ni ejecutar)
```

### **Modificación y Cancelación de Reservas**

#### **Modificación de Reserva NO Disponible**
```
Acción: Usuario o Agente intenta modificar una reserva ya confirmada/emitida
Resultado: Modificación NO está permitida en el sistema
Validar:
- Sistema NO ofrece opción de modificar reserva existente
- No hay botón "Modificar" o "Editar" en detalle de reserva
- Una vez creada y confirmada, la reserva NO puede modificarse
- Si usuario necesita cambiar algo:
  * Debe CANCELAR la reserva actual (sujeto a políticas)
  * Crear una NUEVA reserva desde cero
- Mensaje informativo: "Esta reserva no puede modificarse. Si necesita cambios, debe cancelarla y crear una nueva reserva."

Estados donde NO se puede modificar:
- PENDIENTE DE APROBACIÓN: No modificable
- PARCIALMENTE APROBADA: No modificable
- APROBADA: No modificable
- EMITIDA: No modificable (solo cancelación según políticas)
- RECHAZADA: No aplica (reserva ya cancelada)
- CANCELADA: No aplica (reserva ya cancelada)
```

#### **Cancelación de Reservas - Políticas de la Aerolínea**
```
Escenario 1: Cancelación de reserva ANTES de emisión
Acción: Usuario (Viajero u Organizador) solicita cancelar reserva en estado PENDIENTE o APROBADA
Resultado: Usuario NO puede cancelar directamente, debe contactar Agente
Validar:
- Usuario NO tiene botón "Cancelar" en su panel
- Usuario NO puede ejecutar cancelación por sí mismo
- Usuario debe solicitar cancelación al Agente:
  * Por correo, chat, teléfono u otro canal
  * Explicar motivo de cancelación
- **Agente** es quien ejecuta la cancelación en el sistema:
  * Agente verifica estado de reserva (PENDIENTE o APROBADA)
  * Agente confirma que aún NO está emitida (no hay boleto generado)
  * Agente procesa cancelación inmediata
  * No hay penalización económica
  * Pago corporativo puede ser reversado
- Estado cambia a: CANCELADA POR USUARIO (ejecutada por Agente)
- Notificaciones enviadas:
  * Viajero: "Su reserva ha sido cancelada exitosamente"
  * Aprobador(es): "Reserva cancelada por solicitud de usuario"
  * Contabilidad: "Cargo reversado"
- Proceso de reembolso/reversión automático
- Trazabilidad: 
  * Usuario que solicitó cancelación
  * Agente que ejecutó cancelación
  * Fecha/hora, razón (opcional)

Escenario 2: Cancelación de reserva DESPUÉS de emisión (EMITIDA)
Acción: Usuario (Viajero u Organizador) solicita cancelar boleto ya emitido
Resultado: Usuario NO puede cancelar directamente, debe contactar Agente. Cancelación sujeta a políticas de aerolínea
Validar:
- Usuario NO tiene botón "Cancelar" para boletos emitidos
- Usuario debe solicitar cancelación al Agente
- Boleto YA está emitido (PNR activo, e-ticket generado)
- **Agente consulta políticas** de cancelación de la aerolínea:
  * Tarifa FLEXIBLE: Permite cancelación/cambios (puede haber cargo)
  * Tarifa NO REEMBOLSABLE: No permite cancelación o penalización alta
  * Tarifa PROMOCIONAL: Restricciones estrictas
- **Agente informa al usuario** sobre:
  * Política específica de la aerolínea
  * Costo de penalización (si aplica)
  * Monto reembolsable (si aplica)
  * Deadline para cancelar sin penalización (si aplica)
- **Usuario decide** si procede con cancelación después de conocer costos
- **Proceso ejecutado por Agente:**
  1. Agente verifica políticas en sistema del proveedor
  2. Informa al usuario sobre costos/penalizaciones
  3. Usuario decide si acepta condiciones
  4. Si usuario acepta: Agente gestiona cancelación en plataforma del proveedor
  5. Agente actualiza estado en sistema interno: CANCELADA
  6. Proceso de reembolso según políticas (puede tomar días/semanas)
- Notificaciones enviadas:
  * Viajero: "Su boleto ha sido cancelado según políticas de [AEROLÍNEA]"
  * Aprobador(es): "Boleto emitido cancelado"
  * Contabilidad: "Proceso de reembolso iniciado - Monto: USD [X]"
- Trazabilidad completa:
  * Usuario que solicitó cancelación
  * Agente que procesó cancelación
  * Fecha/hora de solicitud y ejecución
  * Política aplicada
  * Monto de penalización
  * Monto reembolsable
  * Tiempo estimado de reembolso
  * Estado de reembolso (pendiente/procesado/completado)

Escenario 3: Usuario solicita cancelación pero desconoce políticas
Acción: Usuario (Viajero/Organizador) contacta soporte/Agente para cancelar
Resultado: Agente informa políticas antes de proceder
Validar:
- Usuario contacta Agente (no puede cancelar por sí mismo)
- Agente consulta PNR en sistema del proveedor
- Agente verifica tarifa y reglas de cancelación
- Agente explica claramente:
  * ¿Se puede cancelar?
  * ¿Cuánto cuesta cancelar?
  * ¿Cuánto se reembolsa?
  * ¿Cuánto tiempo toma el reembolso?
- Usuario toma decisión informada
- Si usuario rechaza por costo alto: reserva permanece activa
- Si usuario acepta: Agente procede con cancelación

Escenario 4: Cancelación por NO SHOW (pasajero no se presentó)
Acción: Pasajero no se presentó al vuelo
Resultado: Boleto pierde validez, sin reembolso
Validar:
- Aerolínea marca boleto como NO SHOW
- No hay reembolso posible
- Estado en sistema: CANCELADA POR NO SHOW
- Notificación a contabilidad: "Pérdida total - No reembolso"
- Empresa asume costo completo
- Trazabilidad: fecha del vuelo, fecha de NO SHOW

Escenario 5: Cancelación voluntaria vs. involuntaria
Acción: Diferenciar entre tipos de cancelación
Resultado: Políticas diferentes según tipo
Validar:
- **Voluntaria (por usuario):**
  * Sujeta a políticas de tarifa
  * Puede haber penalización
  * Reembolso parcial o nulo
- **Involuntaria (por aerolínea):**
  * Por razones operacionales (clima, falla técnica, etc.)
  * Reembolso COMPLETO sin penalización
  * Aerolínea debe ofrecer alternativas
  * Derecho a compensación adicional (según regulación)
- Sistema debe registrar motivo de cancelación claramente
```

#### **Restricciones de Modificación y Cancelación**
```
MODIFICACIÓN:
- ❌ NO existe funcionalidad de modificar reservas en el sistema
- ❌ Usuario NO puede cambiar fechas, horarios, pasajeros, etc.
- ❌ Agente NO puede modificar reserva existente
- ✅ Única opción: Cancelar y crear nueva reserva

CANCELACIÓN:
- ✅ Antes de emisión: Cancelación libre sin penalización (ejecutada por Agente)
- ⚠️ Después de emisión: Sujeto a políticas de aerolínea (ejecutada por Agente)
- ⚠️ Penalizaciones varían según tarifa contratada
- ⚠️ Tarifas no reembolsables: pérdida total o parcial
- ✅ Cancelación involuntaria (aerolínea): reembolso completo
- ❌ NO SHOW: sin reembolso, pérdida total

ROLES Y PERMISOS:
- Usuario VIAJERO: SOLO puede solicitar cancelación (NO puede ejecutarla)
- Usuario ORGANIZADOR: SOLO puede solicitar cancelación de reservas que creó (NO puede ejecutarla)
- Usuario APROBADOR: NO puede solicitar ni cancelar directamente
- **Rol AGENTE: ÚNICO rol que puede ejecutar cancelaciones en el sistema** (anular y cancelar boletos)
- Administrador: Puede ver historial y trazabilidad de cancelaciones (NO ejecuta cancelaciones)
```

---

### **Cancelación por Proveedor - Pérdida de Cupos**
```
Acción: Reserva pendiente de aprobación pero proveedor cancela por falta de cupos
Resultado: Notificación de cancelación a usuario y aprobador(es)
Estado: CANCELADA POR PROVEEDOR
Validar: 
- Usuario debe comenzar de cero (nueva búsqueda)
- Reserva anterior ya no es válida
- No se puede recuperar la misma reserva
- Mensaje claro: "Lo sentimos, la aerolínea canceló la disponibilidad. Debe realizar una nueva búsqueda."
```

### **Cambio de Proveedor Mid-Flight - Proveedor No Puede Emitir**
```
Escenario 1: Proveedor original no puede emitir después de aprobación
Acción: Agente intenta emitir pero proveedor/aerolínea no puede procesar la emisión
Resultado: Emisión fallida, reserva debe cancelarse
Validar:
- Error en sistema del proveedor (disponibilidad perdida, problema técnico, etc.)
- Agente NO puede completar emisión
- Estado permanece en APROBADA (no cambia a EMITIDA)
- Alerta crítica generada
- Reserva DEBE CANCELARSE
- Sistema marca reserva con estado: CANCELADA POR ERROR DE EMISIÓN
- Notificaciones enviadas:
  * Viajero: "Su reserva no pudo ser emitida por problemas técnicos del proveedor" (**Template de Emisión NO se envía**)
  * Aprobador(es): "Reserva aprobada no pudo emitirse"
  * Contabilidad: "Verificar si se procesó cargo en tarjeta"

Escenario 2: Usuario debe realizar nueva reserva desde cero
Acción: Usuario debe buscar nuevamente después de cancelación
Resultado: Nueva búsqueda y selección de vuelo
Validar:
- Usuario DEBE iniciar nueva búsqueda desde el home
- NO puede recuperar la reserva anterior
- NO puede reutilizar la aprobación anterior
- Debe seleccionar NUEVO vuelo:
  * Puede ser del MISMO proveedor (diferente vuelo)
  * Puede ser de OTRO proveedor (NETACTICA, SABRE, SABRE EDIFACT)
  * Puede ser de OTRA aerolínea
- Nueva reserva requiere:
  * Nueva selección en disponibilidad
  * Nuevo checkout (datos pueden pre-cargarse)
  * Nuevo pago corporativo
  * NUEVA APROBACIÓN (proceso completo desde cero)
- Aprobador(es) deben aprobar nuevamente
- Agente realiza nueva emisión manual

Escenario 3: Cambio de proveedor en nueva búsqueda
Acción: Usuario selecciona vuelo de proveedor diferente al original
Resultado: Reserva con nuevo proveedor procesada normalmente
Validar:
- Sistema permite seleccionar cualquier proveedor disponible:
  * AGGREGATOR - NETACTICA
  * AGGREGATOR - SABRE
  * SABRE EDIFACT
- Proceso E2E completo con nuevo proveedor
- Sin relación con reserva anterior cancelada
- Historial muestra:
  * Reserva 1: CANCELADA POR ERROR DE EMISIÓN (Proveedor A)
  * Reserva 2: EMITIDA (Proveedor B)
- Trazabilidad completa de ambas reservas

Escenario 4: Reembolso o ajuste de cargo si se procesó pago
Acción: Si tarjeta fue cargada pero emisión falló, gestionar reembolso
Resultado: Proceso de reembolso o ajuste
Validar:
- Contabilidad verifica si se procesó cargo en tarjeta
- Si cargo procesado:
  * Iniciar proceso de reembolso con proveedor
  * Contactar banco/procesador de pagos
  * Registrar caso en sistema
  * Notificar a empresa sobre reembolso en proceso
- Si cargo NO procesado:
  * Confirmar que no hay débito
  * Marcar como "Sin cargo procesado"
- Trazabilidad de gestión de reembolso
- Usuario puede proceder con nueva reserva sin esperar reembolso

Escenario 5: Múltiples intentos fallidos de emisión
Acción: Usuario tiene varias reservas canceladas por error de emisión
Resultado: Alerta de patrón de fallas
Validar:
- Sistema detecta múltiples cancelaciones por error de emisión
- Alerta a supervisor/administrador
- Posible problema sistémico con proveedor
- Investigación requerida
- Considerar deshabilitar proveedor temporalmente
- Notificar a usuarios sobre problemas técnicos
```

### **Aprobación Pendiente Sin Timeout**
```
Acción: Reserva pendiente de aprobación por tiempo prolongado (días/semanas)
Resultado: Reserva permanece en estado PENDIENTE DE APROBACIÓN
Validar:
- NO hay cancelación automática por timeout
- Sistema mantiene estado indefinidamente
- Aprobador puede aprobar/rechazar en cualquier momento
- Riesgo: Puede perder cupos si proveedor cancela
```

### **Emisión Manual por Agente - Proceso Completo**
```
Escenario 1: Emisión exitosa sin dispersión de fondos (CORPORATIVO USD)
Acción: Agente procede a emitir boleto aprobado
Resultado: Emisión completada correctamente
Validar:
PASO 1 - Validación:
- Agente accede a administrador
- Reserva en estado APROBADA
- Todos los aprobadores han aprobado
- Trazabilidad de aprobaciones visible

PASO 2-3 - Selección de Tarjeta:
- Botón "Emitir" visible y habilitado
- Opción "Tarjeta corporativa asociada a la empresa" disponible
- Lista de tarjetas corporativas se despliega
- Agente puede seleccionar tarjeta específica
- Tarjeta seleccionada se marca correctamente

PASO 4 - Desencriptación:
- Botón "Emisión" habilitado nuevamente
- Opción "Desencriptar tarjeta" visible
- Sistema muestra datos completos de la tarjeta:
  * Número de tarjeta (16 dígitos)
  * Fecha de vencimiento (MM/AA)
  * CVV/CVC (3-4 dígitos)
  * Nombre del titular
- Datos son legibles y copiables
- Solo rol Agente puede ver esta información

PASO 5 - Pago Manual:
- Agente ingresa a plataforma del proveedor
- Ingresa datos de tarjeta manualmente
- Pago se procesa correctamente
- Confirmación de pago recibida
- Código de autorización obtenido

PASO 6 - Emisión en CASH:
- Agente emite boleto en modo CASH (sin dispersión)
- Sistema del proveedor genera número(s) de ticket
- Agente registra número(s) de ticket en sistema interno
- Estado cambia a EMITIDA
- Timestamp y agente registrados

PASO 7 - Confirmación:
- Sistema confirma emisión exitosa
- **Template de Emisión enviado automáticamente:**
  * Destinatario: Correo del viajero (verificar en trazabilidad)
  * Contenido: PNR + e-ticket + detalles de vuelo + código de barras + políticas
  * Timestamp registrado en sistema
- Notificaciones simples enviadas:
  * Aprobador(es): "Boleto emitido correctamente" (sin e-ticket)
  * Contabilidad: "Registro de gasto corporativo" (factura con tarjeta utilizada)
- Trazabilidad completa visible en admin
- Comprobante descargable

Escenario 2: Error en pago - Tarjeta rechazada
Acción: Agente intenta pago pero tarjeta es rechazada por banco
Resultado: Pago fallido, emisión no procede
Validar:
- Plataforma del proveedor muestra error de pago
- Agente NO puede continuar con emisión
- Estado permanece en APROBADA (no cambia a EMITIDA)
- Agente debe:
  * Seleccionar otra tarjeta corporativa de la empresa
  * Reintentar proceso desde PASO 3
- Sistema registra intento fallido en trazabilidad
- Notificación a contabilidad sobre tarjeta rechazada

Escenario 3: Error en emisión después de pago exitoso
Acción: Pago exitoso pero error al emitir en sistema del proveedor
Resultado: Situación crítica - dinero debitado pero sin boleto
Validar:
- Pago confirmado y debitado
- Error al generar número de ticket en sistema del proveedor
- Estado queda en APROBADA (no EMITIDA)
- Alerta crítica generada
- Agente debe:
  * Contactar soporte del proveedor urgentemente
  * Gestionar emisión manual/recuperación
  * Registrar incidencia en sistema
- Sistema marca reserva con flag "Pago procesado - Emisión pendiente"
- Notificación urgente a supervisor

Escenario 4: Agente intenta emitir sin validar aprobaciones
Acción: Agente intenta emitir reserva que NO está completamente aprobada
Resultado: Sistema bloquea emisión
Validar:
- Botón "Emitir" deshabilitado o no visible
- Mensaje de error: "La reserva debe estar APROBADA para emitir"
- Estado actual visible: PENDIENTE o PARCIALMENTE APROBADA
- Lista de aprobadores pendientes visible
- Agente no puede continuar
- Sistema NO permite acceso a selección de tarjetas

Escenario 5: Múltiples agentes intentan emitir la misma reserva
Acción: Dos agentes acceden simultáneamente a emitir el mismo boleto
Resultado: Lock de reserva - solo un agente puede emitir
Validar:
- Primer agente obtiene lock de emisión
- Segundo agente ve mensaje: "Reserva en proceso de emisión por otro agente"
- Solo un proceso de emisión activo a la vez
- Lock se libera al completar emisión o después de timeout
- Previene doble emisión
- Trazabilidad de quién obtuvo el lock
```

### **Cambio de Aprobador en Checkout**
```
Escenario 1: Configuración "Restringir cambio" ACTIVA
Acción: Usuario intenta cambiar aprobador en checkout
Resultado: Campo de aprobador(es) es SOLO LECTURA
Validar:
- No hay lista desplegable
- Solo muestra aprobador(es) asignado(s)
- Usuario no puede modificar
- Mensaje informativo (opcional): "Aprobador asignado por política corporativa"

Escenario 2: Configuración "Restringir cambio" INACTIVA
Acción: Usuario selecciona otro aprobador de lista desplegable
Resultado: Aprobador cambia correctamente
Validar:
- Lista desplegable visible y funcional
- Muestra todos los aprobadores disponibles
- Selección se guarda correctamente
- Notificación se envía al nuevo aprobador seleccionado (no al asignado originalmente)
```

### **Organizador Invitando Pasajeros (Externos vs. Empleados)**
```
Escenario 1: Usuario ORGANIZADOR - Configuración "Permitir invitar viajeros externos" ACTIVA
Acción: Organizador agrega pasajeros para el viaje
Resultado: Dos opciones disponibles
Validar:
- Botón/opción "Invitar pasajero externo" visible y funcional
- Permite ingresar datos manualmente (nombre, documento, email, etc.)
- Lista desplegable de empleados de la empresa también disponible
- Puede mezclar pasajeros externos e internos en la misma reserva
- Datos de pasajeros externos se validan correctamente

Escenario 2: Usuario ORGANIZADOR - Configuración "Permitir invitar viajeros externos" INACTIVA
Acción: Organizador intenta agregar pasajeros para el viaje
Resultado: SOLO lista desplegable de empleados disponible
Validar:
- NO hay opción "Invitar pasajero externo"
- Solo muestra lista desplegable de empleados de la empresa
- NO permite ingresar datos manualmente
- Mensaje informativo (opcional): "Solo puede seleccionar empleados de la empresa"
- Si intenta buscar pasajero no registrado: no lo encuentra

Escenario 3: Usuario VIAJERO (no Organizador)
Acción: Usuario viajero hace reserva
Resultado: Siempre reserva para sí mismo
Validar:
- Configuración "Permitir invitar viajeros externos" NO aplica
- No hay opción de seleccionar otros pasajeros
- Datos pre-cargados del usuario autenticado
- Solo puede modificar datos opcionales (programa viajero frecuente, etc.)
```

### **Centro de Costos en Checkout**
```
Escenario 1: Configuración "Restringir cambio de centros de costo" ACTIVA
Acción: Usuario intenta cambiar centro de costos en checkout
Resultado: Campo de centro de costos es SOLO LECTURA
Validar:
- No hay lista desplegable
- Solo muestra centro de costos asignado por defecto
- Usuario no puede modificar
- Mensaje informativo (opcional): "Centro de costos asignado por política corporativa"
- Facturación se genera con ese centro de costos

Escenario 2: Configuración "Restringir cambio de centros de costo" INACTIVA
Acción: Usuario selecciona centro de costos de lista desplegable
Resultado: Centro de costos cambia correctamente
Validar:
- Lista desplegable visible y funcional
- Muestra todos los centros de costo autorizados para el usuario
- Selección se guarda correctamente
- Facturación se genera con el centro de costos seleccionado
- Reportes reflejan el centro de costos correcto

Escenario 3: Usuario con múltiples centros de costo - Configuración INACTIVA
Acción: Usuario que maneja 3+ proyectos selecciona centro de costos
Resultado: Puede elegir el centro de costos apropiado para el viaje
Validar:
- Lista muestra TODOS los centros autorizados (no solo el predeterminado)
- Usuario puede cambiar de centro según el propósito del viaje
- Sistema valida que el centro seleccionado esté activo y autorizado
- Confirmación muestra claramente el centro de costos seleccionado
```

### **Política de Reservas - Justificación de Excepciones**
```
Escenario 1: Usuario cumple TODAS las políticas configuradas
Acción: Usuario completa checkout con vuelo que cumple políticas corporativas
Resultado: Flujo normal sin interrupciones
Validar:
- NO aparece campo "Justificación de excepción"
- Usuario puede continuar directo al pago
- Reserva se marca como "Cumple políticas corporativas"
- Sin validaciones adicionales

Escenario 2: Usuario NO cumple UNA O MÁS políticas - Campo obligatorio
Acción: Usuario selecciona vuelo que viola política (ej: precio mayor al permitido)
Resultado: Campo "Justificación de excepción" aparece como OBLIGATORIO
Validar:
- Sistema detecta automáticamente la violación de política
- Campo de texto "Justificación de excepción" visible y obligatorio
- Placeholder indica: "Explique por qué necesita hacer esta reserva sin cumplir las políticas"
- Contador de caracteres visible (mínimo requerido)
- Botón "Proceder al Pago" deshabilitado hasta completar justificación
- Mensaje claro: "Esta reserva no cumple con: [POLÍTICA VIOLADA]"

Escenario 3: Intento de justificación insuficiente
Acción: Usuario escribe texto muy corto o genérico (ej: "urgente")
Resultado: Sistema rechaza justificación
Validar:
- Mensaje de error: "La justificación debe tener al menos [X] caracteres"
- Mensaje de error: "Por favor proporcione una justificación detallada y específica"
- Campo se marca en rojo
- Usuario no puede continuar
- Sugerencia: "Incluya razón de negocio, contexto y necesidad específica"

Escenario 4: Justificación válida ingresada
Acción: Usuario escribe justificación completa y específica (>50 caracteres, con contexto)
Resultado: Sistema acepta justificación
Validar:
- Campo pasa validación (borde verde)
- Botón "Proceder al Pago" se habilita
- Justificación queda registrada en reserva
- Usuario puede continuar al pago

Escenario 5: Aprobador revisa reserva con excepción a política
Acción: Aprobador accede a reserva pendiente que tiene excepción
Resultado: Ve claramente la justificación del usuario
Validar:
- Panel de aprobación muestra alerta: "Esta reserva no cumple políticas corporativas"
- Políticas violadas listadas claramente
- Justificación del usuario visible y legible
- Aprobador puede decidir aprobar o rechazar considerando la justificación
- Comentario del aprobador puede hacer referencia a la justificación

Escenario 6: Reportes y auditoría de excepciones
Acción: Administrador consulta reportes de cumplimiento
Resultado: Puede filtrar y revisar todas las excepciones
Validar:
- Reporte muestra reservas con excepciones a políticas
- Cada excepción incluye: política violada, justificación, aprobador, decisión
- Filtros por tipo de política, fecha, usuario, aprobador
- Exportable para análisis corporativo
- Estadísticas de cumplimiento vs. excepciones
```

---

## ✅ CHECKLIST DE VALIDACIÓN COMPLETA

**Antes de dar OK a un caso de prueba de vuelos CORPORATIVO USD:**

- [ ] Título con formato: `[CORP-USD] Vuelos - [Escenario] - [Proveedor] - [Variante]`
- [ ] Descriptions incluye las 20 imágenes del flujo (completo con aprobación y emisión)
- [ ] Considerations con criterios claros incluyendo aprobación y emisión
- [ ] Pasos inician desde LOGIN
- [ ] Todos los pasos tienen resultado esperado
- [ ] Validaciones críticas incluidas (precios en USD, centro costos, etc.)
- [ ] Usuario tiene UN tipo de flujo de aprobación asignado por administrador (Simple O Serial)
- [ ] Aprobador(es) visible(s) en el checkout antes del pago
- [ ] Validar configuración "Restringir cambio de aprobador":
  - [ ] Si ACTIVA: Campo solo lectura, usuario no puede cambiar
  - [ ] Si INACTIVA: Lista desplegable funcional, usuario puede seleccionar otro aprobador
- [ ] Validar configuración "Restringir cambio de centros de costo":
  - [ ] Si ACTIVA: Campo solo lectura, muestra centro asignado
  - [ ] Si INACTIVA: Lista desplegable funcional con centros autorizados
- [ ] Validar Política de Reservas (si configurada):
  - [ ] Si CUMPLE políticas: Flujo normal sin justificación
  - [ ] Si NO CUMPLE políticas: Campo "Justificación de excepción" obligatorio
  - [ ] Validar mínimo de caracteres en justificación
  - [ ] Validar que justificación sea específica y con contexto
  - [ ] Justificación visible para aprobador
  - [ ] Trazabilidad en admin y reportes
- [ ] **PASO DE APROBACIÓN incluido y validado:**
  - [ ] Estado PENDIENTE DE APROBACIÓN después del pago
  - [ ] Notificación al(los) aprobador(es)
  - [ ] Tipo de aprobación especificado claramente (Serial O Simple, no ambos)
  - [ ] Si es Serial: validar orden secuencial y rechazo bloqueante
  - [ ] Si es Simple: validar aprobación única
  - [ ] Trazabilidad de aprobación
- [ ] **PASO DE EMISIÓN incluido y validado:**
  - [ ] Emisión solo después de aprobación completa (estado APROBADA)
  - [ ] Agente valida aprobaciones en administrador
  - [ ] Agente hace clic en botón "Emitir"
  - [ ] Agente selecciona "Tarjeta corporativa asociada a la empresa"
  - [ ] Agente selecciona tarjeta específica
  - [ ] Agente hace clic en "Desencriptar tarjeta"
  - [ ] Sistema muestra datos completos de tarjeta (número, vencimiento, CVV, titular)
  - [ ] Agente ingresa a plataforma del proveedor
  - [ ] Agente ingresa datos de tarjeta manualmente
  - [ ] Agente envía pago a aerolínea/comercio
  - [ ] Confirmación de pago exitoso recibida
  - [ ] Agente emite en CASH (sin dispersión de fondos)
  - [ ] Número(s) de ticket generados correctamente
  - [ ] Agente registra ticket(s) en sistema
  - [ ] Estado cambia a EMITIDA
  - [ ] **Template de Emisión enviado:** Viajero recibe email automático con PNR, e-ticket, código de barras y políticas al correo registrado en perfil (verificar timestamp en trazabilidad)
  - [ ] Notificaciones simples enviadas: aprobador(es) y contabilidad
  - [ ] Trazabilidad completa: agente, fecha/hora, tarjeta utilizada, timestamp de email
- [ ] Prioridad definida (1-4)
- [ ] Proveedor específico mencionado
- [ ] **Configuración PAX:** SOLO adultos (1-9), NO niños, NO infantes
- [ ] Tipo de viaje claro (ida y vuelta, solo ida, multidestino)
- [ ] Tipo de usuario especificado (Viajero o Organizador)
- [ ] Si usuario es ORGANIZADOR, validar configuración "Permitir invitar viajeros externos":
  - [ ] Si ACTIVA: Puede invitar pasajeros externos O seleccionar de lista de empleados
  - [ ] Si INACTIVA: Solo puede seleccionar de lista de empleados de la empresa
- [ ] Si usuario es VIAJERO: Reserva para sí mismo, configuración no aplica
- [ ] Validación de facturación corporativa
- [ ] Validación de notificaciones en cada etapa
- [ ] Validación en panel admin con trazabilidad completa
- [ ] **Modificación de reserva:** Validar que NO existe opción de modificar (ni botón ni funcionalidad)
- [ ] **Cancelación - Restricción de rol:** Validar que usuario (Viajero/Organizador) NO tiene botón "Cancelar" (solo Agente puede ejecutar)
- [ ] **Cancelación antes de emisión:** Validar que Agente ejecuta cancelación sin penalización, reembolso completo, usuario solo solicita
- [ ] **Cancelación después de emisión:** Validar que Agente consulta políticas, informa usuario, usuario confirma, Agente ejecuta, proceso de reembolso según políticas

---

**Última actualización:** 22 de enero de 2026  
**Versión:** 1.0  
**Estado:** Documentación completa - URL portal definitiva confirmada
