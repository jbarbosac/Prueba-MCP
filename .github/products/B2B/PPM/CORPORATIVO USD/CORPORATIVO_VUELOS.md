# 🛫 CORPORATIVO USD - VUELOS

> Flujo End-to-End completo para reserva de vuelos corporativos en USD

---

## 📋 INFORMACIÓN GENERAL

**Portal:** CORPORATIVO USD  
**Producto:** Vuelos  
**Modelo:** B2B (Business to Business)  
**Moneda:** USD (Dólares)  
**Prefijo:** `[CORP-USD]`  
**Cliente:** Empresas corporativas  

**Tecnología:**  
- [Pendiente definir]

**Proveedores:**  
- [Pendiente definir - puede incluir: SABRE, NETACTICA, Amadeus, etc.]

---

## 🎯 CARACTERÍSTICAS DEL PRODUCTO

### **Modelo de Negocio**

**CORPORATIVO USD es un modelo B2B enfocado en clientes corporativos:**

1. **Autenticación:** Login corporativo con credenciales empresariales
2. **Búsqueda:** Precios en USD, políticas corporativas aplicadas
3. **Selección:** Vuelos disponibles según acuerdos corporativos
4. **Checkout:** Facturación empresarial, centro de costos
5. **Emisión:** [Pendiente definir: Automática/Manual]
6. **Confirmación:** PNR generado, notificaciones a viajero y aprobador

---

## 🔄 FLUJO END-TO-END COMPLETO

### **PASO 1: LOGIN CORPORATIVO**

**Acción:**
```
1. Ingresar a la URL: [URL_CORPORATIVO_USD]
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
   - Centro de costos
4. Aceptar términos y condiciones
5. Hacer clic en "Proceder al Pago"
```

**Validaciones:**
- ✅ Campos obligatorios validados
- ✅ Formato de documento correcto
- ✅ Fechas válidas (mayoría de edad para conductor, etc.)
- ✅ Email con formato válido
- ✅ Datos de facturación corporativa completos
- ✅ Centro de costos válido
- ✅ Términos aceptados

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

**Acción:**
```
1. Revisar método de pago corporativo:
   - [Tarjeta corporativa]
   - [Cuenta corporativa]
   - [Crédito empresarial]
   - [Otro método según modelo]
2. Completar datos de pago:
   - [Campos según método de pago]
3. Revisar precio final en USD
4. Hacer clic en "Confirmar Pago"
5. [Esperar procesamiento de pago]
```

**Validaciones:**
- ✅ Método de pago corporativo disponible
- ✅ Datos de pago válidos
- ✅ Precio final correcto en USD
- ✅ Proceso de pago seguro (HTTPS)
- ✅ Feedback de procesamiento (loading, progress)

**Resultado Esperado:**
```html
<p>Pago procesado exitosamente:</p>
<ul>
  <li>Método: [MÉTODO_PAGO]</li>
  <li>Monto: USD [TOTAL]</li>
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

**[Pendiente definir proveedores específicos]**

Ejemplos según proveedores comunes:

```
[CORP-USD] Vuelos - Ida y vuelta - SABRE - 1 adulto
[CORP-USD] Vuelos - Ida y vuelta - NETACTICA - 1 adulto
[CORP-USD] Vuelos - Ida y vuelta - Amadeus - 1 adulto
```

---

## 🚨 VALIDACIONES CRÍTICAS

### **1. AUTENTICACIÓN CORPORATIVA**
- ✅ Solo usuarios corporativos autorizados
- ✅ Permisos según rol (viajero, aprobador, admin)
- ✅ Centro de costos válido para el usuario
- ✅ Políticas corporativas activas

### **2. BÚSQUEDA Y DISPONIBILIDAD**
- ✅ Precios SIEMPRE en USD
- ✅ Políticas corporativas aplicadas (restricciones de aerolíneas, clases, etc.)
- ✅ Solo vuelos corporativos disponibles
- ✅ Manejo correcto de errores (sin resultados, timeout)

### **3. CHECKOUT Y PAGO**
- ✅ Datos de pasajeros completos y válidos
- ✅ Facturación a nombre de la empresa
- ✅ Centro de costos obligatorio
- ✅ Método de pago corporativo funcional
- ✅ Términos y condiciones corporativos aceptados

### **4. CONFIRMACIÓN**
- ✅ PNR generado correctamente
- ✅ Reserva confirmada en sistema
- ✅ Notificaciones enviadas:
  - ✉️ Viajero
  - ✉️ Aprobador (si aplica)
  - ✉️ Facturación/Contabilidad
- ✅ Comprobante descargable
- ✅ Trazabilidad en admin

### **5. EMISIÓN DE TICKET**
**[Pendiente definir proceso: Automático/Manual]**

- ✅ Ticket emitido correctamente
- ✅ Números de ticket válidos
- ✅ Información consistente con reserva

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
  <li><strong>Checkout:</strong> Datos completos, validaciones OK, centro de costos asignado</li>
  <li><strong>Pago:</strong> Pago corporativo procesado exitosamente</li>
  <li><strong>Confirmación:</strong> PNR generado, notificaciones enviadas, comprobante disponible</li>
  <li><strong>Admin:</strong> Reserva visible en panel con información completa</li>
</ul>
```

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

## 🔄 FLUJO DE APROBACIÓN (SI APLICA)

**[Pendiente definir si el modelo requiere aprobación de reservas]**

Si el modelo corporativo requiere aprobación:

```
1. Viajero crea reserva → Estado: PENDIENTE APROBACIÓN
2. Notificación enviada a aprobador
3. Aprobador revisa en panel admin
4. Aprobador APRUEBA o RECHAZA
5. Si APROBADO → Procesar pago y emisión
6. Si RECHAZADO → Notificar viajero, reserva cancelada
```

**Validaciones adicionales:**
- ✅ Estado PENDIENTE visible para viajero
- ✅ Email de solicitud enviado a aprobador
- ✅ Aprobador puede ver detalles completos
- ✅ Botones APROBAR/RECHAZAR funcionan
- ✅ Notificaciones de decisión enviadas
- ✅ Trazabilidad de aprobaciones en historial

---

## 📝 NOTAS IMPORTANTES

1. **Prioridad del Producto:**
   - Vuelos es el ÚNICO producto disponible en CORPORATIVO USD
   - No crear casos de Hoteles, Autos, Actividades o Disney

2. **Moneda:**
   - TODOS los precios deben mostrarse en USD
   - No hay conversión de monedas

3. **Facturación:**
   - SIEMPRE a nombre de la empresa
   - Centro de costos OBLIGATORIO
   - RUC/NIT/Tax ID requerido

4. **Políticas Corporativas:**
   - Pueden limitar aerolíneas disponibles
   - Pueden limitar clases de vuelo
   - Pueden requerir aprobación para montos altos

5. **Proveedores:**
   - [Pendiente definir lista específica]
   - Documentar según configuración final

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
Validar: Reserva NO confirmada, datos preservados
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

---

## ✅ CHECKLIST DE VALIDACIÓN COMPLETA

**Antes de dar OK a un caso de prueba de vuelos CORPORATIVO USD:**

- [ ] Título con formato: `[CORP-USD] Vuelos - [Escenario] - [Proveedor] - [Variante]`
- [ ] Descriptions incluye las 11 imágenes del flujo
- [ ] Considerations con criterios claros
- [ ] Pasos inician desde LOGIN
- [ ] Todos los pasos tienen resultado esperado
- [ ] Validaciones críticas incluidas (precios en USD, centro costos, etc.)
- [ ] Prioridad definida (1-4)
- [ ] Proveedor específico mencionado
- [ ] Configuración PAX específica (1, 2, 3, etc.)
- [ ] Tipo de viaje claro (ida y vuelta, solo ida, multidestino)
- [ ] Validación de facturación corporativa
- [ ] Validación de notificaciones
- [ ] Validación en panel admin (si aplica)

---

**Última actualización:** 22 de enero de 2026  
**Versión:** 1.0  
**Estado:** Inicial - Pendiente completar configuración específica
