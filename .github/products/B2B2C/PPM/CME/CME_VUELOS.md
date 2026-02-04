# � FLUJO E2E OBLIGATORIO PARA VUELOS - CME

**Proveedor:** Club Miles Ecuador  
**Portal Test:** https://clubmiles-ec.developppm.com/  
**Portal Demo:** https://clubmiles-ec.preprodppm.com/  
**Tecnología:** Angular (TypeScript/JavaScript)  
**Métodos de pago:** Solo Millas (100%) o Millas+Plata (Copago con Slider en CheckOut, mínimo 20%)  
**Fee de procesamiento:** TARJETA DE CRÉDITO (obligatorio, formulario en CheckOut)  
**Pasarela:** PlacetoPay (bash en background, sin interfaz visual)

---

## 📦 PROVEEDORES DISPONIBLES

- **Sabre Edifact**
- **Aggregator - Sabre NDC**
- **Aggregator - Netactica**

---

## � PANTALLAS EXCLUSIVAS DE VUELOS

1. **Resumen** - Después de Disponibilidad, antes de CheckOut
2. **Modal Seguro de Cancelación** - **DESPUÉS** de la pantalla Resumen (si está activo)
3. **Modal Previo a Confirmación**
4. **Confirmación Vuelos+Seguro** - Si se aceptó el seguro de cancelación

---

## ✈️ SEGURO DE CANCELACIÓN

**Disponibilidad:** Solo para vuelos  
**Proveedor del Seguro:** ZURICH  
**Servicio API:** cancellation-insurance (Api Core)  
**Momento:** Modal después del Resumen, componente checkbox en CheckOut

**Flujo completo:**

1. **Modal de Seguro (después del Resumen):**
   - Se muestra Modal con información del seguro
   - Socio visualiza beneficios y costo

2. **Componente Checkbox en CheckOut:**
   - **Opción 1:** "Pago con Millas: Seguro de cancelación aprobado" ✅
   - **Opción 2:** "No quiero asegurar mi viaje" ❌
   - Solo una opción puede estar seleccionada

3. **Pantalla Previa a Confirmación:**
   - Valida qué checkbox está marcado
   - **Si "Seguro aprobado"** → Redirige a **Confirmación Vuelos+Seguro**
   - **Si "No quiero asegurar"** → Redirige a **Confirmación convencional**
   - **Si servicio "cancellation-insurance" falla** → Redirige a **Confirmación convencional**

4. **Confirmación según selección:**
   - **Con seguro:** Pantalla especial mostrando vuelo + seguro
   - **Sin seguro:** Pantalla estándar solo con vuelo

### 📋 RESERVAS EN ADMIN (VUELO+SEGURO):

**Cuando se acepta el seguro de cancelación, se crean DOS reservas separadas:**

1. **Reserva del Vuelo:**
   - Letra indicativa: **"F"** (Flights)
   - Contiene toda la información del vuelo
   - Se puede cancelar desde Admin

2. **Reserva del Seguro:**
   - Letra indicativa: **"I"** (Insurance)
   - Proveedor: **ZURICH**
   - Contiene información del seguro de cancelación
   - ❌ **NO se puede cancelar desde Admin** (limitación actual)

**IMPORTANTE:** 
- Voucher NO disponible para reservas de Vuelos+Seguro de Cancelación
- Si el servicio "cancellation-insurance" (Api Core) falla, el flujo continúa sin seguro
- Solo la reserva del vuelo (F) puede ser cancelada; la reserva del seguro (I) no tiene opción de cancelación

---

## 🎫 VOUCHER EN ADMIN

**Disponibilidad:** ✅ SÍ

**Características:**
- Visualizable y descargable en el detalle de la reserva en Admin
- Formato: PDF
- Idioma: Español

**Limitación:**
- ❌ NO disponible para reservas de Vuelos+Seguro de Cancelación
- ✅ Disponible solo para vuelos sin seguro

---

## 🎚️ MÉTODOS DE PAGO Y FEE

### SLIDER Y COPAGO:

> 📖 **Lógica completa del Slider:** Ver [CME_COMMON_RULES.md](../../../../shared/Reglas%20Marketplace/CME_COMMON_RULES.md) - Sección "MÉTODOS DE PAGO"

**Resumen para vuelos:**
- Slider ajustable en CheckOut (mínimo 20%, máximo 100% o Millas disponibles)
- Solo Millas (100%) o Millas+Plata (Copago)
- Escenarios de redención 1-4 aplican igual que en otros productos

### ✈️ FEE DE PROCESAMIENTO (EXCLUSIVO DE VUELOS):

**Características:**
- **Obligatorio** para todos los vuelos (diferenciador clave vs. otros productos)
- **NO se puede pagar con Millas** (solo con Tarjeta de Crédito)
- **Formulario TC integrado en CheckOut** (NO lightbox, dentro de la misma pantalla)
- **Pasarela:** PlacetoPay bash (procesamiento en background, sin interfaz visual)
- Se procesa al reservar mediante conexión bash en segundo plano

**Cobro del Fee:**
- Se cobra SIEMPRE, independiente del método elegido (Solo Millas o Copago)
- Si elige "Solo Millas 100%": Producto se paga con Millas, Fee se cobra en USD con TC
- Si elige "Millas+Plata": Producto con Copago + Fee adicional en USD con TC

---

## 📋 PASOS OBLIGATORIOS DEL FLUJO E2E

**Siempre incluir estos pasos desde login:**

1. Ingresar a la URL https://clubmiles-ec.preprodppm.com/ | Portal cargado correctamente, pantalla principal visible
2. Realizar login con usuario y contraseña válidos | Login exitoso, acceso al home autenticado
3. Click en la opción Vuelos | Se despliega el formulario de búsqueda de vuelos
4. Seleccionar tipo de viaje (Ida y vuelta, Solo ida, Multidestino) | Tipo de viaje seleccionado correctamente
5. Ingresar criterios de búsqueda (origen, destino, fechas salida, fecha regreso, número de pasajeros, clase) | Criterios ingresados correctamente
6. Click en botón Buscar | Se muestran todos los vuelos disponibles
7. Validar que se muestra lista de vuelos con millas y fee de procesamiento visible | Lista de vuelos visible con precios en millas y fee en moneda
8. Click en botón Canjear de un vuelo disponible | Se despliega automáticamente el popup upsell
9. Seleccionar tarifa en el upsell (Básica, Estándar, Premium) y click en Continuar | Tarifa seleccionada, se muestra pantalla de resumen
10. Validar datos de resumen (vuelo, fechas, pasajeros, millas totales, fee de procesamiento) | Datos correctos y consistentes con la selección
11. Click en botón Continuar | Sistema redirige al checkout
12. Diligenciar todos los campos obligatorios (datos de pasajeros: nombre, apellido, documento, fecha nacimiento; datos de contacto: email, teléfono) | Campos completados correctamente
13. Ingresar datos de tarjeta de crédito en el formulario de CheckOut (número, fecha vencimiento, CVV, titular) | Datos de tarjeta ingresados y validados
14. Validar que el fee de procesamiento es visible en el resumen del checkout | Fee mostrado correctamente
15. Validar que el logo P2P está visible (exclusivo de vuelos) | Logo P2P visible en checkout
16. Validar componente de seguro de cancelación con opciones (si aplica): "Pago con Millas: Seguro aprobado" o "No quiero asegurar mi viaje" | Componente visible con opciones seleccionables
17. Seleccionar opción de seguro según el escenario de prueba | Opción seleccionada correctamente
18. Marcar check de Tratamiento de datos | Check seleccionado
19. Marcar check de Términos y condiciones | Check seleccionado
20. Validar que el botón Canjear se habilita al completar todos los campos obligatorios | Botón Canjear habilitado
21. Click en botón Canjear | Se muestra pantalla previa a confirmación, procesamiento batch PlacetoPay en background
22. Validar pantalla previa que resume la reserva (vuelo, pasajeros, millas, fee) | Resumen correcto antes de confirmación final
23. Click en Confirmar | Se procesa pago con PlacetoPay batch y se muestra pantalla de confirmación (convencional o con seguro según selección)
24. Validar pantalla de confirmación con código de reserva, resumen de pagos (millas canjeadas + fee pagado) | Código de reserva generado, pagos mostrados correctamente
25. Ingresar al módulo de administración CME | Admin cargado correctamente
26. Buscar reserva por código | Reserva localizada y visible
27. Validar que los pagos en admin coinciden con la confirmación (millas + fee) | Pagos correctos en admin
28. Validar que la reserva queda en estado EMITIDA automáticamente | Reserva en estado EMITIDA

### 🚫 PASOS ADICIONALES PARA CANCELACIÓN DE RESERVA:

**Para proveedores AGGREGATOR (Netactica, Sabre NDC):**

29. En el detalle de la reserva en Admin, validar que se muestra el botón "CANCELAR RESERVA" | Botón visible y habilitado
30. Click en botón "CANCELAR RESERVA" | Sistema procesa la cancelación
31. Validar que la reserva cambia a estado CANCELADA | Estado actualizado correctamente

**Para proveedor SABRE EDIFACT:**

29. En el detalle de la reserva en Admin, identificar todos los tiquetes de los pasajeros | Lista de tiquetes visible
30. Cancelar el tiquete de cada pasajero individualmente | Cada tiquete marcado como cancelado
31. Una vez cancelados todos los tiquetes, click en botón "CANCELAR RESERVA" | Sistema procesa la cancelación de la reserva completa
32. Validar que la reserva cambia a estado CANCELADA | Estado actualizado correctamente

**Para reservas con Seguro de Cancelación (Vuelo+Seguro):**

29. Validar que en Admin se muestran DOS reservas separadas: Vuelo (F) y Seguro (I) | Ambas reservas visibles con letras indicativas
30. Identificar la reserva del Vuelo (letra "F") | Reserva de vuelo identificada
31. Seguir el proceso de cancelación según el proveedor (Aggregator o Sabre Edifact) SOLO para la reserva del Vuelo | Reserva de vuelo cancelada
32. Validar que la reserva del Seguro (letra "I", proveedor ZURICH) NO tiene opción de cancelación disponible | Opción de cancelación no disponible para seguro
33. Validar que solo la reserva del Vuelo (F) queda en estado CANCELADA | Reserva de vuelo cancelada, reserva de seguro permanece activa

---

## 🔄 VARIACIONES SEGÚN ESCENARIO

**Tipo de viaje:**
- Ida y vuelta
- Solo ida
- Multidestino (máximo 6 trayectos Ida y Vuelta)

**Proveedores:**
- AGGREGATOR - NETACTICA
- AGGREGATOR - SABRE NDC
- SABRE EDIFACT

**Pasajeros:**
- 1 pasajero
- Múltiples pasajeros (2-9)

**Clase:**
- Económica
- Premium Economy
- Business
- Primera clase

**Tarifas (Upsell):**
- Básica (solo vuelo)
- Estándar (vuelo + equipaje adicional)
- Premium (vuelo + equipaje + asiento + cambios)

---

## ✅ VALIDACIONES CRÍTICAS

✅ **Integridad de datos:** Consistencia entre búsqueda → disponibilidad → upsell → resumen → checkout → previa confirmación → confirmación → admin  
✅ **Fee de procesamiento:** Siempre visible y procesado con tarjeta de crédito en formulario CheckOut  
✅ **PlacetoPay batch:** Procesamiento en background sin interfaz visual durante el canje  
✅ **Logo P2P:** Visible en checkout (exclusivo de vuelos)  
✅ **Componente seguro:** Checkbox con opciones "Seguro aprobado" o "No asegurar" funcionando correctamente  
✅ **Pantalla previa:** Validar que redirige a confirmación correcta según selección de seguro  
✅ **Servicio cancellation-insurance:** Si falla, flujo continúa a confirmación convencional  
✅ **Cálculo de millas:** Millas totales correctas según tarifa y cantidad de pasajeros  
✅ **Campos obligatorios:** Datos de todos los pasajeros, tarjeta de crédito, contacto, aceptación de términos  
✅ **Links funcionales:** Términos y condiciones, tratamiento de datos abren correctamente  
✅ **Estados de reserva:** Confirmada en admin con todos los datos completos  
✅ **Emisión automática:** Reserva en estado EMITIDA sin intervención manual  
✅ **Proveedor:** Validar proveedor correcto (NETACTICA, SABRE NDC, SABRE EDIFACT)  
✅ **Cancelación Aggregator:** Botón "CANCELAR RESERVA" funcional directamente  
✅ **Cancelación Sabre Edifact:** Cancelación de tiquetes individuales antes de cancelar reserva  
✅ **Dos reservas (Vuelo+Seguro):** Validar letras indicativas F (vuelo) e I (seguro)  
✅ **Proveedor ZURICH:** Información del seguro correcta en reserva con letra "I"  
✅ **Cancelación seguro:** Validar que reserva de seguro (I) NO tiene opción de cancelación  

---

## 📝 FORMATO DE TÍTULO

```
[CME] Vuelos - [Tipo viaje] - [Proveedor] - [Característica especial]
```

**Ejemplos:**
- `[CME] Vuelos - Ida y vuelta - SABRE EDIFACT - Con seguro cancelación - 2 pasajeros`
- `[CME] Vuelos - Solo ida - NETACTICA - Tarifa Premium - 1 pasajero`
- `[CME] Vuelos - Multidestino - AGGREGATOR SABRE NDC - 6 trayectos - 4 pasajeros`

---

## 📸 IMÁGENES DE REFERENCIA

Incluir SIEMPRE estas imágenes en el campo Descriptions del Test Case:

- Home-vuelos-CME.png - Pantalla principal con opción Vuelos
- Disponibilidad-vuelos-CME.png - Lista de vuelos disponibles con millas y fee
- upsell-vuelos-CME.png - Popup de selección de tarifas
- Resumen-vuelos-CME.png - Pantalla de resumen antes del checkout
- ModalSeguro-vuelos-CME.png - Modal de seguro de cancelación (si aplica)
- Checkout-vuelos-CME.png - Formulario de checkout completo con logo P2P y componente seguro
- PreviaConfirmacion-vuelos-CME.png - Pantalla previa a confirmación final
- Confirmacion-vuelos-CME.png - Pantalla de confirmación con código de reserva
- ConfirmacionSeguro-vuelos-CME.png - Confirmación con seguro (si aplica)
- Admin.png - Validación en módulo admin CME

---

## 📌 NOTAS IMPORTANTES

**Fee de procesamiento:**
- SIEMPRE requerido en vuelos (diferencia con hoteles, autos, actividades, disney)
- Pago con tarjeta de crédito en formulario integrado en CheckOut
- Procesamiento PlacetoPay batch en background (sin interfaz visual)
- No se puede canjear con millas

**Logo P2P:**
- Exclusivo de vuelos
- Debe ser visible en checkout
- NO aparece en otros productos

**Seguro de cancelación:**
- Solo disponible para vuelos
- Proveedor del seguro: ZURICH
- Servicio API: "cancellation-insurance" (Api Core)
- Si el servicio falla, flujo continúa sin seguro
- Voucher NO disponible si se acepta seguro
- Se crean dos reservas separadas: Vuelo (F) y Seguro (I)
- Solo la reserva del vuelo puede cancelarse; seguro no tiene opción de cancelación

**Cancelación de reservas:**
- **Aggregator (Netactica, Sabre NDC):** Cancelación directa con botón "CANCELAR RESERVA"
- **Sabre Edifact:** Primero cancelar tiquetes de cada pasajero, luego "CANCELAR RESERVA"
- **Vuelo+Seguro:** Solo se puede cancelar la reserva del vuelo (F), no la del seguro (I/ZURICH)

**Emisión:****
- Siempre automática
- Estado EMITIDA inmediato tras confirmación
- Sin proceso manual

---

## 🔗 REFERENCIAS

**Documentación relacionada:**
- [CME_COMMON_RULES.md](../../../shared/Reglas%20Marketplace/CME_COMMON_RULES.md) - Reglas comunes CME
- [SHARED_QA_RULES.md](../../../shared/SHARED_QA_RULES.md) - Fundamentos ISTQB
- [Kepler_Models_Comparison.md](../../../docs/comparisons/Kepler_Models_Comparison.md) - Comparación entre modelos

---

**Última actualización:** 2026-01-23  
**Versión:** 2.0.0  
**Mantenido por:** QA Team Ultragroup  
**Cambios:** Eliminadas referencias a lightbox (ahora PlacetoPay batch), eliminada dispersión de fondos (no aplica en CME), corregido multidestino (6 trayectos), actualizado flujo completo del seguro de cancelación con componente checkbox y servicio cancellation-insurance
