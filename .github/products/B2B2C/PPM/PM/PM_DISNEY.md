# 🎡 FLUJO E2E OBLIGATORIO PARA TICKETS DISNEY - PICHINCHA MILES

**Proveedor:** Pichincha Miles Ecuador

**Portales:**

- 🧪 **TEST:** https://pichinchamiles-ec.developppm.com/?operation=uv
- 🎯 **DEMO:** https://pichinchamiles-ec.preprodppm.com/?operation=uv

**Tecnología:** React (TypeScript/JavaScript)

**Modelo de pago:** 100% Millas o Millas + Plata (sin fee, sin tarjeta de crédito)

**Promocode:** ✅ SÍ APLICA (campo opcional en búsqueda)

**Markup:** ❌ NO APLICA (solo Hoteles y Actividades tienen Markup)  

---

## 📦 PROVEEDORES DISPONIBLES

**Proveedor:** DerbySoft (único)

---

## 🎢 TIPOS DE TICKETS DISPONIBLES

### Tickets individuales por parque

- Magic Kingdom
- Epcot
- Hollywood Studios
- Animal Kingdom

### Tickets con múltiples beneficios

- **Park Hopper:** Visita más de 1 parque el mismo día
- **Park Hopper Plus:** Visita múltiples parques + parques acuáticos + ESPN Sports

### Opciones adicionales

- Parques acuáticos
- Experiencia ESPN Sport

---

## 📋 PASOS OBLIGATORIOS DEL FLUJO E2E

**Siempre incluir estos pasos desde login para el flujo de Tickets Disney:**

1. Ingresar al portal (TEST: https://pichinchamiles-ec.developppm.com/?operation=uv o DEMO: https://pichinchamiles-ec.preprodppm.com/?operation=uv) | El portal carga correctamente y muestra la pantalla de inicio
2. Ingresar usuario y contraseña válidos según el entorno | Credenciales aceptadas, sistema solicita código OTP
3. Ingresar código OTP recibido en el correo pruebasotp@ultragroupla.com | Código OTP validado, login exitoso y acceso al home
3. Click en la opción Disney | Se despliega el formulario de búsqueda para Tickets Disney
4. Seleccionar Fecha de entrada | Fecha registrada correctamente
5. Seleccionar Número de pasajeros | Valores registrados correctamente
6. Click en el botón Buscar | Se muestra la pantalla de disponibilidad con diferentes tipos de entradas
7. Validar listado de opciones disponibles (Park Hopper, Park Hopper Plus, Magic Kingdom, Epcot, Hollywood Studios, Animal Kingdom, Parques acuáticos, ESPN Sports, etc.) | Todas las opciones disponibles se muestran correctamente según el día seleccionado
8. Click en el botón Seleccionar de una de las entradas | Se despliegan las opciones de precio asociadas al ticket
9. Validar que se muestren precios y opciones según el tipo de ticket | Información consistente según producto seleccionado
10. Click en el botón Seleccionar de la opción escogida | El sistema redirige al checkout
11. Diligenciar todos los campos obligatorios en checkout (datos de pasajeros, contacto) | Campos completados correctamente
12. Marcar el check Tratamiento de datos | Check seleccionado
13. Marcar el check Términos y condiciones | Check seleccionado
14. Validar que los enlaces de Tratamiento de datos y Términos y condiciones funcionan | Los links abren correctamente en nueva pestaña
15. Validar que el botón Canjear se habilite únicamente cuando todos los campos obligatorios estén completos | Botón habilitado
16. Click en el botón Canjear | Se procesa el canje (100% millas) y se muestra pantalla de confirmación
17. Validar pantalla de confirmación con código de reserva, millas canjeadas y detalles del ticket | Valores y detalles correctos
18. Ingresar al Admin Pichincha Miles | Admin cargado correctamente
19. Buscar reserva por código | Reserva localizada
20. Validar que las millas canjeadas estén correctas en admin (coinciden con confirmación) | Millas correctas
21. Validar que la reserva queda emitida automáticamente (100% millas - proceso automático) | Reserva en estado EMITIDA
22. Validar procesamiento correcto del proveedor DerbySoft | Confirmación recibida de DerbySoft

---

## 🔄 VARIACIONES SEGÚN ESCENARIO

### Proveedor

- DerbySoft (único)

### Tipos de tickets

- Park Hopper
- Park Hopper Plus
- Magic Kingdom (individual)
- Epcot (individual)
- Hollywood Studios (individual)
- Animal Kingdom (individual)

### Opciones adicionales

- Parques acuáticos
- Experiencia ESPN Sport
- Visita más de 1 parque el mismo día (Park Hopper/Plus)

### Participantes

- 1 a N pasajeros (adultos, niños según edad)

### Fechas

- Diferentes fechas de entrada validando disponibilidad

---

## ✅ VALIDACIONES CRÍTICAS

- ✅ **Flujo completo:** Home → Búsqueda → Disponibilidad → Selección ticket → Checkout → Confirmación → Admin
- ✅ **Tipos tickets:** Park Hopper, Park Hopper Plus, individuales (Magic Kingdom, Epcot, Hollywood, Animal Kingdom)
- ✅ **Opciones incluidas:** Parques acuáticos, ESPN Sports, multi-parque visibles correctamente
- ✅ **Cálculo millas:** Precio ticket × cantidad pasajeros | Consistencia en todas pantallas
- ✅ **Campos obligatorios:** Datos pasajeros completos, contacto, términos | Links funcionales
- ✅ **Emisión automática** 100% millas (sin fee, sin tarjeta) | Estado EMITIDA
- ✅ **Proveedor DerbySoft:** Procesamiento correcto | Fecha entrada válida

---

## 📝 FORMATO DE TÍTULO

```plaintext
[PM] Disney - [Tipo ticket] - [Pasajeros] - [Variante]
```

**Ejemplos:**

- `[PM] Disney - Park Hopper - 2 adultos + 1 niño`
- `[PM] Disney - Magic Kingdom - 1 adulto - Entrada individual`
- `[PM] Disney - Park Hopper Plus - 4 adultos - Con parques acuáticos`
