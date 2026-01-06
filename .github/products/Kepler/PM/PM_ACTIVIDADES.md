# 🎢 FLUJO E2E OBLIGATORIO PARA ACTIVIDADES - PICHINCHA MILES

**Proveedor:** Pichincha Miles Ecuador  
**Portal:** https://pichinchamiles-ec.preprodppm.com/  
**Tecnología:** Angular (TypeScript/JavaScript)  
**Modelo de pago:** 100% Millas (sin fee, sin tarjeta de crédito)  

---

## 📦 PROVEEDORES DISPONIBLES

**Proveedor:** HotelBeds (único)

---

## 📋 PASOS OBLIGATORIOS DEL FLUJO E2E

**Siempre incluir estos pasos desde login para el flujo de Actividades:**

1. Ingresar a la URL https://pichinchamiles-ec.preprodppm.com/ | El portal carga correctamente y muestra la pantalla de inicio
2. Realizar login con un usuario válido | Login exitoso y acceso al home
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

**Proveedor:**
- HotelBeds (único)

**Ciudades:**
- Destinos nacionales (Quito, Guayaquil, Cuenca, Manta)
- Internacionales (Lima, Bogotá, Buenos Aires, Cancún, etc.)

**Tipo de actividades:**
- Tours
- Experiencias
- Entradas a parques
- Actividades acuáticas
- Actividades culturales

**Edad:**
- Algunas actividades requieren validación de edad (menores, adultos, tercera edad)

**Participantes:**
- 1 persona
- Grupos
- Capacidad máxima por actividad

---

## ✅ VALIDACIONES CRÍTICAS

✅ **Integridad de datos:** Consistencia entre búsqueda → disponibilidad → detalle → checkout → confirmación → admin  
✅ **Proveedor:** HotelBeds (validar respuesta correcta del proveedor)  
✅ **Detalle de actividad:** Precio, descripción completa, cantidad de personas, condiciones visibles  
✅ **Cálculo de millas:** Millas totales = precio base × cantidad de personas  
✅ **Campos obligatorios:** Datos de participantes, contacto, aceptación de términos  
✅ **Links funcionales:** Términos y condiciones, tratamiento de datos abren correctamente  
✅ **Estados de reserva:** Confirmada en admin con todos los datos completos  
✅ **Fechas:** Validación de fecha de salida, disponibilidad de la actividad para fecha seleccionada  
✅ **Edad:** Restricciones de edad validadas correctamente según tipo de actividad  
✅ **Pago:** 100% Millas (sin fee, sin tarjeta de crédito)

---

## 📝 FORMATO DE TÍTULO

```
[PM] Actividades - [Ciudad] - [Tipo de actividad] - [Característica especial]
```

**Ejemplos:**
- `[PM] Actividades - Quito - City Tour - HotelBeds - 2 personas`
- `[PM] Actividades - Cancún - Actividad acuática - Validación edad mínima`
- `[PM] Actividades - Lima - Entrada a parque - Grupo de 5 personas`
