# 🎢 FLUJO E2E OBLIGATORIO PARA ACTIVIDADES - BGR

**Proveedor:** BGR Miles Ecuador  
**Portal:** https://bgrmiles-ec.preprodppm.com/  
**Modelo de pago:** Millas (100%) o Millas + Plata (slider con mínimo 20% del total de millas)  

---

## 📦 PROVEEDORES DISPONIBLES

**Proveedor:** HotelBeds (único)

---

## 📋 PASOS OBLIGATORIOS DEL FLUJO E2E

**IMPORTANTE - LÓGICA DE EMISIÓN Y CANCELACIÓN:**
- **Solo Millas (100%):** Emisión AUTOMÁTICA tras la compra
- **Millas + Plata (Emitir):** Proceso MANUAL → ingresar admin → buscar reserva → abrir → debitar millas → emitir en cash → emisión
- **Millas + Plata (Cancelar SIN emitir):** Cancelar en admin → validar devolución de millas al cliente (NO se debitan millas, NO se emite)

**Siempre incluir estos pasos desde login para el flujo de Actividades:**

1. Ingresar al portal https://bgrmiles-ec.preprodppm.com/ | El portal carga correctamente y muestra la pantalla de inicio
2. Realizar login con usuario y contraseña válidos | Login exitoso y acceso al home
3. Click en la opción "Viajes" | Se despliegan los diferentes productos de la agencia (vuelos, hoteles, autos, actividades, disney)
4. Click en la opción "Actividades" | Se muestra el formulario de búsqueda de actividades
5. Diligenciar ciudad destino en el campo de búsqueda | Se despliega una lista de ciudades para seleccionar
6. Seleccionar ciudad desde la lista desplegable | La ciudad queda registrada correctamente
7. Seleccionar fecha "Desde" | Fecha de salida registrada correctamente
8. Seleccionar cantidad de pasajeros | Valor registrado correctamente
9. Seleccionar edad de los pasajeros | Edades registradas correctamente según cantidad seleccionada
10. Validar que después de diligenciar los campos obligatorios se habilite el botón "Buscar actividad" | El botón "Buscar actividad" se habilita
11. Click en el botón "Buscar actividad" | Se envía a la pantalla de disponibilidad con actividades
12. Validar que se listen diferentes actividades disponibles | Se muestran múltiples opciones de actividades
13. Click en el botón "Ver detalle" de una actividad | Se muestra el detalle completo con valor, cantidad de personas, descripción, duración, incluye/no incluye
14. Validar información completa en el detalle (nombre, descripción, duración, incluye, no incluye, condiciones) | Información completa visible
15. Validar disponibilidad para la fecha seleccionada | Disponibilidad confirmada
16. Click en el botón "Canjear" | Se navega al checkout
17. Diligenciar todos los campos obligatorios del checkout (datos de contacto, participantes) | Campos completados correctamente
18. Marcar el check de Tratamiento de datos | Check seleccionado
19. Marcar el check de Términos y condiciones | Check seleccionado
20. Validar que los enlaces de Tratamiento de datos y Términos y condiciones funcionen correctamente | Los links abren correctamente en nueva pestaña
21. Validar que el botón "Canjear" se habilite únicamente cuando todos los campos obligatorios estén completos | El botón "Canjear" se habilita
22. Click en el botón "Canjear" | Se procesa la reserva y se genera la confirmación
23. Validar que la pantalla de confirmación muestre correctamente el código de reserva | Código de reserva visible
24. Validar que el pago se realizó correctamente de acuerdo al producto seleccionado (millas y/o plata) | Valores correctos según modelo de pago
25. Ingresar al admin de BGR y buscar la reserva | Reserva localizada correctamente
26. Validar que el valor pagado (millas y/o plata) coincida con la reserva generada | Los valores coinciden con checkout y confirmación
27. Si fue Solo Millas: Validar en el Admin que la reserva quedó emitida automáticamente | La reserva aparece como emitida
28. Si fue Millas + Plata (emisión): En el Admin buscar la reserva, abrirla, debitar millas y luego emitir en cash | La reserva queda emitida tras el proceso manual
29. Si fue Millas + Plata (cancelación SIN emitir): En el Admin buscar la reserva, cancelarla (NO debitar millas, NO emitir), validar devolución de millas al cliente | Las millas se devuelven automáticamente y NO se genera cobro en cash

---

## 🔄 VARIACIONES SEGÚN ESCENARIO

**Proveedor:**
- HotelBeds (único)

**Tipo de actividad:**
- Tours, Experiencias, Parques, Museos, Deportes, etc.

**Participantes:**
- 1 a N personas (adultos, niños, seniors con edades específicas)

**Duración:**
- Medio día, Día completo, Varios días

**Incluye:**
- Transporte, Comida, Guía, Entradas, Equipo

**Destino:**
- Nacional, Internacional

**Modelo de pago:**
- Solo Millas (100% - emisión automática)
- Millas + Plata (mixto - emisión manual o cancelación con devolución)

---

## ✅ VALIDACIONES CRÍTICAS

✅ **Navegación:** Viajes → Actividades → Formulario de búsqueda  
✅ **Campos obligatorios:** Ciudad destino, fecha desde, cantidad de pasajeros, edad de pasajeros  
✅ **Botón "Buscar actividad":** Debe habilitarse SOLO cuando todos los campos obligatorios estén completos  
✅ **Lista de actividades:** Validar que se muestren múltiples opciones disponibles  
✅ **Detalle de actividad:** Nombre, descripción completa, duración, qué incluye/no incluye, condiciones, valor en millas y/o plata  
✅ **Disponibilidad:** Validar que la actividad esté disponible para la fecha seleccionada  
✅ **Slider funcional:** Mover entre Solo Millas (100%) y Millas + Plata (validar mínimo 20% del total de millas para actividades)  
✅ **Checkout:** Campos obligatorios completos (datos contacto, participantes), tarjeta solo si es Millas + Plata  
✅ **Cálculo de millas:** Millas totales = millas base por persona × cantidad de personas  
✅ **Cálculo de plata (cuando aplica):** Plata total = plata base por persona × cantidad de personas  
✅ **Cálculo visible en checkout:** Débito de millas seleccionadas en slider visible en resumen  
✅ **Links funcionales:** Términos y condiciones, tratamiento de datos abren correctamente en nueva pestaña  
✅ **Confirmación:** Código de reserva, monto millas y plata (si aplica) correctos  
✅ **Admin - Solo Millas:** Emisión automática inmediata (estado EMITIDA desde el inicio)  
✅ **Admin - Millas + Plata (emisión):** Proceso manual (ingresar admin → buscar reserva → abrir → debitar millas → emitir en cash → emisión)  
✅ **Admin - Millas + Plata (cancelación SIN emitir):** Cancelar reserva → validar devolución de millas → NO cobro en cash  
✅ **Integridad de datos:** Consistencia entre búsqueda → disponibilidad → detalle → checkout → confirmación → admin  
✅ **Fechas:** Fecha de salida correcta, disponibilidad de la actividad validada  
✅ **Edad:** Restricciones de edad validadas correctamente según tipo de actividad  
✅ **Proveedor:** HotelBeds (único proveedor de actividades en BGR)  
✅ **NO validar fees:** En BGR no se calculan ni validan fees de procesamiento  

---

## 📝 FORMATO DE TÍTULO

```
[BGR] Actividades - [Ciudad] - [Tipo de actividad] - [Modelo de pago] - [Característica especial]
```

**Ejemplos:**
- `[BGR] Actividades - Quito - City Tour - Solo Millas automático - 2 personas`
- `[BGR] Actividades - Cancún - Actividad acuática - Millas + Plata manual - Validación edad`
- `[BGR] Actividades - Lima - Entrada a parque - Cancelación con devolución - 5 personas`
