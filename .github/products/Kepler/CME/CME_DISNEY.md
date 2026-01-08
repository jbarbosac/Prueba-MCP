# 🎡 FLUJO E2E OBLIGATORIO PARA DISNEY - CME

**Proveedor:** Club Millas Ecuador  
**Portal:** https://clubmiles-ec.preprodppm.com/  
**Tecnología:** React (JavaScript/TypeScript)  
**Modelo de pago:** 100% Millas (sin fee, sin tarjeta de crédito)  

---

## 📦 PROVEEDORES DISPONIBLES

**Proveedor:** DerbySoft (único)

---

## 📋 PASOS OBLIGATORIOS DEL FLUJO E2E

**Siempre incluir estos pasos desde login para el flujo de Tickets Disney:**

1. Ingresar a la URL https://clubmiles-ec.preprodppm.com/ | Portal cargado correctamente, pantalla principal visible
2. Realizar login con un usuario válido | Login exitoso y acceso al home del portal
3. Click en la opción Tickets Disney | Se despliega el formulario de búsqueda de tickets Disney
4. Seleccionar tipo de ticket (parque único o park hopper) | Tipo de ticket seleccionado correctamente
5. Seleccionar parque(s) (Magic Kingdom, Epcot, Hollywood Studios, Animal Kingdom) | Parque(s) seleccionado(s) correctamente
6. Seleccionar cantidad de días (1, 2, 3, 4, 5 días o más) | Cantidad de días registrada correctamente
7. Seleccionar Fecha de inicio | Fecha seleccionada correctamente (no permite fechas pasadas)
8. Diligenciar Cantidad de adultos | El valor queda registrado (mínimo 1)
9. Diligenciar Cantidad de menores (3-9 años) | El valor queda registrado (0 o más)
10. Click en el botón Buscar | El sistema muestra la pantalla de disponibilidad con opciones de tickets
11. Validar que se muestran las opciones de tickets con precios en millas | Opciones visibles con precios correctos
12. Validar descripción de cada tipo de ticket (incluye, restricciones, validez) | Información completa visible
13. Click en el botón Canjear del ticket seleccionado | El sistema redirige al checkout con los datos del ticket seleccionado
14. Diligenciar todos los campos obligatorios del checkout (datos de cada visitante, contacto) | Los campos quedan completos correctamente
15. Validar cálculo de millas totales según cantidad y tipo de tickets | Cálculo correcto visible
16. Validar información importante sobre uso de tickets (políticas de Disney) | Información visible y clara
17. Marcar el check Tratamiento de datos | El check se marca correctamente
18. Marcar el check Términos y condiciones y validar funcionamiento de los links | Los enlaces abren correctamente en nueva pestaña o modal
19. Validar que el botón Canjear se habilite cuando todos los campos están completos | Botón Canjear habilitado
20. Click en el botón Canjear | Se procesa el canje (100% millas) y se muestra pantalla de confirmación
21. Validar pantalla de confirmación con código de reserva y detalles (tipo de ticket, parques, fechas, visitantes, millas canjeadas) | Código de reserva visible, datos completos y correctos
22. Validar que se muestra información sobre cómo retirar o activar los tickets | Instrucciones visibles y claras
23. Ingresar al Admin CME | Admin cargado correctamente
24. Buscar reserva por código | Reserva localizada
25. Validar que las millas canjeadas estén correctas en admin (coinciden con confirmación) | Millas correctas
26. Validar que la reserva queda emitida automáticamente (100% millas - proceso automático) | Reserva en estado EMITIDA
27. Validar respuesta correcta del proveedor DerbySoft | Confirmación recibida de DerbySoft
28. Validar voucher o comprobante de los tickets Disney | Voucher disponible para descarga o envío
29. Validar fecha de validez de los tickets | Fechas correctas en admin
30. Validar cantidad y tipo de tickets emitidos | Coincide con la compra realizada

---

## 🔄 VARIACIONES SEGÚN ESCENARIO

**Tipos de ticket:**
- 1 Parque por día (Park Ticket)
- Park Hopper (múltiples parques en un día)

**Parques:**
- Magic Kingdom
- Epcot
- Hollywood Studios
- Animal Kingdom

**Duración:**
- 1 día
- 2 días
- 3 días
- 4 días
- 5 o más días

**Visitantes:**
- Solo adultos
- Adultos + menores (3-9 años)
- Grupos grandes

**Fechas:**
- Temporada baja
- Temporada alta
- Fechas especiales (feriados)

---

## ✅ VALIDACIONES CRÍTICAS

✅ **Integridad de datos:** Consistencia entre búsqueda → disponibilidad → checkout → confirmación → admin  
✅ **Tipo de ticket:** Park Ticket o Park Hopper correctamente seleccionado  
✅ **Parques:** Parques seleccionados coinciden en todas las pantallas  
✅ **Cálculo de millas:** Millas totales = (millas por adulto × adultos) + (millas por menor × menores)  
✅ **Campos obligatorios:** Datos de todos los visitantes, contacto, aceptación de términos  
✅ **Links funcionales:** Términos y condiciones, tratamiento de datos abren correctamente  
✅ **Estados de reserva:** Confirmada en admin con todos los datos completos  
✅ **Fecha:** Validación de fecha de inicio, no permite fechas pasadas  
✅ **Validez:** Fecha de validez de los tickets correcta  
✅ **Proveedor:** DerbySoft (validar respuesta correcta)  
✅ **Voucher:** Disponible para descarga o envío con instrucciones de uso  
✅ **Pago:** 100% Millas (sin fee, sin tarjeta de crédito)

---

## 📝 FORMATO DE TÍTULO

```
[CME] Disney - [Tipo ticket] - [Días] - [Parques] - [Característica especial]
```

**Ejemplos:**
- `[CME] Disney - Park Ticket - 1 día - Magic Kingdom - 2 adultos`
- `[CME] Disney - Park Hopper - 3 días - 4 parques - 2 adultos + 2 menores`
- `[CME] Disney - Park Ticket - 5 días - Epcot - 1 adulto`

---

## 📸 IMÁGENES DE REFERENCIA

Incluir SIEMPRE estas imágenes en el campo Descriptions del Test Case:

- Home-disney-CME.png - Pantalla principal con opción Tickets Disney
- Disponibilidad-disney-CME.png - Opciones de tickets disponibles
- Checkout-disney-CME.png - Formulario de checkout completo con datos de todos los visitantes
- Confirmacion-disney-CME.png - Pantalla de confirmación con código de reserva e instrucciones
- Admin.png - Validación en módulo admin CME

---

## 📌 NOTAS IMPORTANTES

**Políticas de Disney:**
- Los tickets son válidos por un período específico desde la fecha de inicio
- Park Hopper permite visitar múltiples parques en un mismo día
- Los menores de 3 años no requieren ticket
- Los tickets pueden tener restricciones de fechas según temporada

**Proceso de activación:**
- Algunos tickets requieren activación en taquilla de Disney
- Otros pueden activarse mediante My Disney Experience app
- El voucher debe incluir instrucciones claras de activación

---

**Última actualización:** 2026-01-06  
**Versión:** 1.0.0  
**Mantenido por:** QA Team Ultragroup
