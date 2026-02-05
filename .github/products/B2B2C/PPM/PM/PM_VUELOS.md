# 🛫 FLUJO E2E OBLIGATORIO PARA VUELOS - PICHINCHA MILES

**Proveedor:** Pichincha Miles Ecuador  
**Portal:** https://pichinchamiles-ec.preprodppm.com/  
**Tecnología:** Angular (TypeScript/JavaScript)  
**Modelo de pago:** 100% Millas + Fee de procesamiento (Tarjeta de crédito)  
**Promocode:** ✅ SÍ APLICA (campo opcional en búsqueda)  
**Markup:** ❌ NO APLICA (solo Hoteles y Actividades tienen Markup)  

---

## 🎟️ LÓGICA DE PROMOCODE EN VUELOS

### TIPOS DE DESCUENTO:

**1️⃣ Descuento Porcentual (%):**
- Descuento expresado como porcentaje (ej: 5%, 10%, 15%)
- Se calcula sobre el valor base (Boleto + Fee oculto)
- Fórmula: Base × (% / 100)

**2️⃣ Descuento Fijo:**
- Descuento en cantidad específica de millas (ej: 3,000 millas, 5,000 millas)
- Se resta directamente del valor base
- Fórmula: Base - Millas fijas

### APLICACIÓN DEL DESCUENTO:

**El descuento del Promocode aplica sobre:**
- ✅ **Valor del boleto** (en millas)
- ✅ **Fee oculto** (en millas)
- ❌ **NO aplica sobre TA** (Tasas Aeroportuarias)

### PROCESO DE CÁLCULO:

```
1️⃣ Precio total del vuelo en millas (incluye todo)
2️⃣ Restar las TA equivalentes (convertidas a puntos)
3️⃣ Sobre el valor resultante (Boleto + Fee oculto) → Aplicar descuento Promocode
4️⃣ Sumar nuevamente las TA (sin descuento)
5️⃣ Total final = (Boleto + Fee oculto con descuento) + TA sin descuento
```

### EJEMPLOS PRÁCTICOS:

**Ejemplo 1 - Descuento Porcentual (10%):**

**Datos iniciales:**
- Precio total vuelo: **50,000 millas**
- TA equivalentes: **5,000 millas**
- Promocode: **10% descuento**

**Cálculo:**
```
1. Base de cálculo = 50,000 - 5,000 = 45,000 millas (Boleto + Fee oculto)
2. Descuento 10% = 45,000 × 0.10 = 4,500 millas
3. Subtotal con descuento = 45,000 - 4,500 = 40,500 millas
4. Total final = 40,500 + 5,000 (TA sin descuento) = 45,500 millas
```

**Ahorro total:** 4,500 millas

---

**Ejemplo 2 - Descuento Fijo (3,000 millas):**

**Datos iniciales:**
- Precio total vuelo: **50,000 millas**
- TA equivalentes: **5,000 millas**
- Promocode: **3,000 millas descuento fijo**

**Cálculo:**
```
1. Base de cálculo = 50,000 - 5,000 = 45,000 millas (Boleto + Fee oculto)
2. Descuento fijo = 3,000 millas
3. Subtotal con descuento = 45,000 - 3,000 = 42,000 millas
4. Total final = 42,000 + 5,000 (TA sin descuento) = 47,000 millas
```

**Ahorro total:** 3,000 millas

### VALIDACIONES CRÍTICAS PROMOCODE:

✅ **Campo presente:** Validar que existe en búsqueda de vuelos  
✅ **Código válido:** Promocode existente y activo  
✅ **Tipo de descuento:** Identificar si es % o fijo  
✅ **Cálculo correcto:** Aplicar fórmula según tipo  
✅ **Descuento NO sobre TA:** TA deben mantenerse sin modificar  
✅ **Descuento visible:** Mostrar tipo y valor del descuento en resumen y checkout  
✅ **Total correcto:** (Boleto + Fee - descuento) + TA  
✅ **Validación límites:** Descuento no puede exceder el valor base  

---

## 📦 PROVEEDORES DISPONIBLES

- **AGGREGATOR - NETACTICA** (sin dispersión de fondos)
- **AGGREGATOR - SABRE** (sin dispersión de fondos)
- **SABRE EDIFACT** (con dispersión de fondos)

---

## 🖼️ RECURSOS VISUALES DE REFERENCIA

**Pantallas del flujo completo de Vuelos:**

- **Home:** [Ver pantalla principal](../../imagenes/PM/vuelos/Home-PM.png)
  * Productos disponibles: Vuelos, Hoteles, Autos, Actividades, Disney
  * Navegación principal y acceso a login

- **Home Vuelos:** [Ver búsqueda de vuelos](../../imagenes/PM/vuelos/Home-vuelos-PM.png)
  * Formulario de búsqueda (origen, destino, fechas, pasajeros, clase)
  * Tipo de viaje (Ida y vuelta, Solo ida, Multidestino)

- **Disponibilidad:** [Ver resultados de vuelos](../../imagenes/PM/vuelos/Disponibilidad-vuelos-PM.png)
  * Lista de vuelos disponibles con millas y fee visible
  * Botón Canjear por cada vuelo

- **Upsell:** [Ver popup upsell](../../imagenes/PM/vuelos/upsell-vuelos-PM.png)
  * Tarifas disponibles con diferentes beneficios
  * Selección de tarifa y botón Continuar

- **Resumen:** [Ver pantalla resumen](../../imagenes/PM/vuelos/Resumen-vuelos-PM.png)
  * Detalle del vuelo seleccionado
  * Pasajeros, fechas, millas y botón Continuar al checkout

- **Checkout:** [Ver pantalla de checkout](../../imagenes/PM/vuelos/Checkout-vuelos-PM.png)
  * Formulario con todos los campos obligatorios
  * Fee de procesamiento visible y logo P2P
  * Checks de términos y políticas

- **Lightbox Pago Fee:** [Ver lightbox de tarjeta](../../imagenes/PM/vuelos/lightBox-vuelos-PM.png)
  * Formulario de ingreso de tarjeta de crédito
  * Pago del fee de procesamiento

- **Confirmación:** [Ver pantalla de confirmación](../../imagenes/PM/vuelos/Confirmacion-vuelos-PM.png)
  * Código de reserva generado
  * Resumen de pagos (millas + fees)

- **Admin:** [Ver módulo admin](../../imagenes/PM/vuelos/Admin.png)
  * Búsqueda de reservas y validación de pagos

- **Reserva:** [Ver detalle de reserva](../../imagenes/PM/vuelos/reserva.png)
  * Código de reserva y datos completos del vuelo

- **Resto de Reserva:** [Ver información adicional](../../imagenes/PM/vuelos/restodelareserva.png)
  * Detalles adicionales y validaciones finales

---

## 📋 PASOS OBLIGATORIOS DEL FLUJO E2E

**Siempre incluir estos pasos desde login:**

1. Ingresar a la URL https://pichinchamiles-ec.preprodppm.com/ | Portal cargado correctamente, pantalla Home visible (Ver: Home-PM.png)
2. Realizar login con usuario y contraseña válidos | Login exitoso, acceso al home autenticado
3. Click en la opción Vuelos | Se despliega el formulario de búsqueda de vuelos (Ver: Home-vuelos-PM.png)
4. Seleccionar tipo de viaje (Ida y vuelta, Solo ida, Multidestino) | Tipo de viaje seleccionado correctamente
5. Ingresar criterios de búsqueda (origen, destino, fechas salida, fecha regreso, número de pasajeros, clase) | Criterios ingresados correctamente
6. Click en botón Buscar | Se muestran todos los vuelos disponibles (Ver: Disponibilidad-vuelos-PM.png)
7. Validar que se muestra lista de vuelos con millas y fee de procesamiento visible | Lista de vuelos visible con precios en millas y fee en moneda
8. Click en botón Canjear de un vuelo disponible | Se despliega automáticamente el popup upsell (Ver: upsell-vuelos-PM.png)
9. Seleccionar tarifa en el upsell (Básica, Estándar, Premium) y click en Continuar | Tarifa seleccionada, se muestra pantalla de resumen (Ver: Resumen-vuelos-PM.png)
10. Validar datos de resumen (vuelo, fechas, pasajeros, millas totales, fee de procesamiento) | Datos correctos y consistentes con la selección
11. Click en botón Continuar | Sistema redirige al checkout (Ver: Checkout-vuelos-PM.png)
12. Diligenciar todos los campos obligatorios (datos de pasajeros: nombre, apellido, documento, fecha nacimiento; datos de contacto: email, teléfono) | Campos completados correctamente
13. Validar que el fee de procesamiento es visible en el resumen del checkout | Fee mostrado correctamente
14. Validar que el logo P2P está visible (exclusivo de vuelos) | Logo P2P visible en checkout
15. Marcar check de Tratamiento de datos | Check seleccionado
16. Marcar check de Términos y condiciones | Check seleccionado
17. Validar que el botón Canjear se habilita al completar todos los campos obligatorios | Botón Canjear habilitado
18. Click en botón Canjear | Se despliega el lightbox de pago de fee (Ver: lightBox-vuelos-PM.png)
19. Ingresar datos de tarjeta de crédito en el lightbox (número, fecha vencimiento, CVV, titular) | Tarjeta validada y datos registrados correctamente
20. Click en botón Confirmar pago en el lightbox | Pago del fee procesado, lightbox se cierra y se muestra pantalla de confirmación (Ver: Confirmacion-vuelos-PM.png)
21. Validar pantalla de confirmación con código de reserva, resumen de pagos (millas canjeadas + fee pagado) | Código de reserva generado, pagos mostrados correctamente
22. Ingresar al módulo de administración Pichincha Miles | Admin cargado correctamente (Ver: Admin.png)
23. Buscar reserva por código | Reserva localizada y visible (Ver: reserva.png y restodelareserva.png)
24. Validar que los pagos en admin coinciden con la confirmación (millas + fee) | Pagos correctos en admin
25. Validar que la reserva queda en estado EMITIDA automáticamente (100% millas - proceso automático) | Reserva en estado EMITIDA
26. [Solo para SABRE EDIFACT] Validar dispersión de fondos (fee a PPM, valor del vuelo según el proveedor correspondiente) | Dispersión realizada correctamente en Sabre

---

## 🔄 VARIACIONES SEGÚN ESCENARIO

**Tipo de viaje:**
- Ida y vuelta
- Solo ida
- Multidestino

**Proveedores:**
- AGGREGATOR - NETACTICA (sin dispersión)
- AGGREGATOR - SABRE (sin dispersión)
- SABRE EDIFACT (validar dispersión en paso 26)

**Tarifas upsell:**
- Básica
- Estándar
- Premium (diferentes beneficios)

**Pasajeros:**
- 1 adulto
- Múltiples adultos
- Adultos + menores

---

## ✅ VALIDACIONES CRÍTICAS

✅ **Secuencia de pantallas:** Home → Home Vuelos → Disponibilidad → Upsell → Resumen → Checkout → Lightbox → Confirmación → Admin  
✅ **Fee visible:** Disponibilidad + Checkout (antes del pago)  
✅ **Lightbox:** Aparece SOLO tras click en Canjear (no antes)  
✅ **Logo P2P:** Visible SOLO en vuelos (no en otros productos)  
✅ **Pago fee:** Tarjeta de crédito en lightbox (único uso de tarjeta)  
✅ **Emisión:** Automática e inmediata (estado EMITIDA sin intervención manual)  
✅ **Dispersión SABRE EDIFACT:** Fee a PPM, valor vuelo según proveedor correspondiente  
✅ **Proveedores:** AGGREGATOR - NETACTICA, AGGREGATOR - SABRE (sin dispersión), SABRE EDIFACT (con dispersión)  
✅ **Integridad de datos:** Millas y fee consistentes en todas las pantallas (Disponibilidad → Resumen → Checkout → Confirmación → Admin)

---

## 📝 FORMATO DE TÍTULO

```
[PM] Vuelos - [Tipo de viaje] - [Proveedor] - [Variante adicional]
```

**Ejemplos:**
- `[PM] Vuelos - Ida y vuelta - SABRE EDIFACT - 1 adulto - Tarifa Estándar`
- `[PM] Vuelos - Solo ida - AGGREGATOR NETACTICA - 2 adultos - Tarifa Premium`
- `[PM] Vuelos - Multidestino - AGGREGATOR SABRE - 1 adulto + 1 menor - Tarifa Básica`
