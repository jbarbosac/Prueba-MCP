# 🎡 SANTANDER - FLUJO E2E TICKETS DISNEY

**Portal:** Santander  
**Producto:** Tickets Disney  
**Prefijo:** [SANT]  
**Modelo:** B2B2C (Fidelity)  

---

## 📋 INFORMACIÓN GENERAL

### PROVEEDOR(ES):
**⚠️ PENDIENTE DEFINIR:**
- Proveedor principal: [DerbySoft / OffLine / Otro]

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
2. Hacer clic en "Disney" o "Tickets Disney"

---

### PASO 3: SELECCIÓN DE DESTINO DISNEY
**Pantalla:** Selección de complejo Disney

**Opciones disponibles (según proveedor):**
- Walt Disney World (Orlando, Florida)
  - Magic Kingdom
  - EPCOT
  - Hollywood Studios
  - Animal Kingdom
- Disneyland Resort (California)
  - Disneyland Park
  - Disney California Adventure
- Disneyland Paris (Francia)
- Tokyo Disney Resort (Japón)
- Hong Kong Disneyland
- Shanghai Disney Resort

**Acciones:**
1. Seleccionar destino Disney
2. Hacer clic en "Continuar"

**Validaciones:**
- ✅ Selección obligatoria de destino
- ✅ Información del destino visible (ubicación, parques incluidos)

---

### PASO 4: CONFIGURACIÓN DE TICKETS
**Pantalla:** Opciones de tickets

**Configuraciones a definir:**

**A) Número de días:**
- 1 día
- 2 días
- 3 días
- 4 días
- 5 días
- Hasta 10 días (según destino)

**B) Número de visitantes:**
- Adultos (10+ años)
- Niños (3-9 años)
- Infantes (0-2 años) - Generalmente gratis

**C) Tipo de ticket:**
- **Base Ticket:** Acceso a 1 parque por día
- **Park Hopper:** Acceso a múltiples parques el mismo día
- **Park Hopper Plus:** Park Hopper + parques acuáticos y más

**D) Fecha de inicio:**
- Seleccionar primera fecha de uso
- Válido por número de días consecutivos o dentro de ventana (según tipo)

**Acciones:**
1. Seleccionar número de días
2. Seleccionar número de visitantes (adultos/niños)
3. Seleccionar tipo de ticket (Base / Park Hopper / Park Hopper Plus)
4. Seleccionar fecha de inicio
5. Hacer clic en "Buscar" o "Ver precios"

**Validaciones:**
- ✅ Número de días seleccionado
- ✅ Al menos 1 visitante (adulto o niño)
- ✅ Fecha de inicio no puede ser anterior a hoy
- ✅ Fecha de inicio dentro del período de validez permitido (típicamente hasta 1 año adelante)
- ✅ Información clara de qué incluye cada tipo de ticket

---

### PASO 5: DISPONIBILIDAD Y PRECIOS
**Pantalla:** Opciones de tickets con precios

**Información mostrada:**
- Resumen de la configuración:
  - Destino Disney
  - Número de días
  - Tipo de ticket
  - Número de visitantes
- Precio por visitante (adulto/niño)
- Precio total en puntos (o puntos + dinero)
- Qué incluye el ticket
- Restricciones y condiciones
- Política de cancelación

**Acciones:**
1. Revisar opciones de tickets disponibles
2. Comparar precios entre tipos (si hay opciones)
3. Seleccionar ticket deseado
4. Hacer clic en "Continuar" o "Reservar"

**Validaciones:**
- ✅ Precio calculado correctamente: (precio por adulto × adultos) + (precio por niño × niños)
- ✅ Verificación de puntos suficientes
- ✅ Información clara de parques incluidos
- ✅ Condiciones de uso visibles (fechas bloqueadas, restricciones, etc.)

---

### PASO 6: RESUMEN DE RESERVA
**Pantalla:** Resumen de tickets Disney

**Información a mostrar:**
- Destino Disney
- Tipo de ticket (Base / Park Hopper / Park Hopper Plus)
- Número de días
- Fecha de inicio
- Número de visitantes (adultos/niños)
- Parques incluidos
- Puntos totales a canjear
- Dinero adicional (si modelo es mixto)
- Política de cancelación
- Términos y condiciones

**Validaciones:**
- ✅ Consistencia de datos
- ✅ Cálculo correcto de puntos
- ✅ Información completa de parques y acceso
- ✅ Fechas de validez claramente especificadas

---

### PASO 7: CHECKOUT - DATOS DE VISITANTES
**Pantalla:** Formulario de datos de visitantes

**Visitante principal (obligatorio):**
- Nombre(s) completo(s)
- Apellido(s) completo(s)
- Tipo de documento
- Número de documento
- Nacionalidad
- Fecha de nacimiento
- Email
- Teléfono
- País de residencia

**Visitantes adicionales:**
- Nombre completo
- Apellido completo
- Fecha de nacimiento (para validar categoría adulto/niño)
- Tipo de documento (puede ser opcional según proveedor)
- Número de documento (puede ser opcional según proveedor)

**Información adicional (opcional):**
- Necesidades especiales (accesibilidad, silla de ruedas, etc.)

**Acciones:**
1. Ingresar datos del visitante principal
2. Ingresar datos de visitantes adicionales
3. Agregar información de necesidades especiales (opcional)
4. Aceptar términos y condiciones de Disney
5. Aceptar política de tratamiento de datos
6. Hacer clic en "Continuar"

**Validaciones:**
- ✅ Datos del visitante principal completos
- ✅ Email válido
- ✅ Teléfono válido
- ✅ Fecha de nacimiento coherente con categoría (adulto/niño)
- ✅ Edad de niños dentro del rango permitido (3-9 años)
- ✅ Infantes (0-2 años) correctamente identificados (gratis)
- ✅ Términos aceptados obligatoriamente

---

### PASO 8: PAGO
[Ver proceso de pago según modelo en SANT_VUELOS.md]

---

### PASO 9: CONFIRMACIÓN DE RESERVA
**Pantalla:** Confirmación exitosa

**Información a mostrar:**
- Número de reserva
- Código de confirmación de Disney
- Resumen de los tickets:
  - Destino
  - Tipo de ticket
  - Número de días
  - Fecha de inicio
  - Visitantes
  - Parques incluidos
- Puntos debitados
- Estado: CONFIRMADA
- Instrucciones de canje:
  - Dónde canjear (taquillas, app, etc.)
  - Qué llevar (documento de identidad)
  - Horarios de los parques
- Voucher descargable con código QR/código de barras

**Validaciones:**
- ✅ Número de reserva único
- ✅ Código de confirmación válido del proveedor
- ✅ Email de confirmación enviado con voucher
- ✅ Puntos debitados correctamente
- ✅ Voucher con código QR/barras legible
- ✅ Instrucciones claras de canje
- ✅ Fechas de validez especificadas

---

### PASO 10: VALIDACIÓN EN ADMIN
**Acciones:**
1. Login en panel de admin
2. Buscar reserva por número
3. Verificar estado CONFIRMADA
4. Verificar todos los datos

**Validaciones:**
- ✅ Reserva existe en el sistema
- ✅ Proveedor correcto (DerbySoft/OffLine/Otro)
- ✅ Destino Disney correcto
- ✅ Tipo de ticket correcto
- ✅ Número de días correcto
- ✅ Fecha de inicio correcta
- ✅ Datos del visitante principal
- ✅ Número de visitantes (adultos/niños)
- ✅ Puntos debitados
- ✅ Código de confirmación Disney registrado

---

## 🎯 CASOS DE PRUEBA SUGERIDOS

### CASOS BÁSICOS:

1. **[SANT] Disney - 1 día - Base Ticket - [Proveedor] - 1 adulto**
2. **[SANT] Disney - 2 días - Base Ticket - [Proveedor] - 2 adultos**
3. **[SANT] Disney - 3 días - Park Hopper - [Proveedor] - 2 adultos + 1 niño**
4. **[SANT] Disney - 4 días - Park Hopper Plus - [Proveedor] - Familia (2+2)**
5. **[SANT] Disney - 5 días - Base Ticket - [Proveedor] - 1 adulto + 1 infante gratis**

### CASOS INTERMEDIOS:

6. **[SANT] Disney - 7 días - Park Hopper - Orlando - 4 adultos**
7. **[SANT] Disney - 3 días - Park Hopper Plus - California - 2 adultos**
8. **[SANT] Disney - 2 días - Base Ticket - Paris - 1 adulto + 2 niños**
9. **[SANT] Disney - 5 días - Park Hopper - Grupo grande (6 personas)**
10. **[SANT] Disney - 10 días - Park Hopper Plus - Estancia larga**

### CASOS AVANZADOS:

11. **[SANT] Disney - Visitante con necesidades especiales - Accesibilidad**
12. **[SANT] Disney - Cancelación y reembolso de puntos**
13. **[SANT] Disney - Modificación de fechas pre-visita**
14. **[SANT] Disney - Niño cumple años durante visita - Cambio de categoría**
15. **[SANT] Disney - Múltiples destinos Disney - Reservas separadas**

---

## 📋 INFORMACIÓN ADICIONAL

### CATEGORÍAS DE EDAD DISNEY:

- **Infantes:** 0-2 años (entrada gratuita)
- **Niños:** 3-9 años (precio reducido)
- **Adultos:** 10+ años (precio completo)

### TIPOS DE TICKETS:

**Base Ticket:**
- Acceso a 1 parque por día
- No permite cambiar de parque el mismo día
- Más económico

**Park Hopper:**
- Acceso a múltiples parques el mismo día
- Flexibilidad para visitar más de un parque por día
- Precio intermedio

**Park Hopper Plus:**
- Todo lo de Park Hopper
- Acceso a parques acuáticos (Blizzard Beach, Typhoon Lagoon)
- Acceso a campos de golf, ESPN Wide World of Sports
- Precio premium

### VALIDEZ DE TICKETS:

- **Uso:** Generalmente deben usarse en días consecutivos o dentro de una ventana de tiempo
- **Caducidad:** Típicamente válidos por 1 año desde la fecha de compra
- **Primera entrada:** Define el inicio del período de uso

---

## 📚 REFERENCIAS

📋 [SANTANDER_COMMON_RULES.md](../../../shared/Reglas Marketplace/SANTANDER_COMMON_RULES.md)  
📋 [SHARED_QA_RULES.md](../../../shared/SHARED_QA_RULES.md)  

---

**Versión:** 1.0.0  
**Fecha de creación:** 2026-01-23  
**Estado:** ⚠️ PENDIENTE COMPLETAR INFORMACIÓN TÉCNICA  
