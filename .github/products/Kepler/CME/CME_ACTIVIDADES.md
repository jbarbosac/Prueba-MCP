# 🎢 FLUJO E2E OBLIGATORIO PARA ACTIVIDADES - CME

**Proveedor:** Correos Millas Ecuador  
**Portal:** https://correosmillas-ec.preprodppm.com/  
**Tecnología:** Angular (TypeScript/JavaScript)  
**Modelo de pago:** 100% Millas (sin fee, sin tarjeta de crédito)  

---

## 📦 PROVEEDORES DISPONIBLES

**Proveedor:** HotelBeds (único)

---

## 📋 PASOS OBLIGATORIOS DEL FLUJO E2E

**Siempre incluir estos pasos desde login para el flujo de Actividades:**

1. Ingresar a la URL https://correosmillas-ec.preprodppm.com/ | Portal cargado correctamente, pantalla principal visible
2. Realizar login con un usuario válido | Login exitoso y acceso al home del portal
3. Click en la opción Actividades | Se despliega el formulario de búsqueda de actividades
4. Diligenciar el campo Destino | Se habilita una lista de ciudades sugeridas
5. Seleccionar un destino de la lista | El destino queda registrado correctamente
6. Seleccionar Fecha de inicio de la actividad | Fecha seleccionada correctamente (no permite fechas pasadas)
7. Seleccionar Fecha de fin (si aplica para tours de múltiples días) | Fecha seleccionada correctamente
8. Diligenciar Cantidad de adultos | El valor queda registrado (mínimo 1)
9. Diligenciar Cantidad de menores (si aplica) | El valor queda registrado (0 o más)
10. Click en el botón Buscar | El sistema muestra la pantalla de disponibilidad con lista de actividades de HotelBeds
11. Validar que se muestran diferentes tipos de actividades (tours, excursiones, traslados, entradas) | Lista de actividades visible
12. Click en el botón Ver actividad de una actividad disponible | Se despliega el detalle de la actividad seleccionada
13. Validar descripción completa de la actividad (duración, horarios, incluye, no incluye) | Información completa visible
14. Validar precio en millas por persona | Millas por persona visibles y correctas
15. Validar política de cancelación | Política de cancelación visible y clara
16. Validar imágenes de la actividad | Imágenes cargadas correctamente
17. Click en el botón Canjear | El sistema redirige al checkout con los datos de la actividad seleccionada
18. Diligenciar todos los campos obligatorios del checkout (datos de participante principal, contacto) | Los campos quedan completos correctamente
19. Validar cálculo de millas totales (millas por persona × cantidad de personas) | Cálculo correcto visible
20. Marcar el check Tratamiento de datos | El check se marca correctamente
21. Marcar el check Términos y condiciones y validar funcionamiento de los links | Los enlaces abren correctamente en nueva pestaña o modal
22. Validar que el botón Canjear se habilite cuando todos los campos están completos | Botón Canjear habilitado
23. Click en el botón Canjear | Se procesa el canje (100% millas) y se muestra pantalla de confirmación
24. Validar pantalla de confirmación con código de reserva y detalles (actividad, fecha, participantes, millas canjeadas) | Código de reserva visible, datos completos y correctos
25. Ingresar al Admin CME | Admin cargado correctamente
26. Buscar reserva por código | Reserva localizada
27. Validar que las millas canjeadas estén correctas en admin (coinciden con confirmación) | Millas correctas
28. Validar que la reserva queda emitida automáticamente (100% millas - proceso automático) | Reserva en estado EMITIDA
29. Validar respuesta correcta del proveedor HotelBeds | Confirmación recibida de HotelBeds
30. Validar voucher o comprobante de la actividad | Voucher disponible para descarga o envío

---

## 🔄 VARIACIONES SEGÚN ESCENARIO

**Tipos de actividades:**
- Tours guiados
- Excursiones
- Traslados aeropuerto-hotel
- Entradas a parques o museos
- Actividades acuáticas
- Actividades de aventura

**Destinos:**
- Actividades nacionales (Quito, Guayaquil, Galápagos)
- Actividades internacionales (Orlando, Cancún, Buenos Aires)

**Duración:**
- Medio día
- Día completo
- Múltiples días

**Participantes:**
- Solo adultos
- Adultos + menores
- Grupos grandes

**Horarios:**
- Mañana
- Tarde
- Noche

---

## ✅ VALIDACIONES CRÍTICAS

✅ **Integridad de datos:** Consistencia entre búsqueda → disponibilidad → detalle → checkout → confirmación → admin  
✅ **Descripción completa:** Duración, horarios, incluye, no incluye, punto de encuentro  
✅ **Cálculo de millas:** Millas totales = millas por persona × cantidad de personas  
✅ **Campos obligatorios:** Datos de participante principal, contacto, aceptación de términos  
✅ **Links funcionales:** Términos y condiciones, tratamiento de datos abren correctamente  
✅ **Estados de reserva:** Confirmada en admin con todos los datos completos  
✅ **Fecha:** Validación de fecha, no permite fechas pasadas  
✅ **Política de cancelación:** Visible y clara  
✅ **Proveedor:** HotelBeds (validar respuesta correcta)  
✅ **Voucher:** Disponible para descarga o envío  
✅ **Pago:** 100% Millas (sin fee, sin tarjeta de crédito)

---

## 📝 FORMATO DE TÍTULO

```
[CME] Actividades - [Tipo] - [Destino] - [Característica especial]
```

**Ejemplos:**
- `[CME] Actividades - Tour guiado - Quito - Centro Histórico - Día completo`
- `[CME] Actividades - Excursión - Galápagos - Snorkeling - 2 adultos`
- `[CME] Actividades - Traslado - Aeropuerto Quito - Hotel - 1 persona`

---

## 📸 IMÁGENES DE REFERENCIA

Incluir SIEMPRE estas imágenes en el campo Descriptions del Test Case:

- Home-actividades-CME.png - Pantalla principal con opción Actividades
- Disponibilidad-actividades-CME.png - Lista de actividades disponibles
- Detalle-actividad-CME.png - Detalle de la actividad seleccionada
- Checkout-actividades-CME.png - Formulario de checkout completo
- Confirmacion-actividades-CME.png - Pantalla de confirmación con código de reserva
- Admin.png - Validación en módulo admin CME

---

**Última actualización:** 2026-01-06  
**Versión:** 1.0.0  
**Mantenido por:** QA Team Ultragroup
