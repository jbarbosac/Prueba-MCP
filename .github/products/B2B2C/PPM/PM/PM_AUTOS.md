# 🚗 FLUJO E2E OBLIGATORIO PARA RENTA DE AUTOS - PICHINCHA MILES

**Proveedor:** Pichincha Miles Ecuador  
**Portal:** https://pichinchamiles-ec.preprodppm.com/  
**Tecnología:** Meteor (JavaScript/Node.js)  
**Modelo de pago:** 100% Millas (sin fee, sin tarjeta de crédito)  
**Promocode:** ❌ NO APLICA (Autos es el único producto PM sin Promocode)  
**Markup:** ❌ NO APLICA (solo Hoteles y Actividades tienen Markup)  
**Drop off:** ✅ SÍ APLICA (cargo adicional cuando recogida ≠ devolución)  

---

## 📍 DROP OFF (CARGO POR DEVOLUCIÓN EN PUNTO DIFERENTE)

### ¿QUÉ ES EL DROP OFF?

**Drop off** es un **impuesto/cargo adicional** que se cobra cuando el vehículo se recoge en un punto y se entrega en un punto diferente.

### CARACTERÍSTICAS DEL DROP OFF:

✅ **Se cobra en millas adicionales:** Sumado al costo base de la renta  
✅ **Solo cuando puntos son diferentes:** Recogida ≠ Devolución  
✅ **Pago en punto de entrega:** El Drop off se paga en el punto de devolución del vehículo  
✅ **Visible en disponibilidad:** Incluido en el precio total mostrado  
✅ **Visible en checkout:** Desglosado como cargo adicional  
✅ **Incluido en confirmación:** Parte del total de millas canjeadas  
❌ **No aplica mismo destino:** Si recogida = devolución, NO hay Drop off  

### FLUJOS POSIBLES:

**1️⃣ Mismo destino (SIN Drop off):**
- Recogida: Aeropuerto Madrid
- Devolución: Aeropuerto Madrid
- **Drop off:** ❌ NO APLICA
- **Millas:** Solo costo base de la renta

**2️⃣ Destino diferente (CON Drop off):**
- Recogida: Aeropuerto Madrid
- Devolución: Aeropuerto Barcelona
- **Drop off:** ✅ SÍ APLICA
- **Millas:** Costo base + Drop off

### EJEMPLO DE CÁLCULO:

**Renta con Drop off:**
```
Costo base 5 días: 25,000 millas
Cargo Drop off (Madrid → Barcelona): 8,000 millas
Total a pagar: 33,000 millas
```

**Renta sin Drop off:**
```
Costo base 5 días: 25,000 millas
Cargo Drop off: 0 millas (mismo destino)
Total a pagar: 25,000 millas
```

### VALIDACIONES CRÍTICAS DROP OFF:

✅ **Check activado:** Validar campo "Devolución en otro destino" funcional  
✅ **Destino diferente:** Permitir ingresar ubicación diferente de devolución  
✅ **Cargo visible:** Drop off debe aparecer en disponibilidad  
✅ **Desglose en checkout:** Mostrar Drop off como línea separada  
✅ **Cálculo correcto:** Total = Base + Drop off  
✅ **Pago en entrega:** Confirmar que el Drop off se paga en el punto de devolución  
✅ **Consistencia:** Drop off igual en todas las pantallas (disponibilidad, checkout, confirmación, admin)  
✅ **Sin Drop off si mismo destino:** NO cobrar cuando recogida = devolución  

---

## 📦 PROVEEDORES Y EMPRESAS DE SERVICIO

**Proveedor:** Sabre (único)

**Empresas de servicio disponibles:**
- Hertz
- Dollar
- Thrifty

---

## 📋 PASOS OBLIGATORIOS DEL FLUJO E2E

**Siempre incluir estos pasos desde login para el flujo de Renta de Autos:**

1. Ingresar a la URL https://pichinchamiles-ec.preprodppm.com/ | Portal cargado correctamente, pantalla principal visible
2. Realizar login con un usuario válido | Login exitoso y acceso al home del portal
3. Click en la opción Renta de Autos | Se despliega la sección de Renta de Autos con el formulario de búsqueda
4. Diligenciar el campo Lugar de recogida | El campo acepta el dato y muestra sugerencias válidas de ubicaciones
5. Seleccionar Fecha de recogida | Fecha seleccionada correctamente (no permite fechas pasadas)
6. Seleccionar Fecha de devolución | Fecha seleccionada correctamente (posterior a fecha de recogida)
7. Seleccionar Hora de recogida | Hora registrada correctamente en formato válido
8. Seleccionar Hora de devolución | Hora registrada correctamente en formato válido
9. [OPCIONAL - Flujo alternativo] Activar check Devolución en otro destino y diligenciar nuevo destino | Campo de devolución se habilita y permite ingresar destino diferente
10. Click en el botón Buscar | Sistema muestra pantalla de disponibilidad con ofertas de autos
11. Seleccionar una oferta disponible haciendo click | Sistema redirige al checkout con los datos del auto seleccionado
12. [Si es devolución en otro destino] Validar que el cargo adicional por Dropoff esté incluido en el total | Cargo por Dropoff visible y sumado correctamente
13. Diligenciar todos los campos obligatorios del checkout (datos personales, número de licencia de conducir, contacto) | Datos se guardan correctamente
14. Marcar check de Tratamiento de datos | Check seleccionado
15. Marcar check de Términos y condiciones | Check seleccionado
16. Validar que el botón Canjear se habilita al completar todos los campos obligatorios | Botón Canjear habilitado
17. Click en botón Canjear | Se procesa el canje (100% millas) y se muestra pantalla de confirmación
18. Validar pantalla de Confirmación con código de reserva y millas canjeadas (+ Dropoff si aplica) | Valores mostrados coinciden con checkout
19. Ingresar al Admin Pichincha Miles | Admin cargado correctamente
20. Buscar reserva por código | Reserva localizada
21. Validar que las millas canjeadas estén correctas en admin (coinciden con confirmación) | Millas correctas
22. Validar que la reserva queda emitida automáticamente (100% millas - proceso automático) | Reserva en estado EMITIDA
23. Validar en Sabre que el canje es correcto | Transacción registrada correctamente en Sabre

---

## 🔄 VARIACIONES SEGÚN ESCENARIO

**Mismo destino vs Otro destino:**
- **Mismo destino:** Omitir paso 9 (NO activar check "Devolución en otro destino"), omitir paso 12 (NO hay cargo Dropoff)
- **Otro destino:** INCLUIR paso 9 (Activar check y diligenciar destino diferente) + INCLUIR paso 12 (Validar cargo adicional por Dropoff)

**Proveedor:**
- Sabre (único)

**Empresas de servicio:**
- Hertz
- Dollar
- Thrifty (especificar en título del caso)

**Regiones:**
- Europa (España, Francia, Reino Unido, Italia, Alemania, Portugal, Países Bajos)
- Norteamérica (USA, Canadá)

**Duración:**
- 1 día
- 3 días
- 5 días
- 7+ días

---

## ✅ VALIDACIONES CRÍTICAS

✅ **Integridad de datos:** Consistencia entre checkout → confirmación → admin → Sabre  
✅ **Cálculo de millas:** Millas canjeadas + Dropoff (si aplica) = total correcto  
✅ **Cargo Dropoff:** Solo cuando lugar recogida ≠ lugar devolución (incluido en millas totales)  
✅ **Estados de reserva:** Confirmada en todos los sistemas  
✅ **Fechas y horas:** Validación de rangos y formatos  
✅ **Proveedor:** Sabre (validar transacción correcta)  
✅ **Empresa de servicio:** Hertz, Dollar o Thrifty según corresponda  
✅ **Pago:** 100% Millas (sin fee, sin tarjeta de crédito)

---

## 📝 FORMATO DE TÍTULO

```
[PM] Autos - [Duración] - [Empresa] - [Característica especial]
```

**Ejemplos:**
- `[PM] Autos - 5 días - Hertz - Dropoff diferente (Madrid → Barcelona)`
- `[PM] Autos - 3 días - Dollar - Mismo destino (Miami)`
- `[PM] Autos - 7 días - Thrifty - Europa - Dropoff Londres → París`
