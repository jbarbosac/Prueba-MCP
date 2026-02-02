# 🛫 SANTANDER - FLUJO E2E VUELOS

**Portal:** Santander  
**Producto:** Vuelos  
**Prefijo:** [SANT]  
**Modelo:** B2B2C (Fidelity)  

---

## 📋 INFORMACIÓN GENERAL

### PROVEEDOR(ES):
**⚠️ PENDIENTE DEFINIR:**
- Proveedor principal: [AGGREGATOR NETACTICA / AGGREGATOR SABRE / SABRE EDIFACT / Otro]
- Configuración de dispersión de fondos
- GDS utilizado

### TECNOLOGÍA:
**⚠️ PENDIENTE DEFINIR:**
- Framework frontend: [Angular / React / Otro]
- Versión: [Por definir]

### MODELO DE PAGO:
**⚠️ PENDIENTE DEFINIR:**
```
Opción A: 100% PUNTOS SANTANDER
Opción B: X% PUNTOS + Y% TARJETA (slider)
Opción C: Puntos + Tarjeta (proporciones fijas)
+ Fee de procesamiento (si aplica)
```

---

## 🔄 FLUJO E2E COMPLETO

### PASO 1: LOGIN
**Pantalla:** Login Santander  
**URL:** [Por definir]

**Acciones:**
1. Navegar a URL del portal
2. Ingresar credenciales de cliente Santander
3. Hacer clic en botón "Iniciar sesión"

**Validaciones:**
- ✅ Credenciales correctas permiten acceso
- ✅ Credenciales incorrectas muestran mensaje de error claro
- ✅ Saldo de puntos visible después del login
- ✅ Redirección a página principal/marketplace

---

### PASO 2: HOME / SELECCIÓN DE PRODUCTO
**Pantalla:** Home del marketplace

**Acciones:**
1. Verificar que la página principal carga correctamente
2. Localizar sección/card de Vuelos
3. Hacer clic en "Vuelos" o botón de búsqueda de vuelos

**Validaciones:**
- ✅ Branding de Santander visible en header/footer
- ✅ Saldo de puntos actualizado visible
- ✅ Todos los productos disponibles (Vuelos, Autos, Hoteles, Actividades, Disney)
- ✅ Navegación intuitiva y funcional

---

### PASO 3: BÚSQUEDA DE VUELOS
**Pantalla:** Búsqueda de vuelos

**Campos obligatorios:**
- Origen (ciudad/aeropuerto)
- Destino (ciudad/aeropuerto)
- Fecha de ida
- Fecha de vuelta (si es ida y vuelta)
- Número de pasajeros (adultos, niños, infantes)
- Clase (Económica / Ejecutiva / Primera)

**Acciones:**
1. Ingresar ciudad/aeropuerto de origen
2. Ingresar ciudad/aeropuerto de destino
3. Seleccionar tipo de vuelo: Ida y vuelta / Solo ida / Multidestino
4. Seleccionar fecha de ida
5. Seleccionar fecha de vuelta (si aplica)
6. Seleccionar número de pasajeros
7. Seleccionar clase de vuelo
8. Hacer clic en "Buscar vuelos"

**Validaciones:**
- ✅ Campos obligatorios tienen validación de presencia
- ✅ Origen y destino no pueden ser iguales
- ✅ Fecha de ida no puede ser anterior a hoy
- ✅ Fecha de vuelta debe ser posterior a fecha de ida
- ✅ Máximo de pasajeros permitido (típicamente 9)
- ✅ Mensajes de error claros y descriptivos
- ✅ Botón "Buscar" deshabilitado hasta completar campos obligatorios

---

### PASO 4: DISPONIBILIDAD DE VUELOS
**Pantalla:** Resultados de búsqueda

**Elementos a mostrar:**
- Lista de vuelos disponibles con:
  - Aerolínea
  - Horario de salida/llegada
  - Duración del vuelo
  - Número de escalas
  - Precio en puntos (o puntos + dinero según modelo)
  - Disponibilidad de asientos

**Acciones:**
1. Revisar resultados de búsqueda
2. Aplicar filtros (si disponibles):
   - Aerolínea
   - Horario de salida
   - Número de escalas (directo, 1 escala, 2+ escalas)
   - Precio
3. Ordenar resultados (menor precio, menor duración, etc.)
4. Seleccionar vuelo de ida
5. Seleccionar vuelo de vuelta (si es ida y vuelta)
6. Hacer clic en "Continuar" o "Seleccionar"

**Validaciones:**
- ✅ Al menos un resultado disponible o mensaje "No se encontraron vuelos"
- ✅ Información completa y consistente de cada vuelo
- ✅ Filtros funcionan correctamente
- ✅ Precio en puntos calculado correctamente
- ✅ Verificación de puntos suficientes (advertencia si no hay suficientes)
- ✅ Botón "Continuar" habilitado solo después de selección

---

### PASO 5: UPSELLS (OPCIONAL)
**Pantalla:** Servicios adicionales

**⚠️ PENDIENTE DEFINIR:** Si Santander ofrece upsells

**Opciones comunes:**
- Selección de asientos
- Equipaje adicional
- Seguro de viaje
- Priority boarding
- Upgrade de clase

**Acciones:**
1. Revisar servicios adicionales disponibles
2. Seleccionar servicios deseados (opcional)
3. Hacer clic en "Continuar"

**Validaciones:**
- ✅ Costo adicional en puntos mostrado claramente
- ✅ Servicios opcionales, no obligatorios
- ✅ Total actualizado con servicios seleccionados

---

### PASO 6: RESUMEN DE RESERVA
**Pantalla:** Resumen previo a checkout

**Información a mostrar:**
- Detalle completo del vuelo de ida y vuelta
- Servicios adicionales seleccionados (si aplica)
- Puntos totales a canjear
- Dinero adicional (si modelo es mixto)
- Fee de procesamiento (si aplica)

**Acciones:**
1. Revisar resumen completo
2. Verificar que toda la información sea correcta
3. Modificar si es necesario (volver a búsqueda)
4. Hacer clic en "Continuar al checkout" o "Reservar"

**Validaciones:**
- ✅ Consistencia de datos con selecciones anteriores
- ✅ Cálculo correcto de puntos totales
- ✅ Políticas de cancelación/cambios mostradas
- ✅ Términos y condiciones visibles
- ✅ Opción de volver atrás funcional

---

### PASO 7: CHECKOUT - DATOS DE PASAJEROS
**Pantalla:** Formulario de datos de pasajeros

**Campos obligatorios por pasajero:**
- Nombre(s) completo(s)
- Apellido(s) completo(s)
- Tipo de documento (Pasaporte, Cédula, etc.)
- Número de documento
- Nacionalidad
- Fecha de nacimiento
- Género
- Email
- Teléfono
- País de residencia

**Campos opcionales:**
- Programa de viajero frecuente
- Preferencias dietéticas (si aplica)
- Asistencia especial (silla de ruedas, etc.)

**Acciones:**
1. Ingresar datos del primer pasajero
2. Ingresar datos de pasajeros adicionales (si aplican)
3. Aceptar términos y condiciones
4. Aceptar política de tratamiento de datos
5. Hacer clic en "Continuar" o "Finalizar reserva"

**Validaciones:**
- ✅ Todos los campos obligatorios completados
- ✅ Formato de email válido
- ✅ Formato de teléfono válido
- ✅ Fecha de nacimiento coherente con tipo de pasajero (adulto/niño/infante)
- ✅ Número de documento único por pasajero
- ✅ Términos y condiciones aceptados obligatoriamente
- ✅ Botón deshabilitado hasta completar todo

---

### PASO 8: PAGO (SI APLICA)
**Pantalla:** Método de pago

**⚠️ PENDIENTE DEFINIR:** Proceso de pago según modelo

**Modelo A (100% Puntos):**
- Confirmación directa de débito de puntos
- No requiere tarjeta de crédito

**Modelo B/C (Puntos + Tarjeta):**
- Ingreso de datos de tarjeta de crédito:
  - Número de tarjeta
  - Fecha de vencimiento
  - CVV
  - Nombre del titular
- Pasarela de pago: [Por definir]

**Acciones:**
1. Seleccionar método de pago (si hay opciones)
2. Ingresar datos de tarjeta (si aplica)
3. Aceptar débito de puntos
4. Hacer clic en "Pagar" o "Confirmar reserva"

**Validaciones:**
- ✅ Saldo de puntos suficiente verificado
- ✅ Datos de tarjeta válidos (si aplica)
- ✅ Conexión segura (HTTPS)
- ✅ Tokenización de datos de pago
- ✅ Mensaje de procesamiento visible
- ✅ Timeout adecuado (no cerrar prematuramente)

---

### PASO 9: CONFIRMACIÓN DE RESERVA
**Pantalla:** Confirmación exitosa

**Información a mostrar:**
- Número de reserva/PNR
- Código de confirmación
- Resumen del vuelo
- Datos de pasajeros
- Puntos debitados
- Estado de la reserva: CONFIRMADA / EMITIDA
- Instrucciones siguientes (check-in, documentación, etc.)

**Acciones:**
1. Visualizar confirmación completa
2. Descargar voucher/comprobante (si disponible)
3. Recibir email de confirmación
4. Opción de reservar otro producto

**Validaciones:**
- ✅ Número de reserva único generado
- ✅ PNR válido del proveedor
- ✅ Email de confirmación enviado al pasajero
- ✅ Puntos debitados correctamente de la cuenta
- ✅ Datos completos y correctos en la confirmación
- ✅ Voucher descargable (PDF)

---

### PASO 10: VALIDACIÓN EN ADMIN
**Pantalla:** Panel de administración

**Acciones:**
1. Hacer login en panel de admin
2. Buscar reserva por número de reserva o PNR
3. Verificar estado de la reserva
4. Verificar todos los datos registrados

**Validaciones:**
- ✅ Reserva existe en el sistema
- ✅ Estado correcto: CONFIRMADA o EMITIDA
- ✅ Proveedor correcto registrado
- ✅ Datos de pasajeros completos
- ✅ Datos de vuelos (origen, destino, fechas, horarios)
- ✅ Puntos debitados registrados
- ✅ Pago procesado (si aplica tarjeta)
- ✅ Trazabilidad completa del flujo

---

### PASO 11: EMISIÓN (SI ES MANUAL)
**Pantalla:** Panel de admin - Gestión de reservas

**⚠️ PENDIENTE DEFINIR:** Si el proceso es automático o manual

**Si emisión es MANUAL:**

**Acciones:**
1. Localizar reserva en estado CONFIRMADA
2. Verificar que débito de puntos fue exitoso
3. Verificar que pago con tarjeta fue procesado (si aplica)
4. Hacer clic en "Emitir"
5. Confirmar emisión

**Validaciones:**
- ✅ Cambio de estado de CONFIRMADA a EMITIDA
- ✅ Tickets electrónicos generados
- ✅ Email de emisión enviado al pasajero
- ✅ Registro de fecha y hora de emisión
- ✅ Usuario que emitió registrado (trazabilidad)

**Si emisión es AUTOMÁTICA:**
- ✅ Estado EMITIDA inmediato después de confirmación
- ✅ No requiere intervención manual
- ✅ Proceso transparente para el usuario

---

## 🎯 CASOS DE PRUEBA SUGERIDOS

### CASOS BÁSICOS:

1. **[SANT] Vuelos - Ida y vuelta - [Proveedor] - 1 adulto - Económica**
2. **[SANT] Vuelos - Solo ida - [Proveedor] - 1 adulto - Económica**
3. **[SANT] Vuelos - Ida y vuelta - [Proveedor] - 2 adultos - Ejecutiva**
4. **[SANT] Vuelos - Ida y vuelta - [Proveedor] - 1 adulto + 1 niño**
5. **[SANT] Vuelos - Ida y vuelta - [Proveedor] - 1 adulto + 1 infante**

### CASOS INTERMEDIOS:

6. **[SANT] Vuelos - Ida y vuelta - [Proveedor] - Vuelo directo**
7. **[SANT] Vuelos - Ida y vuelta - [Proveedor] - Con 1 escala**
8. **[SANT] Vuelos - Ida y vuelta - [Proveedor] - Con equipaje adicional**
9. **[SANT] Vuelos - Ida y vuelta - [Proveedor] - Con selección de asientos**
10. **[SANT] Vuelos - Multidestino - [Proveedor] - 3 tramos**

### CASOS AVANZADOS:

11. **[SANT] Vuelos - Saldo de puntos insuficiente - Error controlado**
12. **[SANT] Vuelos - Error de proveedor - Manejo de excepciones**
13. **[SANT] Vuelos - Timeout en búsqueda - Reintento**
14. **[SANT] Vuelos - Cambio de disponibilidad durante reserva**
15. **[SANT] Vuelos - Validación de documentos expirados**

### CASOS DE REGRESIÓN:

16. **[SANT] Vuelos - Vuelo internacional - Validación de pasaportes**
17. **[SANT] Vuelos - Grupo grande - 9 pasajeros**
18. **[SANT] Vuelos - Cancelación de reserva confirmada**
19. **[SANT] Vuelos - Modificación de datos de pasajero pre-emisión**
20. **[SANT] Vuelos - Reembolso de puntos por cancelación**

---

## 🔧 CONFIGURACIÓN TÉCNICA

### PROVEEDORES:
**⚠️ PENDIENTE DEFINIR:**
- Credenciales de proveedor(es)
- Ambiente de testing (sandbox)
- Códigos de aeropuerto válidos para pruebas
- Configuración de mock para casos edge

### USUARIOS DE PRUEBA:
**⚠️ PENDIENTE DEFINIR:**
- Usuario con saldo de puntos alto (100,000+)
- Usuario con saldo de puntos bajo (5,000)
- Usuario sin puntos
- Usuario VIP (si aplica)

### DATOS DE PRUEBA:
**Rutas comunes para testing:**
- Nacional: [Por definir según país]
- Internacional: [Por definir]
- Vuelos directos disponibles
- Vuelos con escalas disponibles

---

## 📊 IMÁGENES DE REFERENCIA

**⚠️ PENDIENTE CAPTURAR:**

Capturas de pantalla de cada paso del flujo:
1. `Home-SANT.png` - Página principal
2. `Home-vuelos-SANT.png` - Sección de vuelos
3. `Busqueda-vuelos-SANT.png` - Formulario de búsqueda
4. `Disponibilidad-vuelos-SANT.png` - Resultados de búsqueda
5. `Upsell-vuelos-SANT.png` - Servicios adicionales (si aplica)
6. `Resumen-vuelos-SANT.png` - Resumen de reserva
7. `Checkout-vuelos-SANT.png` - Datos de pasajeros
8. `Pago-vuelos-SANT.png` - Método de pago
9. `Confirmacion-vuelos-SANT.png` - Confirmación exitosa
10. `Admin-SANT.png` - Panel de administración
11. `Reserva-SANT.png` - Detalle de reserva en admin

**Las imágenes DEBEN incluirse en el campo Descriptions de cada test case.**

---

## 📚 REFERENCIAS

📋 [SANTANDER_COMMON_RULES.md](../../../shared/Reglas Marketplace/SANTANDER_COMMON_RULES.md) - Reglas comunes Santander  
📋 [SHARED_QA_RULES.md](../../../shared/SHARED_QA_RULES.md) - Fundamentos ISTQB y Azure DevOps  

---

**Versión:** 1.0.0  
**Fecha de creación:** 2026-01-23  
**Estado:** ⚠️ PENDIENTE COMPLETAR INFORMACIÓN TÉCNICA  
