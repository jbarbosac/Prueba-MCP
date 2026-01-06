# 🚗 FLUJO E2E OBLIGATORIO PARA AUTOS - BGR

**Proveedor:** BGR Miles Ecuador  
**Portal:** https://bgrmiles-ec.preprodppm.com/  
**Modelo de pago:** Millas (100%) o Millas + Plata (slider con mínimo 20% del total de millas)  

---

## 📦 PROVEEDORES Y EMPRESAS DE SERVICIO

**Proveedor:** Sabre  
**Empresas de renta:** Hertz, Dollar, Thrifty

---

## 📋 PASOS OBLIGATORIOS DEL FLUJO E2E

**Siempre incluir estos pasos desde login para el flujo de Autos:**

1. Ingresar al portal https://bgrmiles-ec.preprodppm.com/ | El portal carga correctamente y muestra la pantalla de inicio
2. Realizar login con usuario y contraseña válidos | Login exitoso y acceso al home
3. Click en la opción Autos | Se despliega el formulario de búsqueda de autos
4. Validar si se selecciona "Devolver en otro destino" | Si se selecciona: se habilita campo ciudad de entrega; Si NO: solo se solicita lugar de recogida
5. Diligenciar ciudad de recogida | La ciudad de recogida queda registrada correctamente
6. Diligenciar ciudad de entrega (solo si aplica "Devolver en otro destino") | La ciudad de entrega queda registrada (si aplica)
7. Seleccionar fecha de recogida | La fecha de recogida queda registrada
8. Seleccionar fecha de devolución | La fecha de devolución queda registrada
9. Seleccionar hora de recogida | La hora de recogida queda registrada
10. Seleccionar hora de devolución | La hora de devolución queda registrada
11. Validar que el botón "Buscar autos" se habilite cuando todos los campos obligatorios estén completos | El botón "Buscar autos" se habilita
12. Click en "Buscar autos" | Se muestra la pantalla de disponibilidad con autos
13. Validar todos los atributos de autos disponibles (modelo, categoría, capacidad, transmisión, aire acondicionado, tarifa, proveedor, millas) | La información se muestra correctamente
14. Si se seleccionó "Devolver en otro destino": Validar que se muestre el cargo adicional de Drop-off fee en la tarifa | El Drop-off fee aparece desglosado en la tarifa del auto
15. Mover el slider para seleccionar modo de pago (Solo Millas o Millas + Plata con mínimo 20% del total de millas) | El sistema muestra el valor según la selección del slider
16. Seleccionar proveedor (Hertz, Dollar o Thrifty) dando click | Se navega al checkout
17. Diligenciar todos los campos obligatorios del checkout | Los campos quedan completos correctamente
18. Si se seleccionó "Devolver en otro destino": Validar que en el resumen del checkout aparezca el cargo de Drop-off fee | El Drop-off fee está incluido en el total a pagar
19. Si es Millas + Plata: Ingresar tarjeta de crédito para pagar el componente en dinero | El sistema valida y registra la tarjeta
20. Si es Solo Millas: NO ingresar tarjeta | El método de pago queda solo con millas
21. Marcar el check de Tratamiento de datos | Check seleccionado
22. Marcar el check de Términos y condiciones | Check seleccionado
23. Validar que los enlaces de Tratamiento de datos y Términos y condiciones funcionan | Los links abren correctamente en nueva pestaña
24. Validar que el botón Canjear se habilite únicamente cuando todos los campos obligatorios estén completos | El botón Canjear se habilita
25. Click en el botón Canjear | Se procesa la reserva y se genera la confirmación
26. Validar que la pantalla de confirmación muestre correctamente el código de reserva y el pago realizado (millas y/o plata) | Valores y código correctos
27. Si se seleccionó "Devolver en otro destino": Validar en Sabre que el Drop-off fee esté registrado correctamente | El cargo de Drop-off fee aparece en Sabre
28. Validar en el admin que el valor pagado (millas y/o plata) coincida con la reserva generada, incluyendo Drop-off fee si aplica | Valores coinciden con checkout y confirmación, Drop-off fee incluido
29. Si fue Solo Millas: Validar en el Admin que la reserva quedó emitida automáticamente | La reserva aparece como emitida
30. Si fue Millas + Plata: En el Admin abrir la reserva, debitar millas y luego pagar cash | La reserva queda emitida tras el proceso manual

---

## 🔄 VARIACIONES SEGÚN ESCENARIO

**Recogida y entrega:**
- Mismo lugar (NO seleccionar "Devolver en otro destino")
- Lugares diferentes (SI seleccionar "Devolver en otro destino")

**Días de renta:**
- 1 a N días

**Categoría:**
- Económico, Compacto, Intermedio, SUV, Lujo

**Transmisión:**
- Manual, Automática

**Proveedor:**
- Hertz, Dollar, Thrifty

**Modelo de pago:**
- Solo Millas (100% - emisión automática)
- Millas + Plata (mixto - emisión manual)

---

## ✅ VALIDACIONES CRÍTICAS

✅ **Integridad de datos:** Consistencia entre búsqueda → resultado → selección proveedor → checkout → confirmación → Sabre → admin  
✅ **Opción "Devolver en otro destino":** Validar que si se selecciona, se habilite campo ciudad de entrega; si NO se selecciona, solo usar lugar de recogida  
✅ **Drop-off fee (cargo adicional por devolver en otro destino):** Validar que se muestre en disponibilidad, checkout, confirmación, Sabre y admin cuando aplica  
✅ **Campos obligatorios:** Ciudad recogida, ciudad entrega (si aplica), fechas recogida/devolución, horas recogida/devolución  
✅ **Botón "Buscar autos":** Debe habilitarse SOLO cuando todos los campos obligatorios estén completos  
✅ **Atributos de autos:** Validar modelo, categoría, capacidad, transmisión, aire acondicionado, tarifa, proveedor, millas  
✅ **Slider funcional:** Mover entre Solo Millas (100%) y Millas + Plata (validar mínimo 20% del total de millas para autos)  
✅ **Proveedores disponibles:** Hertz, Dollar, Thrifty  
✅ **Cálculo de millas:** Millas totales = millas base según días de renta y categoría de auto + Drop-off fee (si aplica)  
✅ **Cálculo de plata (cuando aplica):** Plata total = plata según días de renta y selección del slider + Drop-off fee (si aplica)  
✅ **Cálculo visible en checkout:** Débito de millas seleccionadas en slider visible en resumen + Drop-off fee desglosado (si aplica)  
✅ **Campos obligatorios checkout:** Todos los campos del conductor completos, tarjeta solo si es Millas + Plata, aceptación de términos  
✅ **Links funcionales:** Términos y condiciones, tratamiento de datos abren correctamente  
✅ **Estados de reserva:** Solo Millas = Emisión automática; Millas + Plata = Proceso manual (debitar millas → pagar cash → emisión)  
✅ **Fechas:** Recogida y devolución correctas, días calculados correctamente  
✅ **Proveedor:** Validar que sea Hertz, Dollar o Thrifty según selección  
✅ **NO validar fees:** En BGR no se calculan ni validan fees de procesamiento  

---

## 📝 FORMATO DE TÍTULO

```
[BGR] Autos - [Duración] - [Empresa] - [Modelo de pago] - [Característica especial]
```

**Ejemplos:**
- `[BGR] Autos - 5 días - Hertz - Solo Millas automático - Mismo destino`
- `[BGR] Autos - 3 días - Dollar - Millas + Plata manual - Dropoff diferente`
- `[BGR] Autos - 7 días - Thrifty - Solo Millas automático - Dropoff internacional`
