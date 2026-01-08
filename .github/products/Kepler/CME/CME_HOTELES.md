# 🏨 FLUJO E2E OBLIGATORIO PARA HOTELES - CME

**Proveedor:** Club Millas Ecuador  
**Portal:** https://clubmiles-ec.preprodppm.com/ 
**Tecnología:** Angular (TypeScript/JavaScript)  
**Modelo de pago:** 100% Millas (sin fee, sin tarjeta de crédito)  

---

## 📦 PROVEEDORES DISPONIBLES

**Proveedor:** HotelBeds (único)

---

## 📋 PASOS OBLIGATORIOS DEL FLUJO E2E

**Siempre incluir estos pasos desde login para el flujo de Hoteles:**

1. Ingresar a la URL https://clubmiles-ec.preprodppm.com/ | Portal cargado correctamente, pantalla principal visible
2. Realizar login con un usuario válido | Login exitoso y acceso al home del portal
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
16. Diligenciar todos los campos obligatorios del checkout (datos de huésped principal, contacto) | Los campos quedan completos correctamente
17. Marcar el check Tratamiento de datos | El check se marca correctamente
18. Marcar el check Términos y condiciones y validar funcionamiento de los links | Los enlaces abren correctamente en nueva pestaña o modal
19. Validar que el botón Canjear se habilite cuando todos los campos están completos | Botón Canjear habilitado
20. Click en el botón Canjear | Se procesa el canje (100% millas) y se muestra pantalla de confirmación
21. Validar pantalla de confirmación con código de reserva y detalles (hotel, fechas, millas canjeadas) | Código de reserva visible, datos completos y correctos
22. Ingresar al Admin CME | Admin cargado correctamente
23. Buscar reserva por código | Reserva localizada
24. Validar que las millas canjeadas estén correctas en admin (coinciden con confirmación) | Millas correctas
25. Validar que la reserva queda emitida automáticamente (100% millas - proceso automático) | Reserva en estado EMITIDA
26. Validar respuesta correcta del proveedor HotelBeds | Confirmación recibida de HotelBeds

---

## 🔄 VARIACIONES SEGÚN ESCENARIO

**Destinos:**
- Ciudades nacionales (Quito, Guayaquil, Cuenca)
- Internacionales (Miami, Madrid, Buenos Aires, etc.)

**Habitaciones:**
- 1 habitación
- Múltiples habitaciones

**Huéspedes:**
- Solo adultos
- Adultos + menores
- Grupos

**Políticas de cancelación:**
- Cancelación gratuita
- Cancelación con cargo
- No reembolsable

---

## ✅ VALIDACIONES CRÍTICAS

✅ **Integridad de datos:** Consistencia entre búsqueda → disponibilidad → detalle → checkout → confirmación → admin  
✅ **Política de cancelación:** Fecha límite visible y correcta en disponibilidad y detalle  
✅ **Cálculo de millas:** Millas totales = (millas por noche × noches) × habitaciones  
✅ **Campos obligatorios:** Datos de huésped principal, contacto, aceptación de términos  
✅ **Links funcionales:** Términos y condiciones, tratamiento de datos abren correctamente  
✅ **Estados de reserva:** Confirmada en admin con todos los datos completos  
✅ **Fechas:** Validación de check-in y check-out, noches calculadas correctamente  
✅ **Proveedor:** HotelBeds (validar respuesta correcta)  
✅ **Pago:** 100% Millas (sin fee, sin tarjeta de crédito)

---

## 📝 FORMATO DE TÍTULO

```
[CME] Hoteles - [Noches] - [Destino] - [Característica especial]
```

**Ejemplos:**
- `[CME] Hoteles - 2 noches - Quito - HotelBeds - Cancelación gratuita`
- `[CME] Hoteles - 5 noches - Miami - 2 habitaciones - 4 adultos`
- `[CME] Hoteles - 3 noches - Madrid - No reembolsable - 2 adultos + 1 menor`

---

## 📸 IMÁGENES DE REFERENCIA

Incluir SIEMPRE estas imágenes en el campo Descriptions del Test Case:

- Home-hoteles-CME.png - Pantalla principal con opción Hoteles
- Disponibilidad-hoteles-CME.png - Lista de hoteles disponibles
- Detalle-hotel-CME.png - Detalle del hotel seleccionado
- Checkout-hoteles-CME.png - Formulario de checkout completo
- Confirmacion-hoteles-CME.png - Pantalla de confirmación con código de reserva
- Admin.png - Validación en módulo admin CME

---

**Última actualización:** 2026-01-06  
**Versión:** 1.0.0  
**Mantenido por:** QA Team Ultragroup
