# 🛫 FLUJO E2E OBLIGATORIO PARA VUELOS - BGR

**Proveedor:** BGR Miles Ecuador  
**Portal:** https://bgrmiles-ec.preprodppm.com/  
**Modelo de pago:** Millas (100%) o Millas + Plata (slider con mínimo 2875 millas)  

---

## 📦 PROVEEDORES DISPONIBLES

- **AGGREGATOR - NETACTICA** (sin dispersión de fondos)
- **AGGREGATOR - SABRE** (sin dispersión de fondos)
- **SABRE EDIFACT** (con dispersión de fondos)

---

## 📋 PASOS OBLIGATORIOS DEL FLUJO E2E

**Siempre incluir estos pasos desde login:**

1. Ingresar a la URL https://bgrmiles-ec.preprodppm.com/ | Portal cargado correctamente
2. Ingresar usuario y contraseña válidos | Login exitoso
3. Click en la opción Viajes | Se despliegan los diferentes productos del modelo
4. Click en la opción Vuelos | Se muestra el formulario de búsqueda de vuelos
5. Seleccionar tipo de vuelo (solo ida/ida y vuelta/multidestino) | El sistema habilita los campos correspondientes
6. Seleccionar clase (Todas, Primera clase, Negocios, Económica, Económica Premium, Primera Premium, Ejecutiva Premium) | La selección queda reflejada
7. Seleccionar origen de la lista desplegable | La ciudad de origen se selecciona correctamente
8. Seleccionar destino de la lista desplegable | La ciudad de destino se selecciona correctamente
9. Seleccionar fecha Desde | La fecha de salida queda registrada
10. Seleccionar fecha Hasta (si aplica para ida y vuelta) | La fecha de retorno queda registrada
11. Seleccionar aerolínea (específica o Todas) | La selección queda registrada
12. Indicar cantidad de adultos, menores y bebés | Los valores se actualizan correctamente
13. Validar que el botón Buscar Vuelos se habilite cuando los campos obligatorios están diligenciados | El botón Buscar Vuelos se habilita
14. Click en el botón Buscar Vuelos | Se muestra la pantalla de disponibilidad con vuelos
15. Mover el slider para seleccionar modo de pago (Solo Millas o Millas + Plata con mínimo 2875 millas) | El sistema muestra el valor según la selección del slider
16. Click en el botón Comprar del vuelo seleccionado | Se muestra el pop-up de upsell con tarifas disponibles
17. Seleccionar una tarifa en el upsell y hacer click en Continuar | Se muestra la pantalla de resumen
18. Validar información del vuelo en resumen y hacer click en Continuar | Se muestra la pantalla de checkout
19. Diligenciar todos los campos obligatorios del checkout | Los campos quedan completos correctamente
20. Si es Millas + Plata: Ingresar tarjeta para pagar el componente en dinero | El sistema valida y registra la tarjeta
21. Si es Solo Millas: NO ingresar tarjeta | El método de pago queda solo con millas
22. Marcar el check de Tratamiento de datos | Check seleccionado
23. Marcar el check de Términos y condiciones | Check seleccionado
24. Validar que el botón Comprar se habilite cuando todos los campos obligatorios estén completos | El botón Comprar se habilita
25. Click en el botón Comprar | Se muestra la pantalla de confirmación
26. Validar que la pantalla de confirmación muestre el pago realizado correctamente (millas o millas + cash) | El pago es exitoso y se muestra el código de reserva
27. Validar en el Admin que los montos de millas y cash coincidan con la compra | Los valores coinciden con checkout y confirmación
28. Si fue Solo Millas: Validar en el Admin que la reserva quedó emitida automáticamente | La reserva aparece como emitida
29. Si fue Millas + Plata: En el Admin abrir la reserva, debitar millas y luego pagar cash | La reserva queda emitida tras el proceso manual

---

## 🔄 VARIACIONES SEGÚN ESCENARIO

**Tipo de vuelo:**
- Solo Ida
- Ida y vuelta
- Multidestino

**Proveedores:**
- AGGREGATOR - NETACTICA (sin dispersión)
- AGGREGATOR - SABRE (sin dispersión)
- SABRE EDIFACT (validar dispersión en paso 29)

**Clases:**
- Todas
- Primera clase
- Negocios
- Económica
- Económica Premium
- Primera Premium
- Ejecutiva Premium

**Pasajeros:**
- 1 adulto
- Múltiples adultos
- Adultos + menores
- Adultos + bebés

**Modelo de pago:**
- Solo Millas (100% - emisión automática)
- Millas + Plata (slider con mínimo 2875 millas - emisión manual)

---

## ✅ VALIDACIONES CRÍTICAS

✅ **Navegación:** Viajes → Vuelos → Formulario de búsqueda  
✅ **Campos obligatorios:** Tipo vuelo, clase, origen, destino, fechas, pasajeros  
✅ **Slider funcional:** Mover entre Solo Millas y Millas + Plata (validar mínimo 2875 millas)  
✅ **Slider bloqueado:** NO permitir bajar de 2875 millas  
✅ **Upsell:** Mostrar tarifas con diferentes beneficios y permitir selección  
✅ **Resumen:** Validar información completa antes de checkout  
✅ **Checkout:** Campos obligatorios completos, tarjeta solo si es Millas + Plata  
✅ **Cálculo visible en checkout:** Débito de millas seleccionadas en slider visible en resumen  
✅ **Confirmación:** Código de reserva, monto millas y cash (si aplica)  
✅ **Admin - Solo Millas:** Emisión automática inmediata  
✅ **Admin - Millas + Plata:** Proceso manual (ingresar admin → buscar reserva → debitar millas → pagar cash → emisión)  
✅ **Proveedor:** Identificar y validar si es AGGREGATOR - NETACTICA, AGGREGATOR - SABRE o SABRE EDIFACT  
✅ **NO validar fees:** En BGR no se calculan ni validan fees de procesamiento  
✅ **Integridad de datos:** Consistencia entre búsqueda → disponibilidad → upsell → resumen → checkout → confirmación → admin  

---

## 📝 FORMATO DE TÍTULO

```
[BGR] Vuelos - [Tipo de viaje] - [Proveedor] - [Modelo de pago] - [Variante adicional]
```

**Ejemplos:**
- `[BGR] Vuelos - Ida y vuelta - SABRE EDIFACT - Solo Millas automático - 1 adulto`
- `[BGR] Vuelos - Solo ida - AGGREGATOR NETACTICA - Millas + Plata manual - 2 adultos`
- `[BGR] Vuelos - Multidestino - AGGREGATOR SABRE - Solo Millas automático - 1 adulto + 1 menor`
