# 🏨 FLUJO E2E OBLIGATORIO PARA HOTELES - CME

**Proveedor:** Club Miles Ecuador  
**Portal Test:** https://clubmiles-ec.developppm.com/  
**Portal Demo:** https://clubmiles-ec.preprodppm.com/  
**Tecnología:** Angular (TypeScript/JavaScript)  
**Métodos de pago:** Solo Millas (100%) o Millas+Plata (Copago con Slider en CheckOut, mínimo 20%)  
**Fee:** ❌ NO  
**Pasarela:** PlacetoPay (bash, solo si hay Copago, sin interfaz visual)

---

## 📦 PROVEEDORES DISPONIBLES

**Proveedor:** HotelBeds (único)

**Límites del proveedor HotelBeds:**
- **Máximo de habitaciones:** 2 habitaciones por reserva
- **Máximo de pasajeros:** 9 pasajeros en total (entre todas las habitaciones)
- **Tipos de pasajeros:** Adultos y Niños
- **Distribución:** Los 9 pasajeros pueden distribuirse entre las 2 habitaciones o estar en 1 habitación

---

## 🎫 VOUCHER EN ADMIN

**Disponibilidad:** ❌ NO

**Nota:** Los hoteles NO generan voucher descargable en el Admin de CME.

---

## 🎚️ MÉTODOS DE PAGO Y SLIDER

### SLIDER Y COPAGO:

> 📖 **Lógica completa del Slider:** Ver [CME_COMMON_RULES.md](../../../../shared/Kepler/CME_COMMON_RULES.md) - Sección "MÉTODOS DE PAGO"

**Resumen para hoteles:**
- Slider ajustable en CheckOut (mínimo 20%, máximo 100% o Millas disponibles)
- Solo Millas (100%) o Millas+Plata (Copago)
- Escenarios de redención 1-4 aplican igual que en otros productos CME
- PlacetoPay bash procesamiento en background (solo si hay Copago)

**Diferenciador clave:**
- ❌ **SIN fee de procesamiento** (a diferencia de vuelos)
- ❌ **SIN voucher** en Admin

### PROCESO DE EMISIÓN Y PAGO:

**Escenario 1: Solo Millas (100%):**
- Emisión automática tipo "Cash"
- Sin tarjeta de crédito
- Sin procesamiento en PlacetoPay

**Escenario 2: Millas+Plata (Copago):**
- Emisión automática tipo "Cash"
- Tarjeta de crédito ingresada en CheckOut
- Procesamiento PlacetoPay **bash** (en background, sin interfaz visual)
- **Consulta en Portal P2P:** Se puede verificar el valor pagado en USD, estado del pago, franquicia y número de TC

### 💰 MARKUP DE GANANCIA:

**Configuración de Markup:**
- **Tipo:** Porcentual
- **Porcentaje:** 25% del costo de la reserva
- **Configuración:** Desde el Administrador del Marketplace
- **Aplicación:** Calculado sobre el costo total de la reserva de hotel como ganancia para la empresa

---

## 🏨 PANTALLA DE DISPONIBILIDAD

**Funcionalidades disponibles:**

**Visualización:**
- 🗺️ **Ver mapa:** Hoteles en mapa con ubicaciones cercanas al destino buscado
- 📍 **Ver hotel en mapa:** Ubicación específica de un hotel individual
- 📷 **Ver fotos del hotel:** Galería de imágenes
- 📄 **Ver descripción del hotel:** Información detallada del establecimiento
- 🏠 **Ver habitaciones:** Diferentes tipos de habitación con costos en Millas

**Filtros:**
- 🔍 **Por nombre de hotel:** Búsqueda directa por nombre
- ⭐ **Por cantidad de estrellas:** Clasificación del hotel
- 🍽️ **Por Régimen:** Tipo de alimentación incluida

**Ordenamiento:**
- 💰 **Por precio:** Menor a mayor o Mayor a menor
- 🔤 **Por nombre:** Ascendente (A-Z) o Descendente (Z-A)

**Acciones:**
- 🔗 **Compartir:** Información de un hotel específico

---

## 🚫 POLÍTICAS DE CANCELACIÓN

**Tipos de políticas:**

**1. Con fecha de gastos de cancelación:**
- Si la cancelación se realiza **antes** de la fecha límite → Cancelación **gratuita**
- Si la cancelación se realiza **después** de la fecha límite → Se cobra penalidad

**Ejemplo:**
```
Fecha de reserva: Hoy
Fecha de gastos de cancelación: En 2 meses
Acción: Cancelar mañana → Gratuito (aún no llega la fecha límite)
Acción: Cancelar después de 2 meses → Con cargo
```

**2. Sin fecha de gastos de cancelación:**
- Cancelación **siempre gratuita**
- Sin penalidades en ningún momento

**IMPORTANTE:** Al crear casos de prueba, elegir hoteles con fechas de cancelación gratuita suficientemente alejadas (ej: 2 meses) para poder validar la cancelación sin cargos.

---

## 📋 PASOS OBLIGATORIOS DEL FLUJO E2E

**Siempre incluir estos pasos desde login:**

1. Ingresar a la URL https://clubmiles-ec.preprodppm.com/ | Portal cargado correctamente, pantalla principal visible
2. Realizar login con usuario y contraseña válidos | Login exitoso, acceso al home autenticado
3. Click en la opción Hoteles | Se despliega el formulario de búsqueda de hoteles
4. Diligenciar el campo Destino | Se habilita una lista de ciudades sugeridas
5. Seleccionar un destino de la lista | El destino queda registrado correctamente
6. Seleccionar Fecha de llegada (check-in) | Fecha seleccionada correctamente (no permite fechas pasadas)
7. Seleccionar Fecha de salida (check-out) | Fecha seleccionada correctamente (posterior a fecha de llegada)
8. Diligenciar Número de habitaciones | El valor queda registrado (mínimo 1)
9. Diligenciar Cantidad de adultos | El valor queda registrado (mínimo 1 por habitación)
10. Diligenciar Cantidad de menores | El valor queda registrado (0 o más)
11. Click en el botón Buscar | El sistema muestra la pantalla de disponibilidad con lista de hoteles de HotelBeds
12. Click en el botón Ver hotel de un hotel disponible | Se despliega el detalle del hotel con tipos de habitación disponibles
13. Validar que se muestra política de cancelación con fecha límite sin gastos | La fecha de cancelación gratuita es visible y correcta
14. Validar precio en millas | Millas visibles y correctas
15. Click en el botón Canjear de una habitación | El sistema redirige al checkout con los datos del hotel seleccionado
16. Validar opción de ver hotel en mapa de ubicación en CheckOut | Mapa de ubicación disponible y funcional
17. Diligenciar todos los campos obligatorios del checkout (datos de huésped principal, contacto) | Los campos quedan completos correctamente
18. Validar Slider en CheckOut ajustable (mínimo 20%, máximo 100% o Millas disponibles) | Slider visible y funcional según método de pago elegido
19. Ajustar Slider según el escenario de prueba (100% Millas o Copago) | Slider ajustado correctamente, cálculo dinámico visible
20. Si aplica Copago: Diligenciar datos de tarjeta de crédito | Datos de tarjeta ingresados y validados
21. Marcar el check Tratamiento de datos | El check se marca correctamente
22. Marcar el check Términos y condiciones y validar funcionamiento de los links | Los enlaces abren correctamente en nueva pestaña o modal
23. Validar que el botón Canjear se habilite cuando todos los campos están completos | Botón Canjear habilitado
24. Click en el botón Canjear | Se procesa el canje con emisión automática tipo "Cash", PlacetoPay bash en background si hay Copago
25. Si aplica Copago con tarjeta que requiere OTP: Ingresar código OTP en el modal | Modal OTP aparece, código ingresado correctamente
26. Validar pantalla de confirmación con código de reserva y detalles (hotel, fechas, habitaciones, millas canjeadas) | Código de reserva visible, datos completos y correctos
27. Ingresar al módulo de administración CME | Admin cargado correctamente
28. Buscar reserva por código | Reserva localizada y visible
29. Validar que las millas canjeadas estén correctas en admin (coinciden con confirmación) | Millas correctas
30. Validar que la reserva queda en estado EMITIDA automáticamente | Reserva en estado EMITIDA
31. Validar respuesta correcta del proveedor HotelBeds | Confirmación recibida de HotelBeds
32. Validar que NO hay voucher disponible para descarga en Admin | Confirmado: sin voucher descargable
33. Si aplica Copago: Ingresar al portal P2P y validar transacción (valor USD, estado, franquicia, número TC) | Transacción registrada correctamente en P2P

---

## 🔄 VARIACIONES SEGÚN ESCENARIO

**Destinos:**
- Ciudades nacionales (Quito, Guayaquil, Cuenca)
- Internacionales (Miami, Madrid, Buenos Aires, etc.)

**Habitaciones:**
- 1 habitación
- Múltiples habitaciones (2+)

**Huéspedes:**
- Solo adultos
- Adultos + menores
- Grupos

**Noches:**
- Estancia corta (1-3 noches)
- Estancia media (4-7 noches)
- Estancia larga (8+ noches)

**Políticas de cancelación:**
- Cancelación gratuita (sin fecha de gastos de cancelación)
- Con fecha de gastos de cancelación (gratuita antes de la fecha límite)
- Cancelación con cargo (después de fecha límite)

**Métodos de pago:**
- Solo Millas (100%)
- Millas+Plata (Copago 20%-99%)

**Funcionalidades de Disponibilidad:**
- Ver mapa de hoteles
- Filtros (nombre, estrellas, régimen)
- Ordenamiento (precio, nombre)
- Compartir información de hotel
- Ver fotos y descripción

---

## ✅ VALIDACIONES CRÍTICAS

✅ **Integridad de datos:** Consistencia entre búsqueda → disponibilidad → detalle → checkout → confirmación → admin  
✅ **Política de cancelación:** Fecha límite visible y correcta en disponibilidad y detalle del hotel  
✅ **Cálculo de millas:** Millas totales = (millas por noche × noches) × habitaciones  
✅ **Slider en CheckOut:** Visible solo en CheckOut, mínimo 20%, ajuste manual funcional, cálculo dinámico  
✅ **Campos obligatorios:** Datos de huésped principal por habitación, contacto, aceptación de términos  
✅ **Links funcionales:** Términos y condiciones, tratamiento de datos abren correctamente  
✅ **PlacetoPay bash:** Si aplica Copago, validar procesamiento en background sin interfaz visual  
✅ **Modal OTP:** Si aplica y tarjeta requiere OTP, validar modal y flujo completo  
✅ **Estados de reserva:** Confirmada en admin con todos los datos completos  
✅ **Emisión automática:** Reserva en estado EMITIDA sin intervención manual, tipo "Cash"  
✅ **Fechas:** Validación de check-in y check-out, noches calculadas correctamente  
✅ **Proveedor:** HotelBeds (único proveedor, validar respuesta correcta)  
✅ **Sin fee:** Confirmar que NO se cobra fee de procesamiento  
✅ **Sin voucher:** Validar que NO hay voucher disponible en Admin CME  
✅ **Límites HotelBeds:** Máximo 2 habitaciones y 9 pasajeros en total  
✅ **Pasajeros:** Validar adultos y niños correctamente registrados  
✅ **Políticas de cancelación:** Fecha límite visible y correcta según tipo de política  
✅ **Portal P2P:** Si aplica Copago, validar transacción en portal P2P (valor USD, estado, franquicia, número TC)  
✅ **Mapa en CheckOut:** Validar opción de ver hotel en mapa de ubicación  
✅ **Disponibilidad:** Validar filtros, ordenamiento y opciones de visualización funcionando correctamente  
✅ **Markup 25%:** Validar que la ganancia se calcula correctamente en el admin

---

## 📝 FORMATO DE TÍTULO

```
[CME] Hoteles - [Noches] - [Destino] - [Característica especial]
```

**Ejemplos:**
- `[CME] Hoteles - 2 noches - Quito - HotelBeds - Cancelación gratuita - Solo Millas`
- `[CME] Hoteles - 5 noches - Miami - 2 habitaciones - Copago 50%`
- `[CME] Hoteles - 3 noches - Madrid - Cancelación con cargo - 2 adultos + 1 menor`

---

## 📸 IMÁGENES DE REFERENCIA

Incluir SIEMPRE estas imágenes en el campo Descriptions del Test Case:

- Home-hoteles-CME.png - Pantalla principal con opción Hoteles
- Disponibilidad-hoteles-CME.png - Lista de hoteles disponibles
- Detalle-hotel-CME.png - Detalle del hotel con política de cancelación
- Checkout-hoteles-CME.png - Formulario de checkout completo con Slider visible
- Confirmacion-hoteles-CME.png - Pantalla de confirmación con código de reserva
- Admin.png - Validación en módulo admin CME (sin voucher)

---

## 📌 NOTAS IMPORTANTES

**Sin fee de procesamiento:**
- Diferenciador clave vs vuelos (vuelos SÍ tienen fee obligatorio)
- Solo se paga el producto con Millas o Millas+Plata
- No se requiere tarjeta de crédito si pago es 100% Millas

**Sin voucher:**
- Los hoteles NO generan voucher descargable en Admin
- Diferente a vuelos (que sí tienen voucher excepto con seguro)

**Slider y Copago:**
- Misma lógica que todos los productos CME
- Mínimo 20% del valor del producto
- Ajuste manual por el socio
- PlacetoPay bash en background si hay Copago (sin interfaz visual)

**Políticas de cancelación:**
- Variables según hotel seleccionado
- Fecha límite debe ser visible en disponibilidad y detalle
- Validar que la información es consistente en todas las pantallas

**Emisión:**
- Siempre automática
- Estado EMITIDA inmediato tras confirmación
- Tipo "Cash" en backend
- Sin proceso manual

**Proveedor:**
- HotelBeds es el único proveedor
- No hay proveedores alternativos como en vuelos
- Validar respuesta correcta de HotelBeds en admin

**Límites del proveedor HotelBeds:**
- Máximo 2 habitaciones por reserva
- Máximo 9 pasajeros en total (adultos y niños)
- Los pasajeros pueden distribuirse entre las habitaciones

**Políticas de cancelación detalladas:**
- **Con fecha límite:** Cancelación gratuita antes de la fecha, con cargo después
- **Sin fecha límite:** Cancelación siempre gratuita
- Al crear casos de prueba, elegir fechas de cancelación alejadas (ej: 2 meses) para validar cancelaciones sin cargo

**Portal PlacetoPay (P2P):**
- Procesamiento bash en background (sin interfaz visual)
- Consulta de transacciones en portal P2P: valor USD, estado, franquicia, número TC
- Solo aplica cuando hay Copago (Millas+Plata)

**Markup de ganancia:**
- Configurado en Administrador del Marketplace
- Tipo: Porcentual al 25%
- Aplicado sobre el costo total de la reserva
- Representa la ganancia de la empresa por cada reserva

**Funcionalidades de Disponibilidad:**
- Ver hoteles en mapa con ubicaciones cercanas
- Filtros por nombre, estrellas y régimen
- Ordenamiento por precio y nombre
- Compartir información de hoteles
- Ver fotos, descripción y habitaciones disponibles

---

## 🔗 REFERENCIAS

**Documentación relacionada:**
- [CME_COMMON_RULES.md](../../../../shared/Kepler/CME_COMMON_RULES.md) - Reglas comunes CME (Slider, métodos de pago, emisión, escenarios)
- [SHARED_QA_RULES.md](../../../../shared/SHARED_QA_RULES.md) - Fundamentos ISTQB y Azure DevOps
- [Kepler_Models_Comparison.md](../../../../docs/comparisons/Kepler_Models_Comparison.md) - Comparación entre modelos

---

**Última actualización:** 2026-02-05  
**Versión:** 2.0.0 (Optimizado - Sin redundancia)  
**Mantenido por:** QA Team Ultragroup  
**Cambios:** Eliminada redundancia de explicaciones ya documentadas en COMMON_RULES, mantenida estructura similar a vuelos, enfocado en características específicas de hoteles
