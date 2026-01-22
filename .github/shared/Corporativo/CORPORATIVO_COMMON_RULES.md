# REGLAS COMUNES CORPORATIVO USD

> Documento central de reglas, validaciones y modelo de negocio para CORPORATIVO USD

---

## 🎯 IDENTIFICACIÓN DEL PORTAL

**Nombre completo:** CORPORATIVO USD  
**Tipo de cliente:** B2B (Business to Business)  
**Moneda:** USD (Dólares)  
**País/Región:** [Pendiente definir]  
**URL:** [Pendiente definir]  
**Prefijo obligatorio:** `[CORP-USD]`  
**Célula:** [Pendiente asignar]  

---

## 📦 PRODUCTOS DISPONIBLES

| Producto | Disponible | Tecnología | Proveedores |
|----------|-----------|------------|-------------|
| **Vuelos** | ✅ SÍ | [Pendiente] | [Pendiente] |
| **Hoteles** | ❌ NO | - | - |
| **Autos** | ❌ NO | - | - |
| **Actividades** | ❌ NO | - | - |
| **Disney** | ❌ NO | - | - |

**IMPORTANTE:**  
CORPORATIVO USD es un modelo especializado SOLO en vuelos corporativos.  
No generar casos de prueba para otros productos.

---

## 💼 MODELO DE NEGOCIO

### **Características Principales**

**CORPORATIVO USD es un portal B2B enfocado en clientes corporativos:**

1. **Cliente:** Empresas (no consumidores finales)
2. **Usuario:** Empleados de empresas con permisos corporativos
3. **Moneda:** Todas las transacciones en USD
4. **Productos:** Solo Vuelos (especializado)
5. **Facturación:** Empresarial (RUC/NIT/Tax ID obligatorio)
6. **Centro de Costos:** Obligatorio para trazabilidad interna
7. **Aprobaciones:** [Pendiente definir si requiere flujo de aprobación]

### **Diferenciadores vs Otros Modelos**

| Aspecto | CORPORATIVO USD | PM/BGR (B2B2C) | AVASA (B2C) |
|---------|----------------|----------------|-------------|
| **Tipo** | B2B | B2B2C | B2C |
| **Cliente** | Empresas | Tarjetahabientes | Consumidor final |
| **Autenticación** | Corporativa | Personal | Personal/Guest |
| **Moneda** | USD | Millas (+USD en slider) | Pesos/USD |
| **Productos** | Solo Vuelos | 5 productos | Múltiples |
| **Facturación** | Empresarial | Personal | Personal |
| **Centro Costos** | Obligatorio | No aplica | No aplica |
| **Aprobaciones** | Posible | No | No |

### **Flujo General del Negocio**

```
1. Empresa se registra en portal corporativo
2. Empresa crea usuarios (empleados autorizados)
3. Empresa configura:
   - Centros de costos
   - Políticas de viaje (aerolíneas, clases, montos)
   - Aprobadores (si aplica)
   - Métodos de pago corporativos
4. Empleado hace login con credenciales corporativas
5. Empleado busca y reserva vuelo
6. Sistema valida políticas corporativas
7. [OPCIONAL] Aprobador revisa y aprueba reserva
8. Sistema procesa pago corporativo
9. Sistema emite ticket
10. Sistema genera factura a nombre de empresa
11. Sistema envía notificaciones:
    - Viajero (empleado)
    - Aprobador (si aplica)
    - Contabilidad/Facturación
```

---

## 🔐 AUTENTICACIÓN Y PERMISOS

### **Tipos de Usuario**

1. **Viajero (Empleado):**
   - Puede buscar y reservar vuelos
   - Ve solo sus propias reservas
   - Sujeto a políticas corporativas
   - Debe asignar centro de costos

2. **Aprobador (Manager):**
   - Puede aprobar/rechazar reservas (si aplica)
   - Ve reservas de su equipo
   - Notificado de solicitudes pendientes

3. **Administrador Corporativo:**
   - Gestiona usuarios de la empresa
   - Configura políticas y centros de costos
   - Ve todas las reservas de la empresa
   - Accede a reportes y facturación

### **Validaciones de Autenticación**

- ✅ Login con credenciales corporativas (usuario/contraseña)
- ✅ [OPCIONAL] Código de empresa
- ✅ [OPCIONAL] Autenticación de dos factores (2FA)
- ✅ Sesión con timeout por inactividad
- ✅ Permisos según rol asignado
- ✅ Validación de empresa activa

---

## 💰 MODELO DE PAGO

### **Métodos de Pago Corporativos**

**[Pendiente definir métodos específicos disponibles]**

Posibles opciones:
- Tarjeta corporativa
- Cuenta corporativa (crédito empresarial)
- Transferencia bancaria (post-pago)
- Débito directo a cuenta empresarial

### **Facturación**

- ✅ Factura a nombre de la empresa (NO del empleado)
- ✅ RUC/NIT/Tax ID obligatorio
- ✅ Dirección fiscal requerida
- ✅ Centro de costos en factura
- ✅ Desglose de servicios
- ✅ Formato según legislación local

### **Centro de Costos**

**OBLIGATORIO en todas las reservas:**
- ✅ Debe ser centro de costos válido de la empresa
- ✅ Usuario solo ve centros autorizados para su rol
- ✅ Se incluye en factura para trazabilidad
- ✅ Reportes agrupados por centro de costos

---

## 🛫 ESTRUCTURA DE PROVEEDORES

### **Vuelos**

**[Pendiente definir proveedores específicos]**

Posibles proveedores:
- SABRE (GDS)
- Amadeus (GDS)
- AGGREGATOR NETACTICA
- AGGREGATOR SABRE
- Travelport (GDS)

**Configuración por proveedor:**
- [Pendiente documentar por proveedor cuando se defina]

---

## ✅ VALIDACIONES COMUNES

### **1. Validaciones de Búsqueda**

- ✅ Origen y destino obligatorios
- ✅ Fechas futuras (no pasadas)
- ✅ Fecha regreso >= fecha ida (ida y vuelta)
- ✅ Cantidad de pasajeros entre 1 y 9
- ✅ Políticas corporativas aplicadas automáticamente
- ✅ Solo vuelos permitidos por políticas

### **2. Validaciones de Disponibilidad**

- ✅ Precios SIEMPRE en USD
- ✅ Información completa de vuelos (horarios, escalas, etc.)
- ✅ Aerolíneas permitidas según políticas
- ✅ Clases permitidas según políticas
- ✅ Rango de precios según políticas (si aplica)
- ✅ Manejo de errores (sin resultados, timeout)

### **3. Validaciones de Checkout**

**Datos de Pasajeros:**
- ✅ Nombre completo (según documento de viaje)
- ✅ Tipo de documento válido (pasaporte para internacional)
- ✅ Número de documento formato correcto
- ✅ Fecha de nacimiento válida
- ✅ Nacionalidad
- ✅ Género

**Datos de Contacto:**
- ✅ Email corporativo válido (@empresa.com)
- ✅ Teléfono con formato válido

**Datos de Facturación:**
- ✅ Razón social de la empresa
- ✅ RUC/NIT/Tax ID válido
- ✅ Dirección fiscal completa
- ✅ **Centro de costos OBLIGATORIO**

**Términos y Condiciones:**
- ✅ Términos corporativos aceptados
- ✅ Políticas de cancelación claras

### **4. Validaciones de Pago**

- ✅ Método de pago corporativo válido
- ✅ Datos completos según método
- ✅ Monto en USD correcto
- ✅ Proceso seguro (HTTPS, certificados)
- ✅ Timeout configurado (no esperas infinitas)
- ✅ Manejo de errores (pago rechazado, timeout)

### **5. Validaciones de Confirmación**

- ✅ PNR generado (código de reserva)
- ✅ Estado de reserva: CONFIRMADA
- ✅ Información completa y correcta
- ✅ Notificaciones enviadas:
  - ✉️ Viajero (empleado)
  - ✉️ Aprobador (si aplica)
  - ✉️ Contabilidad/Facturación
- ✅ Comprobante descargable (PDF)
- ✅ Reserva visible en panel admin

### **6. Validaciones de Emisión**

**[Pendiente definir proceso: Automático/Manual]**

- ✅ Ticket emitido correctamente
- ✅ Número(s) de ticket generados
- ✅ Información consistente con reserva
- ✅ Notificación de emisión enviada

---

## 📋 FORMATO DE TÍTULOS DE CASOS DE PRUEBA

### **Estructura Obligatoria**

```
[CORP-USD] [Producto] - [Escenario] - [Proveedor] - [Configuración]
```

### **Ejemplos Válidos**

```
[CORP-USD] Vuelos - Ida y vuelta - SABRE - 1 adulto
[CORP-USD] Vuelos - Ida y vuelta - NETACTICA - 2 adultos
[CORP-USD] Vuelos - Solo ida - SABRE - 1 adulto + equipaje
[CORP-USD] Vuelos - Multidestino - Amadeus - 3 adultos
[CORP-USD] Vuelos - Ida y vuelta - SABRE - Clase ejecutiva
```

### **Componentes del Título**

1. **Prefijo:** `[CORP-USD]` - SIEMPRE obligatorio
2. **Producto:** `Vuelos` - Único producto disponible
3. **Escenario:**
   - `Ida y vuelta` - Round trip
   - `Solo ida` - One way
   - `Multidestino` - Multi-city
4. **Proveedor:** Nombre específico del proveedor (SABRE, NETACTICA, etc.)
5. **Configuración:** Variantes específicas
   - Cantidad de pasajeros: `1 adulto`, `2 adultos`, etc.
   - Clase: `Clase ejecutiva`, `Clase premium`
   - Extras: `+ equipaje`, `+ asientos`, etc.
   - Escalas: `1 escala`, `2 escalas`, `sin escalas`

---

## 🎯 CRITERIOS DE ACEPTACIÓN ESTÁNDAR

### **Template para Campo "Considerations"**

```html
<p><strong>Criterios de Aceptación:</strong></p>
<ul>
  <li><strong>Autenticación:</strong> Login corporativo exitoso con credenciales válidas de empleado autorizado</li>
  <li><strong>Búsqueda:</strong> Formulario captura datos correctamente, validaciones OK, políticas corporativas aplicadas</li>
  <li><strong>Disponibilidad:</strong> Resultados se muestran en USD, solo vuelos permitidos por políticas, información completa</li>
  <li><strong>Selección:</strong> Vuelo seleccionado correctamente, detalles completos visibles</li>
  <li><strong>Upselling:</strong> Opciones adicionales funcionan (si aplica), precio se actualiza dinámicamente</li>
  <li><strong>Resumen:</strong> Información completa y correcta, precio total en USD</li>
  <li><strong>Checkout:</strong> Datos de pasajeros completos, validaciones OK, centro de costos asignado, facturación empresarial</li>
  <li><strong>Pago:</strong> Método corporativo procesado exitosamente, monto correcto en USD</li>
  <li><strong>Confirmación:</strong> PNR generado, estado CONFIRMADA, notificaciones enviadas (viajero, aprobador, facturación)</li>
  <li><strong>Admin:</strong> Reserva visible en panel corporativo con información completa y centro de costos</li>
</ul>
```

---

## 📸 IMÁGENES DE REFERENCIA

### **Ubicación de Imágenes**

```
https://[DOMINIO]/images/CORPORATIVO/
```

### **Imágenes Obligatorias para Descriptions**

```html
<img src="https://[DOMINIO]/images/CORPORATIVO/Login-CORP.png" alt="Login Corporativo" />
<img src="https://[DOMINIO]/images/CORPORATIVO/Home-CORP.png" alt="Home Portal" />
<img src="https://[DOMINIO]/images/CORPORATIVO/Home-vuelos-CORP.png" alt="Widget Vuelos" />
<img src="https://[DOMINIO]/images/CORPORATIVO/Disponibilidad-vuelos-CORP.png" alt="Resultados" />
<img src="https://[DOMINIO]/images/CORPORATIVO/upsell-vuelos-CORP.png" alt="Upselling" />
<img src="https://[DOMINIO]/images/CORPORATIVO/Resumen-vuelos-CORP.png" alt="Resumen" />
<img src="https://[DOMINIO]/images/CORPORATIVO/Checkout-vuelos-CORP.png" alt="Checkout" />
<img src="https://[DOMINIO]/images/CORPORATIVO/Pago-CORP.png" alt="Pago" />
<img src="https://[DOMINIO]/images/CORPORATIVO/Confirmacion-vuelos-CORP.png" alt="Confirmación" />
<img src="https://[DOMINIO]/images/CORPORATIVO/Admin-CORP.png" alt="Panel Admin" />
<img src="https://[DOMINIO]/images/CORPORATIVO/Reserva-CORP.png" alt="Detalle Reserva" />
```

---

## 🚨 CASOS EDGE Y MANEJO DE ERRORES

### **Error: Sin Resultados**
```
Escenario: Búsqueda sin vuelos disponibles
Resultado: Mensaje claro "No hay vuelos disponibles para los criterios seleccionados"
Acción: Permitir modificar búsqueda
```

### **Error: Políticas Corporativas**
```
Escenario: Usuario intenta reservar vuelo no permitido por políticas
Resultado: Mensaje "Este vuelo no cumple con las políticas corporativas de su empresa"
Detalle: Especificar razón (aerolínea, clase, precio, etc.)
```

### **Error: Centro de Costos Inválido**
```
Escenario: Centro de costos no autorizado para usuario
Resultado: Mensaje "Centro de costos no válido"
Acción: Mostrar solo centros autorizados
```

### **Error: Pago Rechazado**
```
Escenario: Pago corporativo rechazado
Resultado: Mensaje específico del motivo
Acción: Permitir reintentar o cambiar método
Estado: Reserva NO confirmada, datos preservados
```

### **Error: Timeout de Proveedor**
```
Escenario: Proveedor no responde a tiempo
Resultado: Mensaje "El servicio está tardando más de lo esperado. Por favor, intente nuevamente"
Acción: Botón para reintentar
Validar: No crash, manejo graceful
```

### **Error: Usuario Sin Permisos**
```
Escenario: Usuario sin permisos intenta acceder a funcionalidad
Resultado: Mensaje "No tiene permisos para realizar esta acción"
Acción: Redirección o bloqueo apropiado
```

---

## 📊 PRIORIDADES DE CASOS DE PRUEBA

### **Prioridad 1 (Crítica)**
- Flujo completo E2E básico (ida y vuelta, 1 adulto)
- Autenticación corporativa
- Pago corporativo
- Emisión de ticket
- Facturación empresarial

### **Prioridad 2 (Alta)**
- Variantes de vuelos (solo ida, multidestino)
- Múltiples pasajeros
- Validaciones de políticas corporativas
- Centro de costos
- Notificaciones

### **Prioridad 3 (Media)**
- Diferentes clases de vuelo
- Upselling (equipaje, asientos, etc.)
- Diferentes proveedores
- Filtros de búsqueda
- Panel admin

### **Prioridad 4 (Baja)**
- Casos edge específicos
- Variaciones de UI/UX
- Combinaciones complejas
- Escenarios poco frecuentes

---

## 🔄 FLUJO DE APROBACIÓN (SI APLICA)

**[Pendiente definir si el modelo requiere aprobación]**

Si se implementa flujo de aprobación:

### **Estados de Reserva**

1. **PENDIENTE APROBACIÓN:** Reserva creada, esperando aprobador
2. **APROBADA:** Aprobador dio OK, proceder a pago/emisión
3. **RECHAZADA:** Aprobador rechazó, reserva cancelada
4. **CONFIRMADA:** Pago procesado, ticket emitido

### **Validaciones Adicionales**

- ✅ Notificación a aprobador cuando se crea reserva
- ✅ Aprobador puede ver detalle completo
- ✅ Botones APROBAR/RECHAZAR funcionales
- ✅ Campo comentarios para aprobador
- ✅ Notificación a viajero de decisión
- ✅ Historial de aprobaciones visible
- ✅ Timeout de aprobación (ej: 24-48 horas)

---

## 📝 CAMPOS AZURE DEVOPS

### **Campos Obligatorios**

```json
{
  "title": "[CORP-USD] [Título del caso]",
  "state": "Design",
  "priority": 1-4,
  "areaPath": "[ÁREA]",
  "iterationPath": "[ITERACIÓN]",
  "assignedTo": "[TESTER]",
  "description": "[HTML con imágenes]",
  "considerations": "[HTML con criterios]",
  "steps": [
    {
      "action": "<p>Paso 1...</p>",
      "expectedResult": "<p>Resultado esperado...</p>"
    }
  ]
}
```

### **Trazabilidad con HU**

- Si existe HU (Historia de Usuario), vincular con campo `relations`
- Tipo de relación: `System.LinkTypes.Hierarchy-Reverse`
- URL: `https://[ORGANIZATION].visualstudio.com/[PROJECT]/_workitems/edit/[HU_ID]`

---

## 🎓 DIFERENCIAS CON OTROS MODELOS

### **vs PM/BGR (Modelos B2B2C de Millas)**

| Aspecto | CORPORATIVO USD | PM/BGR |
|---------|----------------|--------|
| Cliente | Empresas (B2B) | Tarjetahabientes (B2B2C) |
| Moneda | USD | Millas (+USD en slider BGR) |
| Autenticación | Corporativa | Personal banco |
| Facturación | Empresarial | Personal |
| Centro Costos | Obligatorio | No aplica |
| Políticas | Corporativas configurables | Fijas del banco |
| Productos | Solo Vuelos | 5 productos |

### **vs AVASA/VACACIONAL (Modelos B2C)**

| Aspecto | CORPORATIVO USD | AVASA/VACACIONAL |
|---------|----------------|------------------|
| Cliente | Empresas (B2B) | Consumidor final (B2C) |
| Autenticación | Corporativa | Personal/Guest |
| Facturación | Empresarial | Personal |
| Centro Costos | Obligatorio | No aplica |
| Aprobaciones | Posible | No |

---

## 📞 CONTACTOS Y ESCALAMIENTO

**[Pendiente definir]**

- Product Owner: [Nombre]
- Tech Lead: [Nombre]
- QA Lead: [Nombre]
- Célula asignada: [Nombre]

---

## 🆘 TROUBLESHOOTING

### **Problema: No puedo crear casos**
```
Solución:
1. Verificar que estás usando agente CORPORATIVO_USD_QA_Assistant
2. Verificar que tienes planId y suiteId correctos
3. Verificar conexión con Azure DevOps
```

### **Problema: Título incorrecto**
```
Solución:
1. Verificar prefijo [CORP-USD]
2. Verificar formato: [Producto] - [Escenario] - [Proveedor] - [Config]
3. Ejemplo correcto: [CORP-USD] Vuelos - Ida y vuelta - SABRE - 1 adulto
```

### **Problema: Falta información técnica**
```
Solución:
1. Consultar CORPORATIVO_VUELOS.md para flujo detallado
2. Consultar SHARED_QA_RULES.md para fundamentos ISTQB
3. Contactar a Product Owner si faltan definiciones
```

---

## 📅 HISTORIAL DE CAMBIOS

| Fecha | Versión | Cambios |
|-------|---------|---------|
| 2026-01-22 | 1.0 | Documento inicial creado |

---

## 🔗 REFERENCIAS

- [SHARED_QA_RULES.md](../SHARED_QA_RULES.md) - Fundamentos ISTQB y Azure DevOps
- [CORPORATIVO_VUELOS.md](../../products/B2B/PPM/CORPORATIVO USD/CORPORATIVO_VUELOS.md) - Flujo detallado de vuelos
- [AGENT_CONTEXT_VALIDATION.md](../AGENT_CONTEXT_VALIDATION.md) - Validación de contexto de agentes

---

**Última actualización:** 22 de enero de 2026  
**Versión:** 1.0  
**Estado:** Inicial - Requiere completar configuración específica (proveedores, URLs, etc.)
