# 📋 REGLAS COMUNES SANTANDER (SANT)

Documento de referencia con reglas, validaciones y estructura compartida para todos los productos de Santander.

---

## 🎯 IDENTIFICACIÓN Y ALCANCE

**Portal:** https://sder-demo.smartlinks.dev/ (Demo) / https://sder-test.smartlinks.dev/ (Test)  
**País:** México  
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

**MODELO SLIDER (Similar a BGR Miles / Club Miles Ecuador):**

```
Producto = X% PUNTOS SANTANDER + Y% PLATA (Pesos MXN)

Donde:
- X = % de Puntos (mínimo configurable desde administrador)
- Y = % de Plata con tarjeta (máximo = 100% - mínimo)
- X + Y = 100%
```

**CONFIGURACIÓN DEL MÍNIMO:**
- El **porcentaje mínimo de puntos** es configurable desde el administrador
- Similar a BGR (mínimo 2875 puntos o 20%) y CME (mínimo 20%)
- El usuario puede mover el slider entre el mínimo configurado y 100% puntos

**EJEMPLOS:**
```
Si mínimo configurado = 20%:
✅ 100% Puntos + 0% Plata
✅ 50% Puntos + 50% Plata
✅ 20% Puntos + 80% Plata
❌ 10% Puntos + 90% Plata (No permitido - bajo mínimo)
```

**FEE DE PROCESAMIENTO:**
- ✅ **Vuelos:** SÍ tiene fee adicional (como Pichincha Miles)
- ❌ **Otros productos:** Sin fee adicional (Autos, Hoteles, Actividades, Disney)

### EMISIÓN:

**EMISIÓN AUTOMÁTICA:**

✅ La reserva pasa a estado **EMITIDA** inmediatamente después de confirmar la compra
✅ No requiere intervención manual del equipo de operaciones
✅ Similar al modelo de Pichincha Miles (PM)

**FLUJO DE EMISIÓN:**
```
1. Usuario completa datos y selecciona slider (% puntos + % plata)
2. Sistema valida saldo de puntos disponible
3. Débito de puntos + cargo a tarjeta procesados simultáneamente
4. Estado cambia automáticamente a EMITIDA
5. Notificaciones enviadas (email/SMS)
6. Tickets/vouchers generados automáticamente
```

**DIFERENCIA CON EMISIÓN MANUAL:**
- ❌ NO requiere débito manual de puntos
- ❌ NO requiere cambio de estado manual
- ✅ Todo el proceso es automático y transaccional

**⚠️ PENDIENTE DEFINIR:**
- Pasarela de pago específica (PlacetoPay, Lightbox, otra)
- Tiempo máximo de emisión automática
- Manejo de errores en emisión automática

---

## 📦 ESTRUCTURA DE PROVEEDORES

```
SANTANDER (SANT) - México
├─ 🛫 VUELOS
│  └─ SABRE EDIFACT
│     • Dispersión: Similar a PM/BGR (múltiples aerolíneas)
│     • Tipo de boleto: Edifact (emisión automática)
│     • Fee: SÍ (cargo adicional por servicio)
│
├─ 🚗 AUTOS
│  └─ Sabre
│     • Empresas disponibles:
│       - Hertz
│       - Dollar
│       - Thrifty
│     • Validación edad mínima conductor
│     • Extras: GPS, silla bebé, conductor adicional
│
├─ 🏨 HOTELES
│  └─ Sabre
│     • Subproveedor: Expedia
│     • Dispersión de hoteles global
│     • Políticas de cancelación variables
│     • Sistema de estrellas estándar
│
├─ 🎢 ACTIVIDADES
│  └─ HotelBeds
│     • Tours y experiencias
│     • Tickets de atracciones
│     • Traslados y transporte
│     • Disponibilidad en tiempo real
│
└─ 🎡 DISNEY
   └─ DerbySoft
      • Tickets parques Disney
      • Opciones: Park Hopper, días múltiples
      • Emisión electrónica de tickets
      • Validez desde primera entrada
```

**✅ PROVEEDORES CONFIRMADOS - TODOS DEFINIDOS**

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

**Demo:**
```
https://sder-demo.smartlinks.dev/es-mx/auth?provider=bgr&foreignId=[TOKEN]
```

**Test:**
```
https://sder-test.smartlinks.dev/es-mx/auth?provider=bgr&foreignId=[TOKEN]
```

**Generador de tokens:**
```
https://sut.fidelitymkt.net/tknUltra.php
```

**Nota:** El `[TOKEN]` debe obtenerse del generador de tokens de Fidelity antes de acceder. El token se concatena directamente después de `foreignId=`

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

✅ **Autenticación:** Login con credenciales de cliente Santander (token-based)  
✅ **Saldo de puntos:** Verificación de puntos disponibles antes de reservar  
✅ **Restricciones corporativas:** Cumplimiento de políticas de Santander (si aplican)  
✅ **Branding:** Validación de marca Santander en todas las pantallas  
✅ **Términos y condiciones:** Específicos de Santander + PPM  

### VALIDACIONES ESPECÍFICAS DEL SLIDER:

✅ **Mínimo de puntos:** El slider respeta el % mínimo configurado desde administrador  
✅ **Cálculo correcto:** Puntos + Plata suman exactamente el 100% del precio  
✅ **Saldo suficiente:** Usuario tiene puntos disponibles para el % seleccionado  
✅ **Movimiento del slider:** Funciona correctamente en toda la pantalla de pago  
✅ **Visualización de montos:** Muestra claramente cuántos puntos y cuánta plata (MXN)  
✅ **Redondeo:** Puntos y pesos redondeados correctamente (sin decimales en puntos)  
✅ **Tarjeta válida:** Validación de tarjeta si el % de plata es > 0%  

### VALIDACIONES DE EMISIÓN AUTOMÁTICA:

✅ **Estado EMITIDA:** Reserva aparece como EMITIDA inmediatamente después de confirmar  
✅ **Débito de puntos:** Puntos debitados automáticamente del saldo del usuario  
✅ **Cargo a tarjeta:** Monto en plata (MXN) cargado correctamente a la tarjeta  
✅ **Transaccionalidad:** Débito puntos + cargo tarjeta son atómicos (todo o nada)  
✅ **Notificaciones:** Email/SMS enviados automáticamente con confirmación  
✅ **Tickets/Vouchers:** Generados automáticamente y disponibles para descarga  
✅ **Admin visible:** Reserva visible en administrador con estado EMITIDA  
✅ **Proveedor confirmado:** Confirmación exitosa con el proveedor correspondiente  
✅ **Rollback:** Si falla algún paso, se reversa todo (puntos + tarjeta)

---

## 🔍 VALIDACIONES ESPECÍFICAS POR PRODUCTO

### VUELOS:

✅ Búsqueda con origen, destino, fechas válidas  
✅ Filtros funcionan correctamente  
✅ Disponibilidad en tiempo real (Sabre Edifact)  
✅ **Fee de procesamiento:** Validar que se aplica y calcula correctamente  
✅ **Fee en slider:** Verificar que el fee NO es afectado por el slider (se suma al total)  
✅ Upsells mostrados correctamente (si aplican)  
✅ Selección de asientos/equipaje (si aplica)  
✅ Datos de pasajeros completos y válidos  
✅ PNR generado correctamente  
✅ Reserva visible en admin con todos los detalles  
✅ **Proveedor confirmado:** SABRE EDIFACT en detalles de reserva  

### AUTOS:

✅ Búsqueda con ubicación recogida/devolución, fechas válidas  
✅ Filtros de empresa, tipo de vehículo funcionan  
✅ Disponibilidad en tiempo real (Sabre)  
✅ **Empresas disponibles:** Hertz, Dollar, Thrifty solamente  
✅ Extras mostrados correctamente (GPS, silla bebé, etc.)  
✅ Datos de conductor completos y válidos  
✅ Edad mínima validada (21-25 años según empresa)  
✅ Reserva visible en admin con todos los detalles  
✅ **Proveedor confirmado:** Sabre en detalles de reserva  

### HOTELES:

✅ Búsqueda con destino, fechas (check-in/check-out), huéspedes  
✅ Filtros de ubicación, estrellas, servicios funcionan  
✅ Disponibilidad de habitaciones en tiempo real (Sabre/Expedia)  
✅ Políticas de cancelación mostradas claramente  
✅ Datos de huéspedes completos y válidos  
✅ Reserva visible en admin con todos los detalles  
✅ **Proveedor confirmado:** Sabre (Expedia) en detalles de reserva  

### ACTIVIDADES:

✅ Búsqueda con destino, fechas válidas  
✅ Filtros de categoría, duración funcionan  
✅ Disponibilidad en tiempo real (HotelBeds)  
✅ Descripción completa de actividad  
✅ Punto de encuentro/recogida claramente especificado  
✅ Datos de participantes completos y válidos  
✅ Reserva visible en admin con todos los detalles  
✅ **Proveedor confirmado:** HotelBeds en detalles de reserva  

### TICKETS DISNEY:

✅ Selección de parque(s) correcto  
✅ Selección de días correcta (1-10 días)  
✅ Fecha de inicio válida  
✅ Opciones de tickets disponibles (Park Hopper, etc.)  
✅ Datos de visitantes completos y válidos  
✅ Reserva visible en admin con todos los detalles  
✅ **Proveedor confirmado:** DerbySoft en detalles de reserva  
✅ **Emisión electrónica:** Tickets generados automáticamente  

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

**Demo:**
- URL: `https://sder-demo.smartlinks.dev/es-mx/auth?provider=bgr&foreignId=[TOKEN]`
- Token: Obtener desde https://sut.fidelitymkt.net/tknUltra.php

**Test:**
- URL: `https://sder-test.smartlinks.dev/es-mx/auth?provider=bgr&foreignId=[TOKEN]`
- Token: Obtener desde https://sut.fidelitymkt.net/tknUltra.php

**⚠️ PENDIENTE DEFINIR:**
- URL de preprod (si aplica)
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
1. ✅ Definir modelo de pago (Slider con mínimo configurable - COMPLETO)
2. ✅ Definir proceso de emisión (Automática - COMPLETO)
3. ✅ Confirmar proveedores (Sabre Edifact, HotelBeds, DerbySoft - COMPLETO)
4. ✅ Confirmar fee de procesamiento (SÍ en vuelos - COMPLETO)
5. ✅ Obtener URLs de ambientes (Demo y Test - COMPLETO)
6. ⏳ Confirmar pasarela de pago para tarjeta (PlacetoPay, Stripe, otra)
7. ⏳ Obtener % mínimo configurado actualmente en administrador
8. ⏳ Configurar credenciales de prueba (usuarios con/sin puntos)
9. ⏳ Configurar Azure DevOps (planId, suiteId)
10. ⏳ Crear flujos detallados por producto (SANT_VUELOS.md, etc.)

---

**Versión:** 1.2.0  
**Fecha de creación:** 2026-01-23  
**Última actualización:** 2026-02-05  
**Célula:** Rocket  
**Aliado:** Fidelity  
**Líder TM:** Cristian Garzon Sanchez  
**País:** México  
**Modelo:** Slider (Puntos + Plata) con emisión automática  
**Proveedores:** Sabre Edifact, HotelBeds, DerbySoft  
