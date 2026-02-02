# 🏨 SANTANDER - FLUJO E2E HOTELES

**Portal:** Santander  
**Producto:** Hoteles  
**Prefijo:** [SANT]  
**Modelo:** B2B2C (Fidelity)  

---

## 📋 INFORMACIÓN GENERAL

### PROVEEDOR(ES):
**⚠️ PENDIENTE DEFINIR:**
- Proveedor principal: [HotelBeds / Expedia / Otro]

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
2. Hacer clic en "Hoteles"

---

### PASO 3: BÚSQUEDA DE HOTELES
**Pantalla:** Formulario de búsqueda de hoteles

**Campos obligatorios:**
- Destino (ciudad/región)
- Fecha de check-in
- Fecha de check-out
- Número de habitaciones
- Número de adultos por habitación
- Número de niños por habitación (edad de cada niño)

**Acciones:**
1. Ingresar destino
2. Seleccionar fecha de check-in
3. Seleccionar fecha de check-out (mínimo 1 noche)
4. Definir número de habitaciones
5. Seleccionar número de huéspedes (adultos/niños)
6. Ingresar edad de niños (si aplican)
7. Hacer clic en "Buscar hoteles"

**Validaciones:**
- ✅ Destino válido
- ✅ Check-in no puede ser anterior a hoy
- ✅ Check-out debe ser posterior a check-in
- ✅ Mínimo 1 noche
- ✅ Máximo de habitaciones permitido (típicamente 5-9)
- ✅ Edad de niños requerida si hay niños
- ✅ Botón deshabilitado hasta completar campos

---

### PASO 4: DISPONIBILIDAD DE HOTELES
**Pantalla:** Resultados de búsqueda

**Información mostrada por hotel:**
- Nombre del hotel
- Categoría (estrellas: 1-5)
- Ubicación/zona
- Distancia al centro
- Calificación de huéspedes
- Servicios/amenidades principales
- Tipo(s) de habitación disponibles
- Régimen alimenticio (Solo alojamiento, Desayuno incluido, Media pensión, Todo incluido)
- Política de cancelación
- Precio en puntos (o puntos + dinero)
- Disponibilidad

**Acciones:**
1. Revisar hoteles disponibles
2. Aplicar filtros (si disponibles):
   - Categoría (estrellas)
   - Precio
   - Zona/ubicación
   - Servicios (piscina, wifi, estacionamiento, etc.)
   - Tipo de habitación
   - Régimen alimenticio
   - Calificación de huéspedes
3. Ver detalles del hotel (fotos, descripción completa)
4. Seleccionar tipo de habitación
5. Hacer clic en "Continuar" o "Reservar"

**Validaciones:**
- ✅ Al menos un resultado disponible o mensaje apropiado
- ✅ Información completa de cada hotel
- ✅ Precio en puntos calculado correctamente por noche/total
- ✅ Verificación de puntos suficientes
- ✅ Fotos del hotel cargadas correctamente
- ✅ Política de cancelación claramente visible
- ✅ Términos y condiciones del hotel

---

### PASO 5: DETALLE DEL HOTEL
**Pantalla:** Información completa del hotel seleccionado

**Información a mostrar:**
- Galería de fotos
- Descripción completa
- Ubicación en mapa
- Servicios e instalaciones
- Habitaciones disponibles con detalles:
  - Tipo de cama
  - Capacidad
  - Servicios de la habitación
  - Vistas
  - Metraje
- Políticas del hotel:
  - Check-in/check-out
  - Cancelación
  - Depósito/garantía
  - Niños y camas adicionales
  - Mascotas
- Reseñas de huéspedes

**Acciones:**
1. Revisar detalles completos
2. Seleccionar tipo de habitación específica
3. Confirmar número de noches
4. Hacer clic en "Reservar"

**Validaciones:**
- ✅ Información coherente con búsqueda
- ✅ Disponibilidad confirmada
- ✅ Precio total claro (todas las noches)
- ✅ Impuestos/cargos adicionales especificados

---

### PASO 6: RESUMEN DE RESERVA
**Pantalla:** Resumen del hotel seleccionado

**Información a mostrar:**
- Nombre y categoría del hotel
- Ubicación
- Fechas (check-in / check-out)
- Número de noches
- Tipo de habitación
- Régimen alimenticio
- Número de huéspedes
- Puntos totales a canjear
- Dinero adicional (si modelo es mixto)
- Política de cancelación
- Términos y condiciones

**Validaciones:**
- ✅ Consistencia de datos
- ✅ Cálculo correcto: puntos por noche × número de noches
- ✅ Políticas claramente visibles
- ✅ Opción de modificar antes de continuar

---

### PASO 7: CHECKOUT - DATOS DE HUÉSPEDES
**Pantalla:** Formulario de datos de huéspedes

**Huésped principal (obligatorio):**
- Nombre(s) completo(s)
- Apellido(s) completo(s)
- Tipo de documento
- Número de documento
- Nacionalidad
- Fecha de nacimiento
- Email
- Teléfono
- País de residencia

**Huéspedes adicionales (opcional, puede requerirse solo nombre):**
- Datos de otros huéspedes según políticas del hotel

**Solicitudes especiales (opcional):**
- Cama extra
- Cuna
- Piso alto/bajo
- Habitación con vista
- Llegada tarde
- Otras solicitudes

**Acciones:**
1. Ingresar datos del huésped principal
2. Ingresar datos de huéspedes adicionales (si requerido)
3. Agregar solicitudes especiales (opcional)
4. Aceptar términos y condiciones del hotel
5. Aceptar política de tratamiento de datos
6. Hacer clic en "Continuar"

**Validaciones:**
- ✅ Datos del huésped principal completos
- ✅ Email válido
- ✅ Teléfono válido
- ✅ Fecha de nacimiento coherente
- ✅ Términos aceptados obligatoriamente

---

### PASO 8: PAGO
[Ver proceso de pago según modelo en SANT_VUELOS.md]

---

### PASO 9: CONFIRMACIÓN DE RESERVA
**Pantalla:** Confirmación exitosa

**Información a mostrar:**
- Número de reserva
- Código de confirmación del hotel
- Resumen de la reserva:
  - Hotel
  - Fechas (check-in: día/hora, check-out: día/hora)
  - Habitación
  - Huéspedes
- Puntos debitados
- Estado: CONFIRMADA
- Instrucciones de check-in
- Datos de contacto del hotel
- Política de cancelación
- Voucher descargable

**Validaciones:**
- ✅ Número de reserva único
- ✅ Código de confirmación válido del proveedor
- ✅ Email de confirmación enviado
- ✅ Puntos debitados correctamente
- ✅ Voucher con todos los detalles

---

### PASO 10: VALIDACIÓN EN ADMIN
**Acciones:**
1. Login en panel de admin
2. Buscar reserva por número
3. Verificar estado CONFIRMADA
4. Verificar todos los datos

**Validaciones:**
- ✅ Reserva existe en el sistema
- ✅ Proveedor correcto
- ✅ Datos del hotel (nombre, ubicación, categoría)
- ✅ Datos de la habitación (tipo, régimen)
- ✅ Fechas correctas (check-in, check-out, noches)
- ✅ Datos del huésped principal
- ✅ Puntos debitados
- ✅ Política de cancelación registrada

---

## 🎯 CASOS DE PRUEBA SUGERIDOS

### CASOS BÁSICOS:

1. **[SANT] Hoteles - 1 noche - [Proveedor] - 1 adulto - Solo alojamiento**
2. **[SANT] Hoteles - 2 noches - [Proveedor] - 2 adultos - Desayuno incluido**
3. **[SANT] Hoteles - 3 noches - [Proveedor] - 2 adultos + 1 niño - Media pensión**
4. **[SANT] Hoteles - 5 noches - [Proveedor] - Familia (2 adultos + 2 niños)**
5. **[SANT] Hoteles - 7 noches - [Proveedor] - Todo incluido**

### CASOS INTERMEDIOS:

6. **[SANT] Hoteles - 2 habitaciones - 4 adultos - Desayuno**
7. **[SANT] Hoteles - Cancelación gratuita - Reserva y cancelación**
8. **[SANT] Hoteles - No reembolsable - Mejor precio**
9. **[SANT] Hoteles - Hotel 5 estrellas - Lujo**
10. **[SANT] Hoteles - Con solicitudes especiales - Cama extra**

### CASOS AVANZADOS:

11. **[SANT] Hoteles - Llegada tarde (después de medianoche)**
12. **[SANT] Hoteles - Estancia larga - 14 noches**
13. **[SANT] Hoteles - Múltiples habitaciones diferentes**
14. **[SANT] Hoteles - Modificación de fechas pre-check-in**
15. **[SANT] Hoteles - Cancelación y reembolso de puntos**

---

## 📚 REFERENCIAS

📋 [SANTANDER_COMMON_RULES.md](../../../shared/Reglas Marketplace/SANTANDER_COMMON_RULES.md)  
📋 [SHARED_QA_RULES.md](../../../shared/SHARED_QA_RULES.md)  

---

**Versión:** 1.0.0  
**Fecha de creación:** 2026-01-23  
**Estado:** ⚠️ PENDIENTE COMPLETAR INFORMACIÓN TÉCNICA  
