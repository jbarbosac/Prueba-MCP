# 🚗 FLUJO E2E OBLIGATORIO PARA AUTOS - CME

**Proveedor:** Correos Millas Ecuador  
**Portal:** https://correosmillas-ec.preprodppm.com/  
**Tecnología:** Meteor (JavaScript)  
**Modelo de pago:** 100% Millas (sin fee, sin tarjeta de crédito)  

---

## 📦 PROVEEDORES DISPONIBLES

**Proveedor:** Sabre  
**Empresas:** Hertz, Dollar, Thrifty

---

## 📋 PASOS OBLIGATORIOS DEL FLUJO E2E

**Siempre incluir estos pasos desde login para el flujo de Autos:**

1. Ingresar a la URL https://correosmillas-ec.preprodppm.com/ | Portal cargado correctamente, pantalla principal visible
2. Realizar login con un usuario válido | Login exitoso y acceso al home del portal
3. Click en la opción Autos | Se despliega el formulario de búsqueda de autos
4. Diligenciar el campo Ciudad de recogida (pickup) | Se habilita una lista de ciudades sugeridas
5. Seleccionar una ciudad de la lista | La ciudad queda registrada correctamente
6. Seleccionar Fecha y hora de recogida | Fecha y hora seleccionadas correctamente (no permite fechas pasadas)
7. Diligenciar el campo Ciudad de entrega (dropoff) | Se habilita una lista de ciudades sugeridas
8. Seleccionar ciudad de entrega (puede ser igual o diferente a pickup) | La ciudad queda registrada correctamente
9. Seleccionar Fecha y hora de entrega | Fecha y hora seleccionadas correctamente (posterior a fecha de recogida)
10. Validar que el sistema calcule automáticamente los días de renta | Días de renta calculados correctamente
11. Click en el botón Buscar | El sistema muestra la pantalla de disponibilidad con lista de autos disponibles
12. Validar que se muestran autos de Hertz, Dollar y/o Thrifty | Lista de autos visible con diferentes empresas
13. Click en el botón Ver auto o Canjear de un auto disponible | Se despliega el detalle del auto seleccionado
14. Validar características del auto (tipo, capacidad, transmisión, equipaje, aire acondicionado) | Información completa visible
15. Validar precio en millas | Millas totales visibles y correctas
16. Validar política de combustible y kilometraje | Políticas visibles y claras
17. Click en el botón Canjear | El sistema redirige al checkout con los datos del auto seleccionado
18. Diligenciar todos los campos obligatorios del checkout (datos del conductor principal, contacto) | Los campos quedan completos correctamente
19. Validar edad mínima del conductor (si aplica restricción) | Validación correcta de edad
20. Marcar el check Tratamiento de datos | El check se marca correctamente
21. Marcar el check Términos y condiciones y validar funcionamiento de los links | Los enlaces abren correctamente en nueva pestaña o modal
22. Validar que el botón Canjear se habilite cuando todos los campos están completos | Botón Canjear habilitado
23. Click en el botón Canjear | Se procesa el canje (100% millas) y se muestra pantalla de confirmación
24. Validar pantalla de confirmación con código de reserva y detalles (auto, fechas, ubicaciones, millas canjeadas) | Código de reserva visible, datos completos y correctos
25. Ingresar al Admin CME | Admin cargado correctamente
26. Buscar reserva por código | Reserva localizada
27. Validar que las millas canjeadas estén correctas en admin (coinciden con confirmación) | Millas correctas
28. Validar que la reserva queda emitida automáticamente (100% millas - proceso automático) | Reserva en estado EMITIDA
29. Validar respuesta correcta del proveedor Sabre | Confirmación recibida de Sabre
30. Validar empresa de renta correcta (Hertz, Dollar o Thrifty) | Empresa correcta en admin

---

## 🔄 VARIACIONES SEGÚN ESCENARIO

**Ubicaciones:**
- Pickup y dropoff en la misma ciudad
- Dropoff en ciudad diferente (cargo adicional)

**Duración:**
- 1 día
- Múltiples días (3, 5, 7, 14 días)

**Empresas:**
- Hertz
- Dollar
- Thrifty

**Tipo de auto:**
- Económico
- Compacto
- Intermedio
- SUV
- Lujo

**Horarios:**
- Horario laboral
- Fuera de horario laboral (puede tener cargo)

---

## ✅ VALIDACIONES CRÍTICAS

✅ **Integridad de datos:** Consistencia entre búsqueda → disponibilidad → detalle → checkout → confirmación → admin  
✅ **Cálculo de días:** Días de renta calculados correctamente según fechas y horas  
✅ **Cálculo de millas:** Millas totales = millas por día × días de renta + cargos adicionales (si aplica dropoff diferente)  
✅ **Campos obligatorios:** Datos del conductor principal, edad, contacto, aceptación de términos  
✅ **Links funcionales:** Términos y condiciones, tratamiento de datos abren correctamente  
✅ **Estados de reserva:** Confirmada en admin con todos los datos completos  
✅ **Fechas y horas:** Validación de fechas y horas, no permite fechas pasadas  
✅ **Ubicaciones:** Pickup y dropoff correctos en confirmación y admin  
✅ **Proveedor:** Sabre (validar respuesta correcta)  
✅ **Empresa:** Hertz, Dollar o Thrifty (validar empresa correcta)  
✅ **Pago:** 100% Millas (sin fee, sin tarjeta de crédito)

---

## 📝 FORMATO DE TÍTULO

```
[CME] Autos - [Días] - [Empresa] - [Característica especial]
```

**Ejemplos:**
- `[CME] Autos - 3 días - Hertz - Mismo pickup y dropoff`
- `[CME] Autos - 7 días - Dollar - Dropoff diferente - Quito a Guayaquil`
- `[CME] Autos - 5 días - Thrifty - Auto económico`

---

## 📸 IMÁGENES DE REFERENCIA

Incluir SIEMPRE estas imágenes en el campo Descriptions del Test Case:

- Home-autos-CME.png - Pantalla principal con opción Autos
- Disponibilidad-autos-CME.png - Lista de autos disponibles
- Checkout-autos-CME.png - Formulario de checkout completo
- Confirmacion-autos-CME.png - Pantalla de confirmación con código de reserva
- Admin.png - Validación en módulo admin CME

---

**Última actualización:** 2026-01-06  
**Versión:** 1.0.0  
**Mantenido por:** QA Team Ultragroup
