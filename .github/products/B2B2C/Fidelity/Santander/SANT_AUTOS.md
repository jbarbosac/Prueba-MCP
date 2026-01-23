# 🚗 SANTANDER - FLUJO E2E AUTOS

**Portal:** Santander  
**Producto:** Autos  
**Prefijo:** [SANT]  
**Modelo:** B2B2C (Fidelity)  

---

## 📋 INFORMACIÓN GENERAL

### PROVEEDOR(ES):
**⚠️ PENDIENTE DEFINIR:**
- Proveedor principal: [Sabre / Otro]
- Empresas de renta disponibles: [Hertz, Dollar, Thrifty, Avis, Budget, National, Alamo, Europcar, Sixt, etc.]

### MODELO DE PAGO:
**⚠️ PENDIENTE DEFINIR:**
```
Opción A: 100% PUNTOS SANTANDER
Opción B: X% PUNTOS + Y% TARJETA (slider)
Opción C: Puntos + Tarjeta (proporciones fijas)
```

---

## 🔄 FLUJO E2E COMPLETO

### PASO 1: LOGIN
[Ver flujo de login en SANT_VUELOS.md]

---

### PASO 2: HOME / SELECCIÓN DE PRODUCTO
**Acciones:**
1. Desde el home/marketplace
2. Hacer clic en "Autos" o "Renta de autos"

---

### PASO 3: BÚSQUEDA DE AUTOS
**Pantalla:** Formulario de búsqueda de autos

**Campos obligatorios:**
- Lugar de recogida (ciudad/aeropuerto)
- Fecha y hora de recogida
- Lugar de devolución (mismo lugar o diferente)
- Fecha y hora de devolución
- Edad del conductor

**Acciones:**
1. Ingresar lugar de recogida
2. Seleccionar fecha y hora de recogida
3. Seleccionar "Devolver en el mismo lugar" o ingresar lugar diferente
4. Seleccionar fecha y hora de devolución
5. Ingresar edad del conductor (validar mínimo 21-25 según empresa)
6. Hacer clic en "Buscar autos"

**Validaciones:**
- ✅ Fecha de recogida no puede ser anterior a hoy
- ✅ Fecha de devolución debe ser posterior a recogida
- ✅ Mínimo 1 día de renta
- ✅ Edad mínima del conductor (21-25 años según empresa)
- ✅ Ubicación de recogida válida
- ✅ Horarios de oficina validados (si aplica)

---

### PASO 4: DISPONIBILIDAD DE AUTOS
**Pantalla:** Resultados de búsqueda

**Información mostrada por auto:**
- Empresa de renta (Hertz, Dollar, Thrifty, etc.)
- Categoría del vehículo (Compacto, SUV, Lujo, etc.)
- Modelo del vehículo (o similar)
- Capacidad (pasajeros y maletas)
- Transmisión (Manual/Automática)
- Aire acondicionado
- Política de combustible
- Precio en puntos (o puntos + dinero)
- Seguros incluidos

**Acciones:**
1. Revisar autos disponibles
2. Aplicar filtros (si disponibles):
   - Empresa de renta
   - Categoría de vehículo
   - Transmisión
   - Precio
3. Comparar opciones
4. Seleccionar auto deseado
5. Hacer clic en "Continuar" o "Seleccionar"

**Validaciones:**
- ✅ Al menos un resultado disponible o mensaje apropiado
- ✅ Información completa de cada vehículo
- ✅ Precio en puntos calculado correctamente
- ✅ Verificación de puntos suficientes
- ✅ Términos y condiciones de la empresa visibles

---

### PASO 5: EXTRAS Y SERVICIOS ADICIONALES
**Pantalla:** Servicios adicionales del auto

**Opciones comunes:**
- GPS/Navegador
- Silla para bebé/niño
- Conductor adicional
- Seguro adicional (cobertura extendida)
- Peajes/autopistas prepagados
- Tanque lleno (pago anticipado)

**Acciones:**
1. Revisar extras disponibles
2. Seleccionar extras deseados (opcional)
3. Revisar costo adicional en puntos
4. Hacer clic en "Continuar"

**Validaciones:**
- ✅ Costo adicional mostrado claramente
- ✅ Extras opcionales, no obligatorios
- ✅ Total actualizado con extras seleccionados
- ✅ Descripción clara de cada extra

---

### PASO 6: RESUMEN DE RESERVA
**Pantalla:** Resumen del auto seleccionado

**Información a mostrar:**
- Detalles del vehículo
- Lugar y hora de recogida/devolución
- Número de días de renta
- Extras seleccionados
- Seguros incluidos
- Puntos totales a canjear
- Dinero adicional (si modelo es mixto)
- Políticas de cancelación

**Validaciones:**
- ✅ Consistencia de datos
- ✅ Cálculo correcto de puntos
- ✅ Políticas claramente visibles
- ✅ Términos y condiciones de la empresa de renta

---

### PASO 7: CHECKOUT - DATOS DEL CONDUCTOR
**Pantalla:** Formulario de datos del conductor

**Campos obligatorios:**
- Nombre(s) completo(s)
- Apellido(s) completo(s)
- Tipo de documento
- Número de documento
- Fecha de nacimiento
- Edad (validación automática)
- Número de licencia de conducir
- País emisor de licencia
- Fecha de vencimiento de licencia
- Email
- Teléfono
- Dirección completa

**Conductor adicional (si aplica):**
- Datos completos del conductor adicional

**Acciones:**
1. Ingresar datos del conductor principal
2. Ingresar datos del conductor adicional (si se seleccionó)
3. Aceptar términos y condiciones de la empresa de renta
4. Aceptar política de tratamiento de datos
5. Hacer clic en "Continuar"

**Validaciones:**
- ✅ Edad del conductor coincide con fecha de nacimiento
- ✅ Edad mínima cumplida (21-25 años)
- ✅ Licencia de conducir vigente
- ✅ Licencia con antigüedad mínima (si aplica)
- ✅ Email válido
- ✅ Teléfono válido
- ✅ Términos aceptados obligatoriamente

---

### PASO 8: PAGO
[Ver proceso de pago según modelo en SANT_VUELOS.md]

---

### PASO 9: CONFIRMACIÓN DE RESERVA
**Pantalla:** Confirmación exitosa

**Información a mostrar:**
- Número de reserva
- Código de confirmación de la empresa de renta
- Resumen del auto reservado
- Lugar y hora de recogida
- Datos del conductor
- Puntos debitados
- Estado: CONFIRMADA
- Instrucciones de recogida
- Documentos requeridos en el counter

**Validaciones:**
- ✅ Número de reserva único
- ✅ Código de confirmación válido del proveedor
- ✅ Email de confirmación enviado
- ✅ Puntos debitados correctamente
- ✅ Voucher descargable

---

### PASO 10: VALIDACIÓN EN ADMIN
**Acciones:**
1. Login en panel de admin
2. Buscar reserva por número
3. Verificar estado CONFIRMADA
4. Verificar todos los datos

**Validaciones:**
- ✅ Reserva existe en el sistema
- ✅ Proveedor correcto (Sabre)
- ✅ Empresa de renta correcta
- ✅ Datos del conductor completos
- ✅ Datos del auto (categoría, modelo)
- ✅ Fechas y horas de recogida/devolución
- ✅ Puntos debitados
- ✅ Extras registrados

---

## 🎯 CASOS DE PRUEBA SUGERIDOS

1. **[SANT] Autos - Mismo lugar - [Empresa] - 3 días - Compacto**
2. **[SANT] Autos - Dropoff diferente - [Empresa] - 5 días - SUV**
3. **[SANT] Autos - Con GPS - [Empresa] - 7 días**
4. **[SANT] Autos - Con silla de bebé - [Empresa] - 4 días**
5. **[SANT] Autos - Conductor adicional - [Empresa] - 5 días**
6. **[SANT] Autos - Conductor menor de 25 años - Cargo adicional**
7. **[SANT] Autos - Licencia internacional - Validación**
8. **[SANT] Autos - Cancelación de reserva**
9. **[SANT] Autos - Modificación de fechas pre-recogida**
10. **[SANT] Autos - Seguro extendido - Cobertura completa**

---

## 📚 REFERENCIAS

📋 [SANTANDER_COMMON_RULES.md](../../../shared/Reglas Marketplace/SANTANDER_COMMON_RULES.md)  
📋 [SHARED_QA_RULES.md](../../../shared/SHARED_QA_RULES.md)  

---

**Versión:** 1.0.0  
**Fecha de creación:** 2026-01-23  
**Estado:** ⚠️ PENDIENTE COMPLETAR INFORMACIÓN TÉCNICA  
