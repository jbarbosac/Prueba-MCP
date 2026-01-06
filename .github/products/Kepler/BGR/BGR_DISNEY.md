# 🎠 FLUJO E2E OBLIGATORIO PARA TICKETS DISNEY - BGR

**Proveedor:** BGR Miles Ecuador  
**Portal:** https://bgrmiles-ec.preprodppm.com/?operation=uv  
**Modelo de pago:** Millas (100%) o Millas + Plata (slider con mínimo 20% del total de millas)  

---

## 📦 PROVEEDORES DISPONIBLES

**Proveedor:** OffLine (único)

---

## 🎢 TIPOS DE TICKETS DISPONIBLES

- Park Hopper
- Park Hopper Plus
- Magic Kingdom
- Epcot
- Hollywood Studios
- Animal Kingdom
- Parques acuáticos
- Experiencia ESPN Sport

---

## 📋 PASOS OBLIGATORIOS DEL FLUJO E2E

**Siempre incluir estos pasos desde login para el flujo de Tickets Disney:**

1. Ingresar al portal https://bgrmiles-ec.preprodppm.com/?operation=uv | El portal carga correctamente y muestra la pantalla de inicio
2. Realizar login con usuario y contraseña válidos | Login exitoso y acceso al home
3. Click en la opción Viajes | Se despliegan los productos del marketplace
4. Click en la opción Tickets Disney | Formulario de búsqueda para Tickets Disney visible
5. Seleccionar Fecha de entrada | Fecha registrada correctamente
6. Seleccionar Número de pasajeros | Valores registrados correctamente
7. Click en el botón Buscar | Se muestra la pantalla de disponibilidad con diferentes tipos de entradas
8. Validar listado de opciones disponibles (Park Hopper, Park Hopper Plus, Magic Kingdom, Epcot, Hollywood Studios, Animal Kingdom, Parques acuáticos, ESPN Sports, etc.) | Todas las opciones disponibles se muestran correctamente según el día seleccionado
9. Validar que se muestren opciones de pago: Millas y/o Millas + Plata | Opciones de pago visibles según disponibilidad
10. Mover el slider para seleccionar modo de pago (Solo Millas o Millas + Plata con mínimo 20% del total de millas) | El sistema muestra el valor según la selección del slider
11. Click en el botón Seleccionar de una de las entradas | Se despliegan las opciones de precio asociadas al ticket
12. Validar que se muestren precios en millas y/o plata según el tipo de ticket | Información consistente según producto seleccionado
13. Click en el botón Seleccionar de la opción escogida | El sistema redirige al checkout
14. Diligenciar todos los campos obligatorios en checkout (datos de pasajeros, contacto) | Campos completados correctamente
15. Si es Millas + Plata: Ingresar tarjeta para pagar el componente en dinero | El sistema valida y registra la tarjeta
16. Si es Solo Millas: NO ingresar tarjeta | El método de pago queda solo con millas
17. Marcar el check Tratamiento de datos | Check seleccionado
18. Marcar el check Términos y condiciones | Check seleccionado
19. Validar que los enlaces de Tratamiento de datos y Términos y condiciones funcionan | Los links abren correctamente en nueva pestaña
20. Validar que el botón Canjear se habilite únicamente cuando todos los campos obligatorios estén completos | Botón habilitado
21. Click en el botón Canjear | Se procesa la compra y se genera la confirmación
22. Validar que la pantalla de confirmación muestre el código de ticket | Código de ticket visible
23. Validar que la confirmación muestre el pago realizado correctamente (millas o millas + plata) | Valores y detalles correctos
24. Validar en el admin que los valores de millas y/o plata coincidan con la reserva generada | Valores coinciden con checkout y confirmación
25. Si fue Solo Millas: Validar en el Admin que la reserva quedó emitida automáticamente | La reserva aparece como emitida
26. Si fue Millas + Plata: En el Admin buscar la reserva, abrirla, debitar millas manualmente y luego pagar en cash | La reserva queda emitida tras el proceso manual

---

## 🔄 VARIACIONES SEGÚN ESCENARIO

**Proveedor:**
- OffLine (único)

**Tipos de tickets:**
- Park Hopper
- Park Hopper Plus
- Magic Kingdom
- Epcot
- Hollywood Studios
- Animal Kingdom

**Opciones adicionales:**
- Parques acuáticos
- Experiencia ESPN Sport

**Beneficios:**
- Visita más de 1 parque el mismo día (Park Hopper/Plus)

**Participantes:**
- 1 a N pasajeros (adultos, niños según edad)

**Fechas:**
- Diferentes fechas de entrada validando disponibilidad

**Modelo de pago:**
- Solo Millas (100% - emisión automática)
- Millas + Plata (mixto - emisión manual)

---

## ✅ VALIDACIONES CRÍTICAS

✅ **Navegación:** Viajes → Tickets Disney → Formulario de búsqueda  
✅ **Integridad de datos:** Consistencia entre búsqueda → disponibilidad → selección de ticket → checkout → confirmación → admin  
✅ **Modelos de pago:** Validar correctamente opciones de Solo Millas (100%) y Millas + Plata cuando estén disponibles  
✅ **Slider funcional:** Mover entre Solo Millas (100%) y Millas + Plata (validar mínimo 20% del total de millas para tickets Disney)  
✅ **Tipos de tickets:** Validación correcta de Park Hopper, Park Hopper Plus, entradas individuales por parque  
✅ **Opciones incluidas:** Verificar que se muestren correctamente las opciones (parques acuáticos, ESPN Sports, multi-parque)  
✅ **Cálculo de millas:** Millas totales = millas por ticket × cantidad de pasajeros  
✅ **Cálculo de plata (cuando aplica):** Plata total = plata por ticket × cantidad de pasajeros  
✅ **Cálculo visible en checkout:** Débito de millas seleccionadas en slider visible en resumen  
✅ **Checkout:** Campos obligatorios completos (datos pasajeros, contacto), tarjeta solo si es Millas + Plata  
✅ **Campos obligatorios:** Datos de pasajeros completos, contacto, aceptación de términos  
✅ **Links funcionales:** Términos y condiciones, tratamiento de datos abren correctamente  
✅ **Confirmación:** Código de ticket, monto millas y plata (si aplica)  
✅ **Admin - Solo Millas:** Emisión automática inmediata (estado EMITIDA desde el inicio)  
✅ **Admin - Millas + Plata:** Proceso manual (ingresar admin → buscar reserva → abrir → debitar millas manualmente → pagar en cash → emisión)  
✅ **Estados de reserva:** Solo Millas = Emisión automática; Millas + Plata = Proceso manual (debitar millas → pagar cash → emisión)  
✅ **Fechas:** Validación de fecha de entrada, disponibilidad para fecha seleccionada  
✅ **Cantidad pasajeros:** Validación correcta del número de entradas según pasajeros ingresados  
✅ **NO validar fees:** En BGR no se calculan ni validan fees de procesamiento  

---

## 📝 FORMATO DE TÍTULO

```
[BGR] Disney - [Tipo de ticket] - [Modelo de pago] - [Variante adicional]
```

**Ejemplos:**
- `[BGR] Disney - Park Hopper - Solo Millas automático - 2 adultos`
- `[BGR] Disney - Park Hopper Plus - Millas + Plata manual - 1 adulto + 2 niños`
- `[BGR] Disney - Magic Kingdom - Solo Millas automático - 4 personas`
