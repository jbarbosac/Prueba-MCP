# 🎢 FLUJO E2E OBLIGATORIO PARA ACTIVIDADES - PICHINCHA MILES

**Proveedor:** Pichincha Miles Ecuador

**Portales:**

- 🧪 **TEST:** https://pichinchamiles-ec.developppm.com/
- 🎯 **DEMO:** https://pichinchamiles-ec.preprodppm.com/

**Tecnología:** Angular (TypeScript/JavaScript)

**Modelo de pago:** 100% Millas o Millas + Plata (sin fee, sin tarjeta de crédito)

**Promocode:** ✅ SÍ APLICA (campo opcional en búsqueda)

**Markup:** ✅ SÍ APLICA (impuesto/recargo incluido en precio)  

---

## 💰 MARKUP EN ACTIVIDADES

**Markup:** Impuesto/recargo incluido en el precio final. No se muestra separado.

### Tipos

#### 1️⃣ Porcentual (%)

**Fórmula:** `Precio base × % markup`

**Ejemplo:** 5%, 10%

#### 2️⃣ Fijo

**Fórmula:** `Precio base + Markup fijo`

**Ejemplo:** 1,500 millas, 2,500 millas

### Ejemplo

```plaintext
Precio base: 15,000 millas | Markup 10%: 1,500 millas
Precio final: 16,500 millas → 2 personas: 33,000 millas
```

### Validaciones

- ✅ Precio mostrado incluye markup | Cálculo correcto | Consistencia en todas las pantallas  

---

## 📦 PROVEEDORES DISPONIBLES

**Proveedor:** HotelBeds (único)

---

## 📋 PASOS OBLIGATORIOS DEL FLUJO E2E

**Siempre incluir estos pasos desde login para el flujo de Actividades:**

1. Ingresar al portal (TEST: https://pichinchamiles-ec.developppm.com/ o DEMO: https://pichinchamiles-ec.preprodppm.com/) | El portal carga correctamente y muestra la pantalla de inicio
2. Ingresar usuario y contraseña válidos según el entorno | Credenciales aceptadas, sistema solicita código OTP
3. Ingresar código OTP recibido en el correo pruebasotp@ultragroupla.com | Código OTP validado, login exitoso y acceso al home
3. Click en la opción Actividades | Se despliega el formulario de búsqueda con opciones disponibles
4. Diligenciar el campo Ciudad | Se despliega una lista de ciudades sugeridas
5. Seleccionar una ciudad de la lista | La ciudad queda registrada correctamente
6. Seleccionar Fecha de salida | La fecha queda registrada
7. Seleccionar Edad (si aplica) | El valor queda registrado correctamente
8. Click en el botón Buscar | Se muestra la pantalla de disponibilidad de actividades
9. Validar que se listan diferentes actividades disponibles | Se visualizan actividades con nombre, precio y detalles
10. Click en el botón Ver detalle | Se muestra el detalle de la actividad seleccionada
11. Validar precio, cantidad de personas y descripción | La información corresponde al producto
12. Click en el botón Canjear de una actividad | Se redirige al checkout con los datos de la actividad
13. Diligenciar todos los campos obligatorios (datos de participantes, contacto) | Campos completados correctamente
14. Marcar el check Tratamiento de datos | Check marcado correctamente
15. Marcar el check Términos y condiciones | Check marcado correctamente
16. Validar que los links de Tratamiento de datos y Términos y condiciones funcionan | Los enlaces abren correctamente
17. Validar que el botón Canjear se habilite cuando todos los obligatorios están diligenciados | Botón habilitado
18. Click en el botón Canjear | Se procesa el canje (100% millas) y se muestra pantalla de confirmación
19. Validar pantalla de confirmación con código de reserva y millas canjeadas | Valor correcto y consistente con checkout
20. Ingresar al Admin Pichincha Miles | Admin cargado correctamente
21. Buscar reserva por código | Reserva localizada
22. Validar que las millas canjeadas estén correctas en admin (coinciden con confirmación) | Millas correctas
23. Validar que la reserva queda emitida automáticamente (100% millas - proceso automático) | Reserva en estado EMITIDA
24. Validar respuesta correcta del proveedor HotelBeds | Confirmación recibida de HotelBeds

---

## 🔄 VARIACIONES SEGÚN ESCENARIO

### Proveedor

- HotelBeds (único)

### Ciudades

- Destinos nacionales (Quito, Guayaquil, Cuenca, Manta)
- Internacionales (Lima, Bogotá, Buenos Aires, Cancún, etc.)

### Tipo de actividades

- Tours
- Experiencias
- Entradas a parques
- Actividades acuáticas
- Actividades culturales

### Edad

- Algunas actividades requieren validación de edad (menores, adultos, tercera edad)

### Participantes

- 1 persona
- Grupos
- Capacidad máxima por actividad

---

## ✅ VALIDACIONES CRÍTICAS

- ✅ **Flujo completo:** Home → Búsqueda → Disponibilidad → Detalle → Checkout → Confirmación → Admin
- ✅ **Detalle actividad:** Precio, descripción, cantidad personas, condiciones visibles
- ✅ **Cálculo millas:** Precio base × cantidad personas | Consistencia en todas pantallas
- ✅ **Campos obligatorios:** Datos participantes, contacto, términos | Links funcionales
- ✅ **Edad:** Restricciones validadas según tipo actividad | Fecha salida válida
- ✅ **Emisión automática** 100% millas (sin fee, sin tarjeta) | Estado EMITIDA
- ✅ **Proveedor HotelBeds:** Respuesta correcta

---

## 📝 FORMATO DE TÍTULO

```plaintext
[PM] Actividades - [Ciudad] - [Tipo] - [Variante]
```

**Ejemplos:**

- `[PM] Actividades - Quito - City Tour - 2 personas`
- `[PM] Actividades - Cancún - Actividad acuática - Edad mínima`
- `[PM] Actividades - Lima - Entrada parque - Grupo 5 personas`
