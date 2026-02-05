# 🏨 FLUJO E2E OBLIGATORIO PARA HOTELES - PICHINCHA MILES

**Proveedor:** Pichincha Miles Ecuador

**Portales:**

- 🧪 **TEST:** https://pichinchamiles-ec.developppm.com/
- 🎯 **DEMO:** https://pichinchamiles-ec.preprodppm.com/

**Tecnología:** Angular (TypeScript/JavaScript)

**Modelo de pago:** 100% Millas o Millas + Plata (sin fee, sin tarjeta de crédito)

**Promocode:** ✅ SÍ APLICA (campo opcional en búsqueda)

**Markup:** ✅ SÍ APLICA (impuesto/recargo incluido en precio)  

---

## 💰 MARKUP EN HOTELES

**Markup:** Impuesto/recargo incluido en el precio final. No se muestra separado.

### Tipos

#### 1️⃣ Porcentual (%)

**Fórmula:** `Precio base × % markup`

**Ejemplo:** 8%, 10%

#### 2️⃣ Fijo

**Fórmula:** `Precio base + Markup fijo`

**Ejemplo:** 2,000 millas, 3,500 millas

### Ejemplo

```plaintext
Precio base/noche: 10,000 millas | Markup 8%: 800 millas
Precio final/noche: 10,800 millas → 3 noches: 32,400 millas
```

### Validaciones

- ✅ Precio mostrado incluye markup | Cálculo correcto | Consistencia en todas las pantallas  

---

## 📦 PROVEEDORES DISPONIBLES

**Proveedor:** HotelBeds (único)

---

## 📋 PASOS OBLIGATORIOS DEL FLUJO E2E

**Siempre incluir estos pasos desde login para el flujo de Hoteles:**

1. Ingresar al portal (TEST: https://pichinchamiles-ec.developppm.com/ o DEMO: https://pichinchamiles-ec.preprodppm.com/) | Portal cargado correctamente, pantalla principal visible
2. Ingresar usuario y contraseña válidos según el entorno | Credenciales aceptadas, sistema solicita código OTP
3. Ingresar código OTP recibido en el correo pruebasotp@ultragroupla.com | Código OTP validado, login exitoso y acceso al home del portal
4. Click en la opción Hoteles | Se despliega el formulario de búsqueda de hoteles
5. Diligenciar el campo Destino | Se habilita una lista de ciudades sugeridas
6. Seleccionar un destino de la lista | El destino queda registrado correctamente
7. Seleccionar Fecha de llegada (check-in) | Fecha seleccionada correctamente (no permite fechas pasadas)
8. Seleccionar Fecha de salida (check-out) | Fecha seleccionada correctamente (posterior a fecha de llegada)
9. Diligenciar Número de habitaciones | El valor queda registrado (mínimo 1)
9. Diligenciar Cantidad de adultos | El valor queda registrado (mínimo 1 por habitación)
10. Diligenciar Cantidad de menores | El valor queda registrado (0 o más)
11. Click en el botón Buscar | El sistema muestra la pantalla de disponibilidad con lista de hoteles de HotelBeds
12. Click en el botón Ver hotel de un hotel disponible | Se despliega el detalle del hotel con tipos de habitación disponibles
13. Validar que se muestra política de cancelación con fecha límite sin gastos | La fecha de cancelación gratuita es visible y correcta
14. Validar precio en millas y fee de procesamiento | Millas y fee visibles
15. Click en el botón Canjear de una habitación | El sistema redirige al checkout con los datos del hotel seleccionado
16. Diligenciar todos los campos obligatorios del checkout (datos de huésped principal, contacto) | Los campos quedan completos correctamente
17. Marcar el check Tratamiento de datos | El check se marca correctamente
18. Marcar el check Términos y condiciones y validar funcionamiento de los links | Los enlaces abren correctamente en nueva pestaña o modal
19. Validar que el botón Canjear se habilite cuando todos los campos están completos | Botón Canjear habilitado
20. Click en el botón Canjear | Se procesa el canje (100% millas) y se muestra pantalla de confirmación
21. Validar pantalla de confirmación con código de reserva y detalles (hotel, fechas, millas canjeadas) | Código de reserva visible, datos completos y correctos
22. Ingresar al Admin Pichincha Miles | Admin cargado correctamente
23. Buscar reserva por código | Reserva localizada
24. Validar que las millas canjeadas estén correctas en admin (coinciden con confirmación) | Millas correctas
25. Validar que la reserva queda emitida automáticamente (100% millas - proceso automático) | Reserva en estado EMITIDA
26. Validar respuesta correcta del proveedor HotelBeds | Confirmación recibida de HotelBeds

---

## 🔄 VARIACIONES SEGÚN ESCENARIO

### Destinos

- Ciudades nacionales (Quito, Guayaquil, Cuenca)
- Internacionales (Miami, Madrid, Buenos Aires, etc.)

### Habitaciones

- 1 habitación
- Múltiples habitaciones

### Huéspedes

- Solo adultos
- Adultos + menores
- Grupos

### Políticas de cancelación

- Cancelación gratuita
- Cancelación con cargo
- No reembolsable

---

## ✅ VALIDACIONES CRÍTICAS

- ✅ **Flujo completo:** Home → Búsqueda → Disponibilidad → Detalle → Checkout → Confirmación → Admin
- ✅ **Política cancelación** visible con fecha límite sin gastos
- ✅ **Cálculo millas:** (millas/noche × noches) × habitaciones | Consistencia en todas las pantallas
- ✅ **Campos obligatorios** completos: Huésped principal, contacto, términos | Links funcionales
- ✅ **Emisión automática** 100% millas (sin fee, sin tarjeta) | Estado EMITIDA en admin
- ✅ **Proveedor HotelBeds:** Respuesta correcta | Fechas y noches validadas

---

## 📝 FORMATO DE TÍTULO

```plaintext
[PM] Hoteles - [Noches] - [Destino] - [Variante]
```

**Ejemplos:**

- `[PM] Hoteles - 2 noches - Quito - Cancelación gratuita`
- `[PM] Hoteles - 5 noches - Miami - 2 habitaciones`
- `[PM] Hoteles - 3 noches - Madrid - No reembolsable`
