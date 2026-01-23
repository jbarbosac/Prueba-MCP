# 🎢 SANTANDER - FLUJO E2E ACTIVIDADES

**Portal:** Santander  
**Producto:** Actividades  
**Prefijo:** [SANT]  
**Modelo:** B2B2C (Fidelity)  

---

## 📋 INFORMACIÓN GENERAL

### PROVEEDOR(ES):
**⚠️ PENDIENTE DEFINIR:**
- Proveedor principal: [HotelBeds / Viator / Otro]

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
2. Hacer clic en "Actividades" o "Tours y Actividades"

---

### PASO 3: BÚSQUEDA DE ACTIVIDADES
**Pantalla:** Formulario de búsqueda de actividades

**Campos obligatorios:**
- Destino (ciudad/región)
- Fecha de la actividad
- Número de participantes (adultos y niños)

**Campos opcionales:**
- Categoría de actividad (Tours, Aventura, Cultural, Gastronómica, etc.)
- Duración
- Rango de precio

**Acciones:**
1. Ingresar destino
2. Seleccionar fecha de la actividad
3. Seleccionar número de participantes (adultos/niños)
4. Aplicar filtros de categoría (opcional)
5. Hacer clic en "Buscar actividades"

**Validaciones:**
- ✅ Destino válido
- ✅ Fecha no puede ser anterior a hoy
- ✅ Al menos 1 participante seleccionado
- ✅ Edad de niños requerida si hay niños
- ✅ Botón deshabilitado hasta completar campos obligatorios

---

### PASO 4: DISPONIBILIDAD DE ACTIVIDADES
**Pantalla:** Resultados de búsqueda

**Información mostrada por actividad:**
- Nombre de la actividad
- Categoría (Tour, Aventura, Cultural, etc.)
- Duración aproximada
- Idioma(s) disponibles
- Descripción breve
- Calificación de usuarios
- Incluye (entradas, transporte, guía, comida, etc.)
- No incluye
- Restricciones (edad mínima, condición física, etc.)
- Punto de encuentro o recogida
- Horarios disponibles
- Política de cancelación
- Precio en puntos (o puntos + dinero) por persona

**Acciones:**
1. Revisar actividades disponibles
2. Aplicar filtros (si disponibles):
   - Categoría
   - Duración
   - Precio
   - Calificación
   - Idioma
3. Ver detalles de la actividad (fotos, itinerario completo)
4. Seleccionar actividad deseada
5. Hacer clic en "Continuar" o "Reservar"

**Validaciones:**
- ✅ Al menos un resultado disponible o mensaje apropiado
- ✅ Información completa de cada actividad
- ✅ Precio en puntos calculado por persona y total
- ✅ Verificación de puntos suficientes
- ✅ Fotos de la actividad cargadas
- ✅ Política de cancelación visible
- ✅ Restricciones claramente especificadas

---

### PASO 5: DETALLE DE LA ACTIVIDAD
**Pantalla:** Información completa de la actividad seleccionada

**Información a mostrar:**
- Galería de fotos
- Descripción completa
- Itinerario detallado
- Qué incluye / Qué no incluye
- Punto de encuentro con mapa
- Horarios de salida disponibles
- Duración total
- Idioma del guía
- Restricciones y recomendaciones
- Qué llevar (ropa cómoda, protector solar, etc.)
- Política de cancelación
- Reseñas de participantes anteriores

**Acciones:**
1. Revisar detalles completos
2. Seleccionar horario de salida (si hay opciones)
3. Confirmar número de participantes
4. Leer y comprender restricciones
5. Hacer clic en "Reservar"

**Validaciones:**
- ✅ Información coherente con búsqueda
- ✅ Disponibilidad confirmada para la fecha/horario
- ✅ Precio total claro (todos los participantes)
- ✅ Restricciones cumplidas (edad, condición física, etc.)

---

### PASO 6: RESUMEN DE RESERVA
**Pantalla:** Resumen de la actividad seleccionada

**Información a mostrar:**
- Nombre de la actividad
- Fecha y horario
- Duración
- Número de participantes (adultos/niños)
- Punto de encuentro/recogida
- Qué incluye
- Puntos totales a canjear
- Dinero adicional (si modelo es mixto)
- Política de cancelación
- Términos y condiciones

**Validaciones:**
- ✅ Consistencia de datos
- ✅ Cálculo correcto: puntos por persona × número de participantes
- ✅ Políticas claramente visibles
- ✅ Punto de encuentro claramente especificado

---

### PASO 7: CHECKOUT - DATOS DE PARTICIPANTES
**Pantalla:** Formulario de datos de participantes

**Participante principal (obligatorio):**
- Nombre(s) completo(s)
- Apellido(s) completo(s)
- Tipo de documento
- Número de documento
- Nacionalidad
- Fecha de nacimiento
- Email
- Teléfono
- País de residencia

**Participantes adicionales:**
- Nombre completo
- Edad (si es niño)
- Restricciones dietéticas (si la actividad incluye comida)
- Condiciones médicas relevantes (opcional pero recomendado)

**Información adicional:**
- Hotel de hospedaje (si la actividad incluye recogida)
- Solicitudes especiales

**Acciones:**
1. Ingresar datos del participante principal
2. Ingresar datos de participantes adicionales
3. Proporcionar información de hospedaje (si aplica)
4. Agregar solicitudes especiales (opcional)
5. Aceptar términos y condiciones de la actividad
6. Aceptar política de tratamiento de datos
7. Hacer clic en "Continuar"

**Validaciones:**
- ✅ Datos del participante principal completos
- ✅ Email válido
- ✅ Teléfono válido
- ✅ Edad de participantes coherente
- ✅ Restricciones de edad cumplidas
- ✅ Términos aceptados obligatoriamente

---

### PASO 8: PAGO
[Ver proceso de pago según modelo en SANT_VUELOS.md]

---

### PASO 9: CONFIRMACIÓN DE RESERVA
**Pantalla:** Confirmación exitosa

**Información a mostrar:**
- Número de reserva
- Código de confirmación del proveedor
- Resumen de la actividad:
  - Nombre
  - Fecha y horario
  - Duración
  - Participantes
  - Punto de encuentro/recogida
  - Datos de contacto del operador
- Puntos debitados
- Estado: CONFIRMADA
- Instrucciones previas a la actividad
- Qué llevar
- Voucher descargable

**Validaciones:**
- ✅ Número de reserva único
- ✅ Código de confirmación válido del proveedor
- ✅ Email de confirmación enviado
- ✅ Puntos debitados correctamente
- ✅ Voucher con todos los detalles
- ✅ Instrucciones claras de punto de encuentro

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
- ✅ Datos de la actividad (nombre, categoría, duración)
- ✅ Fecha y horario correctos
- ✅ Datos del participante principal
- ✅ Número de participantes
- ✅ Puntos debitados
- ✅ Punto de encuentro registrado

---

## 🎯 CASOS DE PRUEBA SUGERIDOS

### CASOS BÁSICOS:

1. **[SANT] Actividades - Tour ciudad - [Proveedor] - 1 adulto - Medio día**
2. **[SANT] Actividades - Tour gastronómico - [Proveedor] - 2 adultos**
3. **[SANT] Actividades - Aventura - [Proveedor] - 2 adultos + 1 niño**
4. **[SANT] Actividades - Cultural - [Proveedor] - Familia**
5. **[SANT] Actividades - Día completo - [Proveedor] - Grupo**

### CASOS INTERMEDIOS:

6. **[SANT] Actividades - Con recogida en hotel - [Proveedor]**
7. **[SANT] Actividades - Con comida incluida - [Proveedor]**
8. **[SANT] Actividades - Multiidioma - [Proveedor]**
9. **[SANT] Actividades - Aventura extrema - Restricción edad mínima**
10. **[SANT] Actividades - Tour privado - [Proveedor]**

### CASOS AVANZADOS:

11. **[SANT] Actividades - Cancelación gratuita - Reserva y cancelación**
12. **[SANT] Actividades - Modificación de fecha**
13. **[SANT] Actividades - Restricciones dietéticas - Menú especial**
14. **[SANT] Actividades - Accesibilidad - Silla de ruedas**
15. **[SANT] Actividades - Reembolso de puntos por mal tiempo**

---

## 📚 REFERENCIAS

📋 [SANTANDER_COMMON_RULES.md](../../../shared/Reglas Marketplace/SANTANDER_COMMON_RULES.md)  
📋 [SHARED_QA_RULES.md](../../../shared/SHARED_QA_RULES.md)  

---

**Versión:** 1.0.0  
**Fecha de creación:** 2026-01-23  
**Estado:** ⚠️ PENDIENTE COMPLETAR INFORMACIÓN TÉCNICA  
