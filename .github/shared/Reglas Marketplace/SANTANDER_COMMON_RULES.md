# 📋 REGLAS COMUNES SANTANDER (SANT)

Documento de referencia con reglas, validaciones y estructura compartida para todos los productos de Santander.

---

## 🎯 IDENTIFICACIÓN Y ALCANCE

**Portal:** [URL por definir]  
**País:** [País por definir]  
**Prefijo obligatorio:** [SANT]  
**Aliado:** Fidelity  
**Célula:** Rocket  
**Modelo:** B2B2C  

**Productos disponibles:**
- ✅ Vuelos
- ✅ Autos
- ✅ Hoteles
- ✅ Actividades
- ✅ Tickets Disney

---

## 💰 MODELO DE NEGOCIO

### TIPO DE MODELO:

**B2B2C (Business to Business to Consumer)**
- **B2B:** Santander es el cliente corporativo de PPM/Fidelity
- **2C:** Los usuarios finales son clientes del banco Santander que acceden al marketplace de beneficios
- **Puntos/Millas:** Los clientes de Santander usan puntos del programa de fidelización del banco

### ECUACIÓN DE PAGO:

**[NOTA: Definir modelo específico de pago - Opciones comunes:]**

```
Opción A (100% Puntos):
Producto = 100% PUNTOS SANTANDER
Sin fee adicional

Opción B (Slider):
Producto = X% PUNTOS + Y% TARJETA
Mínimo: [por definir]%

Opción C (Mixto):
Producto = PUNTOS + TARJETA (proporciones fijas)
```

### EMISIÓN:

**[NOTA: Definir tipo de emisión - Opciones comunes:]**

- **Automática:** Estado EMITIDA inmediato, sin intervención manual
- **Manual/Semiautomática:** Requiere débito de puntos → pago tarjeta → emisión

**⚠️ PENDIENTE DEFINIR:**
- Modelo exacto de pago (100% puntos, slider, mixto)
- Proceso de emisión (automática vs manual)
- Fee de procesamiento (si aplica)
- Pasarela de pago (si aplica tarjeta)

---

## 📦 ESTRUCTURA DE PROVEEDORES

```
SANTANDER (SANT)
├─ 🛫 VUELOS
│  ├─ [Proveedor por definir]
│  └─ Opciones comunes: AGGREGATOR NETACTICA, AGGREGATOR SABRE, SABRE EDIFACT
│
├─ 🚗 AUTOS
│  ├─ Proveedor: [Por definir - Típicamente Sabre]
│  └─ Empresas: [Por definir - Típicamente Hertz, Dollar, Thrifty]
│
├─ 🏨 HOTELES
│  └─ [Proveedor por definir - Opciones: HotelBeds, Expedia, otro]
│
├─ 🎢 ACTIVIDADES
│  └─ [Proveedor por definir - Opciones: HotelBeds, Viator, otro]
│
└─ 🎡 DISNEY
   └─ [Proveedor por definir - Opciones: DerbySoft, OffLine, otro]
```

**⚠️ PENDIENTE DEFINIR:**
- Proveedor de vuelos y configuración de dispersión
- Proveedor de autos y empresas disponibles
- Proveedor de hoteles
- Proveedor de actividades
- Proveedor de tickets Disney

---

## 🎨 FORMATO DE TÍTULO ESPECÍFICO SANTANDER

```
[SANT] [Producto] - [Escenario] - [Variante] - [Proveedor si aplica]
```

**Ejemplos:**
- ✅ `[SANT] Vuelos - Ida y vuelta - [Proveedor] - 1 adulto`
- ✅ `[SANT] Hoteles - 2 noches - [Proveedor] - Cancelación gratuita`
- ✅ `[SANT] Autos - Dropoff diferente - [Empresa] - 5 días`
- ✅ `[SANT] Actividades - Tour ciudad - [Proveedor] - 2 adultos`
- ✅ `[SANT] Disney - 3 días - [Proveedor] - Park Hopper`

**URL de login:**
```
[URL por definir]
```

---

## ✅ VALIDACIONES COMUNES A TODOS LOS PRODUCTOS

### VALIDACIONES FUNCIONALES:

✅ **Integridad de datos:** Consistencia entre todas las pantallas del flujo  
✅ **Campos obligatorios:** Validación completa antes de habilitar botón Canjear/Reservar  
✅ **Links funcionales:** Términos y condiciones, tratamiento de datos abren correctamente  
✅ **Estados de reserva:** Confirmada en admin con todos los datos completos  
✅ **Proveedor:** Confirmación correcta del proveedor correspondiente  
✅ **Cálculo correcto:** Puntos/Millas canjeados calculados correctamente según producto  

### VALIDACIONES ESPECÍFICAS B2B2C:

✅ **Autenticación:** Login con credenciales de cliente Santander  
✅ **Saldo de puntos:** Verificación de puntos disponibles antes de reservar  
✅ **Restricciones corporativas:** Cumplimiento de políticas de Santander (si aplican)  
✅ **Branding:** Validación de marca Santander en todas las pantallas  
✅ **Términos y condiciones:** Específicos de Santander + PPM  

### VALIDACIONES DE EMISIÓN:

**[NOTA: Ajustar según modelo definido]**

✅ **Emisión automática (si aplica):** Reserva en estado EMITIDA sin intervención manual  
✅ **Emisión manual (si aplica):** 
- Débito de puntos exitoso
- Pago con tarjeta procesado (si aplica)
- Cambio de estado manual correcto
- Notificaciones enviadas

---

## 🔍 VALIDACIONES ESPECÍFICAS POR PRODUCTO

### VUELOS:

✅ Búsqueda con origen, destino, fechas válidas  
✅ Filtros funcionan correctamente  
✅ Disponibilidad en tiempo real  
✅ Upsells mostrados correctamente (si aplican)  
✅ Selección de asientos/equipaje (si aplica)  
✅ Datos de pasajeros completos y válidos  
✅ PNR generado correctamente  
✅ Reserva visible en admin con todos los detalles  

### AUTOS:

✅ Búsqueda con ubicación recogida/devolución, fechas válidas  
✅ Filtros de empresa, tipo de vehículo funcionan  
✅ Disponibilidad en tiempo real  
✅ Extras mostrados correctamente (GPS, silla bebé, etc.)  
✅ Datos de conductor completos y válidos  
✅ Edad mínima validada (21-25 años según empresa)  
✅ Reserva visible en admin con todos los detalles  

### HOTELES:

✅ Búsqueda con destino, fechas (check-in/check-out), huéspedes  
✅ Filtros de ubicación, estrellas, servicios funcionan  
✅ Disponibilidad de habitaciones en tiempo real  
✅ Políticas de cancelación mostradas claramente  
✅ Datos de huéspedes completos y válidos  
✅ Reserva visible en admin con todos los detalles  

### ACTIVIDADES:

✅ Búsqueda con destino, fechas válidas  
✅ Filtros de categoría, duración funcionan  
✅ Disponibilidad en tiempo real  
✅ Descripción completa de actividad  
✅ Punto de encuentro/recogida claramente especificado  
✅ Datos de participantes completos y válidos  
✅ Reserva visible en admin con todos los detalles  

### TICKETS DISNEY:

✅ Selección de parque(s) correcto  
✅ Selección de días correcta (1-10 días)  
✅ Fecha de inicio válida  
✅ Opciones de tickets disponibles (Park Hopper, etc.)  
✅ Datos de visitantes completos y válidos  
✅ Reserva visible en admin con todos los detalles  

---

## 🛡️ SEGURIDAD Y COMPLIANCE

### DATOS PERSONALES:

✅ **RGPD/Normativas locales:** Manejo correcto de datos personales  
✅ **Cifrado:** Datos sensibles cifrados (tarjetas, documentos)  
✅ **Consentimiento:** Aceptación explícita de tratamiento de datos  
✅ **Cookies:** Política de cookies implementada correctamente  

### TRANSACCIONES:

✅ **PCI-DSS:** Cumplimiento en manejo de tarjetas (si aplica)  
✅ **Tokenización:** Datos de pago tokenizados correctamente  
✅ **SSL/TLS:** Conexión segura en todo el flujo  
✅ **Logs:** Trazabilidad completa de transacciones  

---

## 📊 MÉTRICAS Y REPORTES

### KPIs PRINCIPALES:

- **Tasa de conversión:** % de búsquedas que terminan en reserva
- **Tiempo de respuesta:** Búsqueda, disponibilidad, confirmación
- **Tasa de error:** % de transacciones fallidas
- **Emisión exitosa:** % de reservas emitidas correctamente
- **Uso de puntos:** Promedio de puntos canjeados por producto

### REPORTES REQUERIDOS:

- Reservas por producto (diario/semanal/mensual)
- Puntos canjeados por categoría
- Errores por tipo y frecuencia
- Tiempos de procesamiento por proveedor
- Tasa de cancelaciones por producto

---

## 🔧 CONFIGURACIÓN TÉCNICA

### ENTORNOS:

**⚠️ PENDIENTE DEFINIR:**
- URL de desarrollo
- URL de testing/QA
- URL de preprod
- URL de producción

### CREDENCIALES DE PRUEBA:

**⚠️ PENDIENTE DEFINIR:**
- Usuario QA con saldo de puntos
- Usuario sin puntos
- Usuario VIP (si aplica)
- Credenciales de admin

### AZURE DEVOPS:

**⚠️ PENDIENTE DEFINIR:**
- Organization: [Por definir]
- Project: [Por definir]
- Plan ID: [Por definir]
- Suite ID base: [Por definir]

---

## 📚 REFERENCIAS

### DOCUMENTACIÓN RELACIONADA:

📋 [SHARED_QA_RULES.md](../SHARED_QA_RULES.md) - Fundamentos ISTQB y Azure DevOps  
📋 [AGENT_CONTEXT_VALIDATION.md](../AGENT_CONTEXT_VALIDATION.md) - Validación de contexto de agentes  

### FLUJOS DETALLADOS POR PRODUCTO:

🛫 [SANT_VUELOS.md](../../products/B2B2C/Fidelity/Santander/SANT_VUELOS.md) - Flujo E2E completo de Vuelos  
🚗 [SANT_AUTOS.md](../../products/B2B2C/Fidelity/Santander/SANT_AUTOS.md) - Flujo E2E completo de Autos  
🏨 [SANT_HOTELES.md](../../products/B2B2C/Fidelity/Santander/SANT_HOTELES.md) - Flujo E2E completo de Hoteles  
🎢 [SANT_ACTIVIDADES.md](../../products/B2B2C/Fidelity/Santander/SANT_ACTIVIDADES.md) - Flujo E2E completo de Actividades  
🎡 [SANT_DISNEY.md](../../products/B2B2C/Fidelity/Santander/SANT_DISNEY.md) - Flujo E2E completo de Tickets Disney  

---

## 📝 NOTAS IMPORTANTES

⚠️ **DOCUMENTO EN CONSTRUCCIÓN**

Este documento define la estructura base del modelo Santander.  
Las secciones marcadas con **[PENDIENTE DEFINIR]** requieren información del equipo de producto/negocio.

**Próximos pasos:**
1. ✅ Definir modelo de pago (100% puntos, slider, mixto)
2. ✅ Definir proceso de emisión (automática vs manual)
3. ✅ Confirmar proveedores para cada producto
4. ✅ Obtener URLs de ambientes
5. ✅ Configurar credenciales de prueba
6. ✅ Configurar Azure DevOps (planId, suiteId)
7. ✅ Crear flujos detallados por producto (SANT_VUELOS.md, etc.)

---

**Versión:** 1.0.0  
**Fecha de creación:** 2026-01-23  
**Última actualización:** 2026-01-23  
**Célula:** Rocket  
**Aliado:** Fidelity  
**Líder TM:** Cristian Garzon Sanchez  
