# � FLUJO E2E OBLIGATORIO PARA VUELOS - CME

**Proveedor:** Club Miles Ecuador  
**Portal Test:** https://clubmiles-ec.developppm.com/  
**Portal Demo:** https://clubmiles-ec.preprodppm.com/  
**Tecnología:** Angular (TypeScript/JavaScript)  
**Métodos de pago:** Solo Millas (100%) o Millas+Plata (Copago con Slider en CheckOut, mínimo 20%)  
**Fee de procesamiento:** TARJETA DE CRÉDITO (obligatorio, formulario en CheckOut)  
**Pasarela:** PlacetoPay (bash, sin interfaz visual)

---

## 📦 PROVEEDORES DISPONIBLES

- **Sabre Edifact**
- **Aggregator - Sabre NDC**
- **Aggregator - Netactica**

---

## � PANTALLAS EXCLUSIVAS DE VUELOS

1. **Resumen** - Después de Disponibilidad, antes de CheckOut
2. **Modal Seguro de Cancelación** - **DESPUÉS** de la pantalla Resumen (si está activo)
3. **Modal Previo a Confirmación**
4. **Confirmación Vuelos+Seguro** - Si se aceptó el seguro de cancelación

---

## ✈️ SEGURO DE CANCELACIÓN

**Disponibilidad:** Solo para vuelos  
**Momento:** **DESPUÉS** de la pantalla Resumen

**Flujo:**
1. Se muestra Modal de Seguro de Cancelación (después del Resumen)
2. El socio puede Aceptar o Denegar
3. Si acepta:
   - Confirmación muestra pantalla especial: Confirmación Vuelos+Seguro
   - Incluye información del seguro de cancelación

**IMPORTANTE:** Voucher NO disponible para reservas de Vuelos+Seguro de Cancelación

---

## 🎫 VOUCHER EN ADMIN

**Disponibilidad:** ✅ SÍ

**Características:**
- Visualizable y descargable en el detalle de la reserva en Admin
- Formato: PDF
- Idioma: Español

**Limitación:**
- ❌ NO disponible para reservas de Vuelos+Seguro de Cancelación
- ✅ Disponible solo para vuelos sin seguro

---

## 🎚️ SLIDER Y MÉTODOS DE PAGO

### MÉTODOS DISPONIBLES:

**1. Solo Millas (100%):**
- Ajustar slider al 100% del valor del producto
- No se cobra nada en USD para el producto
- Fee de vuelos obligatorio con TC

**2. Millas+Plata (Copago):**
- Slider visible en CheckOut
- Mínimo: 20% del valor del producto
- Máximo: 100% o Millas disponibles
- Ajuste manual por el socio
- Cálculo dinámico en tiempo real

### FEE DE PROCESAMIENTO:
- **Obligatorio** para todos los vuelos
- **Formulario TC en CheckOut** (NO lightbox)
- **PlacetoPay bash** (sin interfaz visual)
- Se cobra al reservar mediante conexión bash

### ESCENARIOS DE PAGO:

**Escenario 1:** Millas ≥ 20% pero < 100%
```
✅ Mostrar Slider en CheckOut
- Ajustar desde 20% hasta Millas disponibles
- Cobrar restante en USD vía PlacetoPay bash
- Fee obligatorio con TC
```

**Escenario 2:** Millas < 20%
```
❌ Mostrar CheckOut con popup sobrepuesto
- Mensaje: "Debe comprar más Millas"
- CheckOut de fondo con gris transparente
- No permite continuar
```

**Escenario 3:** Millas ≥ 100%
```
✅ Mostrar Slider en CheckOut
- Ajustar desde 20% hasta 100%
- Socio decide cuántas Millas usar
- Fee obligatorio con TC
```

**Escenario 4:** Pago 100% Millas
```
✅ Ajustar slider al 100%
- No se cobra USD para el producto
- Fee obligatorio con TC (único cargo USD)
- Emisión automática
```

---

## �📋 PASOS OBLIGATORIOS DEL FLUJO E2E

**Siempre incluir estos pasos desde login:**

1. Ingresar a la URL https://clubmiles-ec.preprodppm.com/ | Portal cargado correctamente, pantalla principal visible
2. Realizar login con usuario y contraseña válidos | Login exitoso, acceso al home autenticado
3. Click en la opción Vuelos | Se despliega el formulario de búsqueda de vuelos
4. Seleccionar tipo de viaje (Ida y vuelta, Solo ida, Multidestino) | Tipo de viaje seleccionado correctamente
5. Ingresar criterios de búsqueda (origen, destino, fechas salida, fecha regreso, número de pasajeros, clase) | Criterios ingresados correctamente
6. Click en botón Buscar | Se muestran todos los vuelos disponibles
7. Validar que se muestra lista de vuelos con millas y fee de procesamiento visible | Lista de vuelos visible con precios en millas y fee en moneda
8. Click en botón Canjear de un vuelo disponible | Se despliega automáticamente el popup upsell
9. Seleccionar tarifa en el upsell (Básica, Estándar, Premium) y click en Continuar | Tarifa seleccionada, se muestra pantalla de resumen
10. Validar datos de resumen (vuelo, fechas, pasajeros, millas totales, fee de procesamiento) | Datos correctos y consistentes con la selección
11. Click en botón Continuar | Sistema redirige al checkout
12. Diligenciar todos los campos obligatorios (datos de pasajeros: nombre, apellido, documento, fecha nacimiento; datos de contacto: email, teléfono) | Campos completados correctamente
13. Validar que el fee de procesamiento es visible en el resumen del checkout | Fee mostrado correctamente
14. Validar que el logo P2P está visible (exclusivo de vuelos) | Logo P2P visible en checkout
15. Marcar check de Tratamiento de datos | Check seleccionado
16. Marcar check de Términos y condiciones | Check seleccionado
17. Validar que el botón Canjear se habilita al completar todos los campos obligatorios | Botón Canjear habilitado
18. Click en botón Canjear | Se despliega el lightbox de pago de fee
19. Ingresar datos de tarjeta de crédito en el lightbox (número, fecha vencimiento, CVV, titular) | Tarjeta validada y datos registrados correctamente
20. Click en botón Confirmar pago en el lightbox | Pago del fee procesado, lightbox se cierra y se muestra pantalla de confirmación
21. Validar pantalla de confirmación con código de reserva, resumen de pagos (millas canjeadas + fee pagado) | Código de reserva generado, pagos mostrados correctamente
22. Ingresar al módulo de administración CME | Admin cargado correctamente
23. Buscar reserva por código | Reserva localizada y visible
24. Validar que los pagos en admin coinciden con la confirmación (millas + fee) | Pagos correctos en admin
25. Validar que la reserva queda en estado EMITIDA automáticamente (100% millas - proceso automático) | Reserva en estado EMITIDA
26. [Solo para SABRE EDIFACT] Validar dispersión de fondos (fee a PPM, valor del vuelo según el proveedor correspondiente) | Dispersión realizada correctamente en Sabre

---

## 🔄 VARIACIONES SEGÚN ESCENARIO

**Tipo de viaje:**
- Ida y vuelta
- Solo ida
- Multidestino (máximo 4 tramos)

**Proveedores:**
- AGGREGATOR - NETACTICA (sin dispersión)
- AGGREGATOR - SABRE (sin dispersión)
- SABRE EDIFACT (con dispersión de fondos)

**Pasajeros:**
- 1 pasajero
- Múltiples pasajeros (2-9)

**Clase:**
- Económica
- Premium Economy
- Business
- Primera clase

**Tarifas (Upsell):**
- Básica (solo vuelo)
- Estándar (vuelo + equipaje adicional)
- Premium (vuelo + equipaje + asiento + cambios)

---

## ✅ VALIDACIONES CRÍTICAS

✅ **Integridad de datos:** Consistencia entre búsqueda → disponibilidad → upsell → resumen → checkout → confirmación → admin  
✅ **Fee de procesamiento:** Siempre visible y cobrado con tarjeta de crédito en lightbox  
✅ **Logo P2P:** Visible en checkout (exclusivo de vuelos)  
✅ **Cálculo de millas:** Millas totales correctas según tarifa y cantidad de pasajeros  
✅ **Campos obligatorios:** Datos de todos los pasajeros, contacto, aceptación de términos  
✅ **Links funcionales:** Términos y condiciones, tratamiento de datos abren correctamente  
✅ **Lightbox:** Formulario de tarjeta funcional, validación de datos  
✅ **Estados de reserva:** Confirmada en admin con todos los datos completos  
✅ **Emisión automática:** Reserva en estado EMITIDA sin intervención manual  
✅ **Proveedor:** Validar proveedor correcto (NETACTICA, SABRE, SABRE EDIFACT)  
✅ **Dispersión:** Solo en SABRE EDIFACT, validar fee a PPM y valor vuelo al proveedor  

---

## 📝 FORMATO DE TÍTULO

```
[CME] Vuelos - [Tipo viaje] - [Proveedor] - [Característica especial]
```

**Ejemplos:**
- `[CME] Vuelos - Ida y vuelta - SABRE EDIFACT - Fee con lightbox - 2 pasajeros`
- `[CME] Vuelos - Solo ida - NETACTICA - Tarifa Premium - 1 pasajero`
- `[CME] Vuelos - Multidestino - AGGREGATOR SABRE - 3 tramos - 4 pasajeros`

---

## 📸 IMÁGENES DE REFERENCIA

Incluir SIEMPRE estas imágenes en el campo Descriptions del Test Case:

- Home-vuelos-CME.png - Pantalla principal con opción Vuelos
- Disponibilidad-vuelos-CME.png - Lista de vuelos disponibles con millas y fee
- upsell-vuelos-CME.png - Popup de selección de tarifas
- Resumen-vuelos-CME.png - Pantalla de resumen antes del checkout
- Checkout-vuelos-CME.png - Formulario de checkout completo con logo P2P
- lightBox-vuelos-CME.png - Lightbox de pago del fee con tarjeta
- Confirmacion-vuelos-CME.png - Pantalla de confirmación con código de reserva
- Admin.png - Validación en módulo admin CME

---

## 📌 NOTAS IMPORTANTES

**Fee de procesamiento:**
- SIEMPRE requerido en vuelos (diferencia con hoteles, autos, actividades, disney)
- Pago SOLO con tarjeta de crédito en lightbox
- No se puede canjear con millas

**Logo P2P:**
- Exclusivo de vuelos
- Debe ser visible en checkout
- NO aparece en otros productos

**Dispersión de fondos:**
- Solo en SABRE EDIFACT
- Fee se dispersa a PPM (Plataforma de pagos)
- Valor del vuelo se dispersa al proveedor correspondiente
- NETACTICA y AGGREGATOR SABRE NO tienen dispersión

**Emisión:**
- Siempre automática (100% millas)
- Estado EMITIDA inmediato tras confirmación
- Sin proceso manual (diferente a BGR con pago mixto)

---

**Última actualización:** 2026-01-06  
**Versión:** 1.0.0  
**Mantenido por:** QA Team Ultragroup

✅ **Emisión:** Automática (100% millas) / Manual (mixto)  
✅ **Admin - Solo Millas:** Estado EMITIDA automáticamente  
✅ **Admin - Millas + Plata:** Proceso manual (debitar → emitir cash)  

---

## 📝 FORMATO DE TÍTULO

```
[{PORTAL}] {PRODUCTO} - [Escenario] - [Variante] - [Característica especial]
```

**Ejemplos:**
- `[{PORTAL}] {PRODUCTO} - [Escenario A] - [Variante X] - {PROVEEDOR}`
- `[{PORTAL}] {PRODUCTO} - [Escenario B] - [Variante Y] - [Característica especial]`
- `[{PORTAL}] {PRODUCTO} - [Escenario C] - [Múltiples opciones]`

**Para PM:**
```
[PM] {PRODUCTO} - [Escenario] - [Variante] - {PROVEEDOR}
```

**Para BGR:**
```
[BGR] {PRODUCTO} - [Escenario] - [Modelo de pago] - {PROVEEDOR}
```

---

## 🖼️ RECURSOS VISUALES (Opcional)

**Si existen capturas de pantalla del flujo:**

Agregar a `.github/imagenes/{PORTAL}/{producto}/`:
- Home-{producto}-{PORTAL}.png
- Disponibilidad-{producto}-{PORTAL}.png
- Checkout-{producto}-{PORTAL}.png
- Confirmacion-{producto}-{PORTAL}.png
- Admin.png

**Referencias en Descriptions:**
```html
<strong>📸 Imágenes de referencia del flujo:</strong><br>
• Home-{producto}-{PORTAL}.png - Pantalla principal<br>
• Disponibilidad-{producto}-{PORTAL}.png - Resultados de búsqueda<br>
• Checkout-{producto}-{PORTAL}.png - Pantalla de checkout<br>
• Confirmacion-{producto}-{PORTAL}.png - Confirmación de reserva<br>
• Admin.png - Módulo administrativo<br>
```

---

## ⚙️ CONFIGURACIÓN TÉCNICA

**Tecnología:** {TECNOLOGIA}  
**Framework:** [Especificar si es Angular con TypeScript, Meteor con MongoDB, etc.]  
**Proveedor externo:** {PROVEEDOR}  
**API de integración:** [Si aplica]  
**Proceso de emisión:** [Automático/Manual/Mixto]  

---

## 📊 MATRIZ DE ESCENARIOS

| Escenario | Variante | Validaciones clave | Prioridad |
|-----------|----------|-------------------|-----------|
| [Escenario A] | [Variante X] | [Lista de validaciones] | Alta |
| [Escenario B] | [Variante Y] | [Lista de validaciones] | Media |
| [Escenario C] | [Variante Z] | [Lista de validaciones] | Baja |

---

## 🔗 REFERENCIAS

**Documentación relacionada:**
- [{PORTAL}_COMMON_RULES.md](../shared/{PORTAL}_COMMON_RULES.md) - Reglas comunes del portal
- [SHARED_QA_RULES.md](../shared/SHARED_QA_RULES.md) - Fundamentos ISTQB

**Documentación del proveedor:**
- [Link a documentación oficial del proveedor si está disponible]

---

## ✅ CHECKLIST FINAL (Verificar antes de commit)

- [ ] Metadata YAML completa
- [ ] Portal correcto (PM o BGR)
- [ ] Pasos E2E completos (mínimo 15-30)
- [ ] Inicio desde login (paso 1)
- [ ] Cada paso tiene resultado esperado
- [ ] Validaciones críticas documentadas
- [ ] Variaciones según escenario incluidas
- [ ] Formato de título definido
- [ ] Proveedor identificado
- [ ] Modelo de pago descrito
- [ ] Referencias a COMMON_RULES
- [ ] Imágenes agregadas (si aplica)
- [ ] CHANGELOG.md actualizado
- [ ] Agente actualizado con referencia a este archivo
- [ ] COMMON_RULES actualizado con nuevo producto
- [ ] Sin duplicación de información compartida

---

## 🚀 PRÓXIMOS PASOS

Después de completar este archivo:

1. **Actualizar agente:**
   ```markdown
   En {PORTAL}_QA_Assistant.agent.md agregar:
   🎨 [{PORTAL}_{PRODUCTO}.md](../products/{PORTAL}_{PRODUCTO}.md) - Flujo E2E completo de {PRODUCTO}
   ```

2. **Actualizar COMMON_RULES:**
   ```markdown
   En {PORTAL}_COMMON_RULES.md agregar a estructura de proveedores:
   ├─ 🎨 {PRODUCTO} [{TECNOLOGIA}]
   │  └─ {PROVEEDOR}
   ```

3. **Documentar en CHANGELOG:**
   ```markdown
   ## [Unreleased]
   ### Added
   - ✅ {PORTAL}_{PRODUCTO}.md (X pasos E2E)
   - ✅ Proveedor: {PROVEEDOR}
   - ✅ Tecnología: {TECNOLOGIA}
   ```

4. **Validar:**
   ```powershell
   .\validation\validate-structure.ps1
   ```

---

## 📸 IMÁGENES DE REFERENCIA

**Incluir SIEMPRE en el campo Descriptions del Test Case:**

```
.github/images/CME/Vuelos/
├── Home-vuelos-CME.png
├── Disponibilidad-vuelos-CME.png
├── Resumen-vuelos-CME.png
├── Modal-seguro-CME.png (si aplica)
├── Checkout-vuelos-CME.png (con slider y formulario TC)
├── Confirmacion-vuelos-CME.png
├── Confirmacion-vuelos-seguro-CME.png (si aplica)
├── Voucher-vuelos-CME.png
└── Admin.png
```

---

**Template versión:** 1.0.0  
**Fecha creación:** 2026-01-05  
**Mantenido por:** QA Team Ultragroup
