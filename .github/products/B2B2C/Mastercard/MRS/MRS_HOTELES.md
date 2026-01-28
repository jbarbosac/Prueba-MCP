# 🏨 FLUJO E2E OBLIGATORIO PARA HOTELES - MRS

**Sistema:** MRS (Mastercard Rewards System)  
**Clientes:** Austro (Ecuador), Ficohsa (multi-país), Coopenae (Costa Rica)  
**Portales:**  
- Austro: https://austec.smartlinks.dev/es-ec  
- Ficohsa Honduras: https://ficsahonduras.smartlinks.dev/es-hn  
- Ficohsa Guatemala: https://ficsaguatemala.smartlinks.dev/es-gt  
- Ficohsa Panamá: https://ficsapanama.smartlinks.dev/es-pa  
- Ficohsa Nicaragua: https://ficsanicaragua.smartlinks.dev/es-ni  
- Coopenae: https://cpn-mrs.smartlinks.dev/es-cr  
**Modelo de pago:** Millas (100%) o Millas + Plata (slider con mínimo 20% del total de millas)  

---

## 📦 PROVEEDORES DISPONIBLES

**Proveedor:** Hotel Sabre (único)

---

## 📋 PASOS OBLIGATORIOS DEL FLUJO E2E

**IMPORTANTE - LÓGICA DE EMISIÓN Y CANCELACIÓN:**
- **Solo Millas (100%):** Emisión AUTOMÁTICA tras la compra
- **Millas + Plata:** Emisión AUTOMÁTICA tras la compra
- **Cancelación:** Cancelar en admin MRS → validar devolución de millas según políticas → reverso de cobro si aplica

**Siempre incluir estos pasos desde login para el flujo de Alojamiento:**

1. Ingresar al portal MRS correspondiente al cliente (Austro/Ficohsa/Coopenae) | El portal carga correctamente y muestra la pantalla de inicio
2. Realizar login con usuario y contraseña válidos | Login exitoso y acceso al home
3. Click en la opción "Viajes" | Se despliegan los diferentes productos del modelo
4. Click en la opción "Alojamiento" | Se habilita el formulario de búsqueda de alojamiento
5. Diligenciar ciudad de alojamiento | Ciudad registrada correctamente
6. Seleccionar fecha "Desde" | Fecha de entrada registrada
7. Seleccionar fecha "Hasta" | Fecha de salida registrada
8. Diligenciar cantidad de habitaciones | Cantidad de habitaciones registrada
9. Diligenciar número de adultos | Cantidad de adultos registrada
10. Diligenciar número de menores | Cantidad de menores registrada
11. Validar que después de diligenciar los campos obligatorios se habilite el botón "Buscar alojamiento" | El botón "Buscar alojamiento" se habilita
12. Click en el botón "Buscar alojamiento" | Se muestra la pantalla de disponibilidad con lista de hoteles
13. Validar que se muestre la lista de hoteles disponibles | Información de hoteles mostrada correctamente
14. Click en el botón "Ver hotel" | Se despliega el detalle del hotel seleccionado
15. Validar la fecha hasta que se puede cancelar (que no entre en gastos de cancelación) | La fecha límite de cancelación sin gastos se muestra correctamente
16. Validar detalle del hotel (nombre, ubicación, servicios, políticas de cancelación, millas y/o plata) | Información completa visible
17. Mover el slider para seleccionar modo de pago (Solo Millas o Millas + Plata con mínimo 20% del total de millas) | El sistema muestra el valor según la selección del slider
18. Click en el botón "Canjear" | Se navega al checkout
19. Diligenciar todos los campos obligatorios del checkout | Los campos quedan completos correctamente
20. Marcar el check de Tratamiento de datos | Check seleccionado
21. Marcar el check de Términos y condiciones | Check seleccionado
22. Validar que los enlaces de Tratamiento de datos y Términos y condiciones funcionen correctamente | Los links abren correctamente en nueva pestaña
23. Validar que el botón "Canjear" se habilite únicamente cuando todos los campos obligatorios estén completos | El botón "Canjear" se habilita
24. Click en el botón "Canjear" | Se procesa la reserva y se genera la pantalla de confirmación
25. Validar que la pantalla de confirmación muestre correctamente el código de reserva y el pago realizado (millas o millas + plata) | Valores y código de reserva correctos
26. Ingresar al Admin MRS del cliente correspondiente | Admin cargado correctamente
27. Buscar reserva por código | Reserva localizada
28. Validar que los valores de millas y/o plata coincidan con la reserva generada | Los valores coinciden con checkout y confirmación
29. Validar que la reserva quedó emitida automáticamente en estado EMITIDA (tanto Solo Millas como Millas + Plata) | Reserva emitida automáticamente

---

## 🔄 VARIACIONES SEGÚN ESCENARIO

**Habitaciones:**
- 1 a N habitaciones

**Huéspedes:**
- 1 a N por habitación (adultos + menores con edades)

**Noches:**
- 1 a N noches de estadía

**Modelo de pago:**
- Solo Millas (100% - emisión automática)
- Millas + Plata (mixto - emisión automática)

**Proveedor:**
- Hotel Sabre (único proveedor de alojamiento)

---

## ✅ VALIDACIONES CRÍTICAS

✅ **Navegación:** Viajes → Alojamiento → Formulario de búsqueda  
✅ **Campos obligatorios:** Ciudad, fechas (Desde/Hasta), habitaciones, adultos, menores  
✅ **Botón "Buscar alojamiento":** Debe habilitarse SOLO cuando todos los campos obligatorios estén completos  
✅ **Lista de hoteles:** Validar información completa (nombre, ubicación, servicios, tarifas)  
✅ **Detalle del hotel:** Validar políticas de cancelación (fecha límite sin gastos de cancelación)  
✅ **Slider funcional:** Mover entre Solo Millas (100%) y Millas + Plata (validar mínimo 20% del total de millas para alojamiento)  
✅ **Checkout:** Campos obligatorios completos, tarjeta solo si es Millas + Plata  
✅ **Cálculo visible en checkout:** Débito de millas seleccionadas en slider visible en resumen  
✅ **Links funcionales:** Términos y condiciones, tratamiento de datos abren correctamente  
✅ **Confirmación:** Código de reserva, monto millas y plata (si aplica)  
✅ **Admin - Solo Millas:** Emisión automática inmediata  
✅ **Admin - Millas + Plata:** Emisión automática inmediata  
✅ **Cancelación:** Según políticas del producto → validar devolución de millas y reverso de cobro  
✅ **Proveedor:** Hotel Sabre (único proveedor de alojamiento en MRS)  
✅ **Integridad de datos:** Consistencia entre búsqueda → disponibilidad → detalle → checkout → confirmación → admin MRS  
✅ **Cálculo de millas:** Millas totales = (millas por noche × número de noches) × habitaciones  
✅ **Cálculo de plata (cuando aplica):** Plata total = (plata por noche × número de noches) × habitaciones  
✅ **Fechas:** Check-in (Desde) y check-out (Hasta) correctos, noches calculadas correctamente  
✅ **NO validar fees:** En MRS no se calculan ni validan fees de procesamiento  
✅ **Cliente:** Validar acceso al admin MRS correspondiente (Austro, Ficohsa o Coopenae)  
✅ **Estado EMITIDA:** Validar que ambos modelos de pago queden EMITIDA automáticamente  

---

## 📝 FORMATO DE TÍTULO

```
[MRS] Hoteles - [Noches] - [Modelo de pago] - [Cliente]
```

**Ejemplos:**
- `[MRS] Hoteles - 3 noches - Hotel Sabre - Solo Millas automático - Austro`
- `[MRS] Hoteles - 5 noches - Hotel Sabre - Millas + Plata manual - Ficohsa Honduras`
- `[MRS] Hoteles - 2 noches - Hotel Sabre - Cancelación con devolución - Coopenae`
