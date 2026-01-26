# 🎢 PRODUCTO: ACTIVIDADES - PROMERICA REWARDS

> **📖 Información Global:** Ver [PROM_QA_Assistant.agent.md](../../../../agents/PROM_QA_Assistant.agent.md) para URL del portal, país activo, modelo de negocio y versión del marketplace.

---

## 📌 Descripción General

Producto de Actividades en el marketplace Promerica Rewards que permite a usuarios canjear puntos o combinación Puntos + Plata para reservar experiencias, tours, excursiones y actividades turísticas a nivel internacional.

**Características principales:**
1. **Búsqueda flexible:** Destino, rango de fechas, y configuración de visitantes con edades
2. **Catálogo amplio:** Actividades de HotelBeds con múltiples categorías (tours, excursiones, entradas, experiencias)
3. **Modelo de pago:** Puntos + Plata con slider ajustable
4. **Filtrado avanzado:** Categorías, precio, duración, calificación
5. **Información detallada:** Descripciones, itinerarios, qué incluye/no incluye, políticas de cancelación
6. **Reserva en línea:** Proceso completo desde selección hasta voucher descargable

---

## 📦 CONTEXTO OPERATIVO

### Proveedores Disponibles

**Proveedor confirmado:**

- **HotelBeds** (proveedor principal para actividades)

⚠️ **Pendiente validar:** Si existen proveedores adicionales o alternativas

### Componentes Transversales

> **Nota:** Estos componentes son compartidos por todos los productos del marketplace (Vuelos, Autos, Hoteles, Disney, **Actividades**). Ver detalle completo en [PROM_VUELOS.md](PROM_VUELOS.md#-componentes-transversales).

#### Header Global

Barra superior con navegación principal, branding personalizado de Promerica y acceso de usuario.

#### Tabs de Productos

Pestañas horizontales para navegación entre productos (Vuelos, Autos, Hoteles, Disney, **Actividades**).

#### Footer Global

Sección inferior con información institucional y canales de contacto personalizados por país.

### Flujo E2E Obligatorio

**Siempre incluir estos pasos desde login para el flujo completo de Actividades:**

1. **Acceder al portal** → https://traveltest-club-promerica.preprodppm.com/es-cr | El portal carga correctamente y muestra la pantalla de inicio
2. **Realizar login** → Ingresar usuario y contraseña válidos | Login exitoso y acceso al home con tabs de productos visibles
3. **Navegar a Actividades** → Clic en tab "Actividades" | Widget de búsqueda de actividades se muestra correctamente
4. **Seleccionar destino** → Clic en campo "Destino" o "¿A dónde quieres ir?" | Modal de búsqueda de destinos se abre
5. **Buscar y seleccionar ciudad** → Escribir ciudad/país en buscador | Sistema filtra resultados y muestra lista de destinos
6. **Confirmar destino** → Clic en ciudad deseada de la lista | Modal se cierra y campo "Destino" se actualiza con selección
7. **Seleccionar fechas** → Clic en campo "Selecciona tus fechas" | Calendario mensual se abre
8. **Confirmar rango de fechas** → Seleccionar fecha inicio y fecha fin | Calendario se cierra y campo muestra el rango seleccionado
9. **Configurar visitantes** → Clic en campo "Visitantes" | Dropdown/modal de visitantes se abre
10. **Ajustar cantidad** → Seleccionar cantidad de pasajeros con botones +/- | Sistema muestra dropdowns de edad por cada pasajero
11. **Confirmar visitantes** → Clic en "Aceptar" o fuera del modal | Modal se cierra y campo muestra resumen (ej: "2 pasajeros")
12. **Ejecutar búsqueda** → Clic en botón "Buscar" verde | Sistema redirige a módulo de Disponibilidad con resultados
13. **Revisar widget de búsqueda persistente** → Verificar resumen de criterios en parte superior | Widget compacto muestra destino, fechas y visitantes
14. **Navegar por lista de actividades** → Scroll por resultados | Cards de actividades se muestran con información básica
15. **Aplicar filtros laterales** → Seleccionar categoría, precio, duración | Resultados se actualizan dinámicamente
16. **Ver detalle de actividad** → Clic en card o botón "Ver más" | ⚠️ Pendiente documentar: ¿Abre modal de detalle o redirige a nueva página?
17. **Revisar descripción completa** → ⚠️ Pendiente documentar contenido de detalle | ⚠️ Pendiente documentar secciones disponibles
18. **Ajustar slider Puntos + Plata** → ⚠️ Pendiente documentar ubicación del slider | ⚠️ Pendiente documentar validación de saldo
19. **Seleccionar fecha/horario específico** → ⚠️ Pendiente documentar opciones de calendario/horarios | ⚠️ Pendiente documentar disponibilidad por fecha
20. **Continuar a Checkout** → Clic en botón de confirmación | ⚠️ Pendiente documentar validaciones de checkout
21. **Completar datos de participantes** → Llenar formulario con información de cada participante | ⚠️ Pendiente documentar campos específicos
22. **Agregar solicitudes especiales (opcional)** → ⚠️ Pendiente documentar opciones disponibles | ⚠️ Pendiente documentar tipos de solicitud
23. **Seleccionar método de pago** → Ingresar datos de tarjeta si hay copago en plata | ⚠️ Pendiente documentar proceso de pago
24. **Confirmar reserva** → Clic en botón de confirmación final | ⚠️ Pendiente documentar proceso de emisión
25. **Validar confirmación** → Verificar código de reserva, voucher | ⚠️ Pendiente documentar datos mostrados
26. **Verificar en Admin** → Buscar reserva en aplicativo Admin | ⚠️ Pendiente documentar validaciones de backend

**Nota:** Los pasos 16-26 están pendientes de documentación completa según información de módulos Detalle, Checkout, Confirmación y Admin.

---

## 🏠 MÓDULO: HOME/LOGIN

### 📋 Descripción del Módulo

Página principal del marketplace donde el usuario accede al buscador de actividades y navega entre productos disponibles. La interfaz es personalizable según el país configurado (Costa Rica en Test).

### 🎨 FUNCIONALIDADES

#### 🔹 Funcionalidad: Widget de Búsqueda de Actividades

##### 📖 Descripción Funcional

Formulario principal para búsqueda de actividades con selectores de destino, rango de fechas y visitantes. Permite configurar criterios básicos antes de buscar experiencias y tours disponibles.

**Ubicación:** Centro de la página de inicio, debajo del header y tabs de productos  
**Tipo de componente:** Formulario interactivo con modal de destinos y calendario  
**Acceso:** Disponible para todos los usuarios autenticados

##### 🧩 Componentes

1. **Selector "Destino":**
   - Campo con ícono de ubicación
   - Placeholder: "¿A dónde quieres ir?"
   - Clic abre modal de búsqueda de destinos
   - Campo obligatorio

2. **Selector "Selecciona tus fechas":**
   - Campo con ícono de calendario
  - Placeholder: "Selecciona tus fechas"
  - Clic abre calendario mensual (rango inicio/fin)
   - Campo obligatorio

3. **Dropdown "Visitantes":**
   - Campo con ícono de personas
  - Placeholder: "Visitantes"
  - Valor por defecto: "1 adulto"
  - Clic abre modal de visitantes con controles +/-
  - Muestra resumen dinámico (ej: "1 adulto", "2 pasajeros")
   - Campo obligatorio

4. **Botón "Buscar":**
   - Color: Verde institucional (#00563F)
   - Texto: "Buscar" en blanco, centrado
   - Estado deshabilitado (gris) si faltan campos obligatorios
   - Habilitado (verde) cuando todos los campos están completos

##### 💻 Comportamiento Esperado

**Interacción con selector de destino (Modal de búsqueda):**
- Clic en campo "Destino" abre modal emergente "¿A dónde quieres ir?"
- **Componentes del modal:**
  - Título: "¿A dónde quieres ir?" o "Buscar destino"
  - Botón Cerrar (X) en esquina superior derecha
  - Campo de búsqueda con ícono de lupa, placeholder: "Ciudad o país"
  - Lista scrollable de resultados con formato: "Nombre Ciudad | País"
    - Ejemplo: "San José | Costa Rica"
  - Sugerencias populares (opcional) cuando el campo está vacío
  - Mensaje de estado vacío: "No se encontraron resultados" / "Intenta con otro destino"
- **Comportamiento de búsqueda:**
  - Usuario escribe destino → Sistema filtra en tiempo real (< 1 seg)
  - Resultados encontrados → Muestra lista de ciudades coincidentes
  - Sin resultados → Muestra mensaje de estado vacío
  - Clic en destino de la lista → Cierra modal y actualiza campo "Destino" con selección
  - Botón X o clic fuera del modal → Cierra sin aplicar cambios

**Interacción con selector de fecha (Calendario):**
- Clic en campo "Selecciona tus fechas" abre calendario interactivo (selección de rango)
- **Componentes del calendario:**
  - Navegación de mes/año: Flechas < > para cambiar mes
  - Selector de mes y año en encabezado
  - Vista desktop (según UI): Calendario dual (dos meses lado a lado)
  - Grilla de días: Días de la semana (L, M, M, J, V, S, D)
  - Indicadores visuales:
    - Día actual destacado
    - Fechas pasadas deshabilitadas (gris)
    - Fecha inicio seleccionada (verde)
    - Rango seleccionado (verde claro)
    - Fecha fin seleccionada (verde)
  - Botones de acción: "Cancelar" (cierra sin cambios) y "Aceptar" (verde, confirma selección)
- **Comportamiento de selección:**
  - Primer clic selecciona fecha inicio
  - Segundo clic selecciona fecha fin (debe ser posterior)
  - No permite fechas pasadas
  - Botón "Cancelar" cierra calendario sin aplicar cambios
  - Botón "Aceptar" actualiza el campo principal con el rango y cierra calendario

**Interacción con selector de participantes (Dropdown):**
- Clic en campo "Visitantes" abre modal con control de cantidad y edades
- **Controles de visitantes:**
  - **Sección Pasajeros:**
    - Label: "Pasajeros"
    - Contador numérico con botones - / +
    - Validación: mínimo 1 pasajero
  - **Dropdowns condicionales "Edad del pasajero":**
    - Aparecen dinámicamente según cantidad de pasajeros
    - Label: "Edad del pasajero 1", "Edad del pasajero 2", etc.
    - Placeholder: "Selecciona la edad"
    - Obligatorio seleccionar edad para cada pasajero
  - **Botones de acción del modal:**
    - "Cancelar": descarta cambios y cierra modal sin aplicar
    - "Aceptar": guarda configuración, actualiza texto del dropdown y cierra modal
- **Comportamiento:**
  - Botones +/- ajustan cantidad
  - Al aumentar pasajeros, aparecen dropdowns de edad adicionales
  - Al disminuir pasajeros, se eliminan dropdowns de edad correspondientes
  - Al cerrar, el campo principal actualiza su resumen (ej: "1 adulto", "2 pasajeros")

**Validaciones del sistema:**
- **Todos los campos son obligatorios** antes de poder buscar
- **Destino:** Debe seleccionar ciudad/país de la lista del modal
- **Fechas:** No permite fechas pasadas, fecha inicio debe ser anterior a fecha fin
- **Visitantes:** Mínimo 1 pasajero y edades obligatorias para cada pasajero
- **Botón "Buscar":**
  - Deshabilitado (gris) si faltan campos obligatorios
  - Habilitado (verde) cuando todos los campos están completos
- Al hacer clic en "Buscar" → Redirige a módulo Disponibilidad con resultados filtrados según destino, fecha y participantes

**Variaciones móviles:**
- **Layout:** Campos apilados verticalmente, cada campo ocupa ancho completo
- **Modal de destino:** Pantalla completa con buscador
- **Calendario:** Vista en pantalla completa con navegación táctil optimizada
- **Dropdown participantes:** Modal de pantalla completa con controles +/- grandes y áreas táctiles amplias
- **Botón "Buscar":** Sticky en la parte inferior, siempre visible durante scroll

##### ✅ VALIDACIONES DE QA

Estas validaciones deben incluirse en todos los casos de prueba que involucren el Widget de Búsqueda:

- [ ] **VAL-ACT-HOME-001:** Todos los campos son obligatorios
  - **Verificar:** Botón "Buscar" deshabilitado (gris) si falta algún campo, habilitado (verde) solo con todos completos
  
- [ ] **VAL-ACT-HOME-002:** Modal de destinos abre correctamente
  - **Verificar:** Clic en campo "Destino" abre modal con buscador funcional
  
- [ ] **VAL-ACT-HOME-003:** Búsqueda de destinos filtra en tiempo real
  - **Verificar:** Al escribir ciudad, resultados se filtran (< 1 seg)
  
- [ ] **VAL-ACT-HOME-004:** Selección de destino actualiza campo
  - **Verificar:** Clic en resultado cierra modal y actualiza campo "Destino" correctamente
  
- [ ] **VAL-ACT-HOME-005:** Calendario no permite fechas pasadas
  - **Verificar:** Fechas anteriores a hoy están deshabilitadas (gris) y no seleccionables
  
- [ ] **VAL-ACT-HOME-006:** Calendario valida rango de fechas
  - **Verificar:** Permite seleccionar rango inicio/fin; inicio/fin resaltados (verde) y rango (verde claro)
  
- [ ] **VAL-ACT-HOME-007:** Dropdown participantes valida límites
  - **Verificar:** Mínimo 1 pasajero; dropdowns de edad aparecen por pasajero; edades obligatorias
  
- [ ] **VAL-ACT-HOME-008:** Resumen de participantes correcto
  - **Verificar:** Campo muestra resumen dinámico (ej: "1 adulto", "2 pasajeros") actualizado correctamente
  
- [ ] **VAL-ACT-HOME-009:** Botón "Buscar" redirige a Disponibilidad
  - **Verificar:** Clic en "Buscar" redirige a módulo Disponibilidad con resultados según criterios
  
- [ ] **VAL-ACT-HOME-010:** Variaciones móviles
  - **Verificar:** Layout apilado vertical, modal/calendario/dropdown en pantalla completa, botón sticky en móviles

##### 🧪 Escenarios de Prueba

**Escenario 1: Búsqueda exitosa de actividades - San José - 2 adultos**
- **Prioridad:** 1 (Crítico)
- **Modelo de pago:** Puntos + Plata
- **Precondición:** Usuario autenticado en home Actividades
- **Pasos:**
  1. Clic en campo "Destino"
  2. Modal se abre, escribir "San José"
  3. Seleccionar "San José | Costa Rica" de la lista
  4. **Validar:** Campo "Destino" actualiza a "San José, Costa Rica"
  5. Clic en campo "Fecha"
  6. Calendario se abre, seleccionar fecha 7 días adelante
  7. Clic en "Aceptar"
  8. **Validar:** Campo "Fecha" muestra fecha seleccionada
  9. Clic en campo "Participantes"
  10. Dropdown se abre, configurar "2 adultos" con botón +
  11. Clic en "Listo"
  12. **Validar:** Campo muestra "2 adultos"
  13. **Validar:** Botón "Buscar" habilitado (verde)
  14. Clic en "Buscar"
  15. **Validar:** Redirige a Disponibilidad con resultados
- **Resultado esperado:** Búsqueda exitosa, resultados de actividades en San José para 2 adultos
- **Resultado esperado:** Búsqueda exitosa, resultados de actividades en San José con criterios seleccionados
- **Título ADO:** `[PROM] Actividades - Home - Búsqueda exitosa - San José - 2 pasajeros - Puntos + Plata`

**Escenario 2: Validación de campos obligatorios**
- **Prioridad:** 1 (Crítico)
- **Precondición:** Usuario autenticado en home Actividades
- **Pasos:**
  1. **NO** llenar campo "Destino"
  2. **Validar:** Botón "Buscar" deshabilitado (gris)
  3. Seleccionar destino "San José, Costa Rica"
  4. **Validar:** Botón "Buscar" sigue deshabilitado (falta fecha)
  5. Seleccionar rango de fechas
  6. **Validar:** Botón "Buscar" sigue deshabilitado (faltan visitantes)
  7. Configurar "1 pasajero" y seleccionar su edad
  8. **Validar:** Botón "Buscar" ahora habilitado (verde)
- **Resultado esperado:** Sistema valida campos obligatorios correctamente
- **Título ADO:** `[PROM] Actividades - Home - Validación campos obligatorios - San José`

**Escenario 3: Validación de fechas pasadas en calendario**
- **Prioridad:** 2 (Importante)
- **Precondición:** Usuario en home Actividades
- **Pasos:**
  1. Clic en campo "Selecciona tus fechas"
  2. Calendario se abre
  3. Intentar seleccionar fecha pasada (ej: día anterior)
- **Resultado esperado:** Fechas pasadas deshabilitadas (gris), no permite selección
- **Título ADO:** `[PROM] Actividades - Home - Calendario bloquea fechas pasadas`

**Escenario 4: Búsqueda modal de destinos - sin resultados**
- **Prioridad:** 2 (Importante)
- **Precondición:** Usuario en home Actividades
- **Pasos:**
  1. Clic en campo "Destino"
  2. Modal se abre
  3. Escribir texto sin coincidencias (ej: "XYZABC123")
  4. **Validar:** Mensaje "No se encontraron resultados" o similar
  5. **Validar:** Lista de destinos vacía
- **Resultado esperado:** Sistema muestra mensaje claro cuando no hay resultados
- **Título ADO:** `[PROM] Actividades - Home - Modal destinos sin resultados`

**Escenario 5: Dropdown participantes - límites mínimos/máximos**
- **Prioridad:** 2 (Importante)
- **Precondición:** Usuario en home Actividades
- **Pasos:**
  1. Clic en campo "Visitantes"
  2. Modal se abre
  3. Intentar reducir pasajeros a 0 con botón -
  4. **Validar:** Botón - deshabilitado, mínimo 1 pasajero
  5. Aumentar a 2 pasajeros con botón +
  6. **Validar:** Aparecen "Edad del pasajero 1" y "Edad del pasajero 2"
  7. Seleccionar edades para ambos pasajeros
  8. Clic en "Aceptar"
  9. **Validar:** Campo muestra resumen (ej: "2 pasajeros")
- **Resultado esperado:** Sistema respeta límites mínimos y exige edades por pasajero
- **Título ADO:** `[PROM] Actividades - Home - Visitantes límites y edades obligatorias`

---

## 📋 MÓDULO: DISPONIBILIDAD

### Descripción del Módulo

Módulo que muestra los resultados de búsqueda de actividades disponibles según los criterios del usuario (destino, fechas, visitantes). Permite filtrar y comparar opciones de tours, excursiones y experiencias turísticas del proveedor HotelBeds.

**Características principales:**
- Widget de búsqueda persistente para modificar criterios
- Filtros laterales por categoría, precio, duración, calificación
- Cards de actividades con información básica y botón de acción
- Paginación o scroll infinito según cantidad de resultados

### 🎨 FUNCIONALIDADES

#### 🔹 Funcionalidad: Widget de Búsqueda Persistente

##### 📖 Descripción Funcional

Resumen compacto de criterios de búsqueda que permanece visible en la parte superior del módulo de disponibilidad. Permite al usuario modificar destino, fecha o participantes sin perder su posición en los resultados.

**Ubicación:** Parte superior del módulo Disponibilidad, debajo del header  
**Tipo de componente:** Barra informativa con campos editables  
**Persistencia:** Visible durante toda la navegación en Disponibilidad

##### 🧩 Componentes

| Componente | Descripción | Tipo | Editable |
|------------|-------------|------|----------|
| **Campo "Destino"** | Muestra destino seleccionado (ej: "San José, Costa Rica") | Text/Link | ✅ Clic abre modal de destinos |
| **Campo "Fechas"** | Muestra rango con formato corto | Text/Link | ✅ Clic abre calendario |
| **Campo "Visitantes"** | Muestra resumen (ej: "2 pasajeros") | Text/Link | ✅ Clic abre modal de configuración |
| **Botón "Buscar"** | Ejecuta nueva búsqueda con criterios modificados | Button (CTA verde) | ✅ Actualiza resultados |
| **Link "Ocultar búsqueda"** | Colapsa widget para dar más espacio a resultados | Text Link | ✅ Alterna visibilidad |

##### 💻 Comportamiento Esperado

**Widget persistente:**
- Permanece visible mientras el usuario navega por los resultados (sticky)
- Scroll en resultados no oculta el widget
- Usuario mantiene contexto de su búsqueda en todo momento

**Edición de criterios:**
- Clic en campo "Destino" → Abre modal de búsqueda de destinos con valor precargado
- Clic en campo "Fechas" → Abre calendario con selección actual
- Clic en campo "Visitantes" → Abre modal con configuración actual y edades
- Modificar cualquier campo no ejecuta búsqueda automáticamente, requiere clic en "Buscar"

**Botón "Buscar":**
- Habilitado siempre (criterios ya validados en HOME)
- Clic ejecuta nueva búsqueda con criterios modificados
- Muestra indicador de carga (spinner/skeleton) durante búsqueda
- Actualiza resultados sin recargar página completa
- Scroll automático a inicio de resultados tras actualización

**Ocultar/Mostrar widget:**
- Link "Ocultar búsqueda" colapsa widget a barra mínima con solo destino visible
- Link "Mostrar búsqueda" expande widget completo
- Estado de colapso se mantiene durante navegación en resultados

**Variaciones móviles:**
- Widget colapsado por defecto: Barra compacta con resumen "Destino • Fecha • X participantes"
- Tap en widget expande en modal de pantalla completa para editar
- Campos abren modales/calendarios/dropdowns fullscreen
- Botón "Buscar" sticky en parte inferior del modal
- Botón "Cerrar" (X) en esquina superior para salir sin cambios

##### ✅ VALIDACIONES DE QA

- [ ] **VAL-ACT-DISP-001:** Widget visible en todo momento
  - **Verificar:** Widget persistente en parte superior, no desaparece al hacer scroll
  
- [ ] **VAL-ACT-DISP-002:** Campos editables funcionan correctamente
  - **Verificar:** Clic en cada campo abre control correspondiente con valor actual precargado
  
- [ ] **VAL-ACT-DISP-003:** Modificaciones se reflejan correctamente
  - **Verificar:** Cambios en campos se muestran en widget antes de buscar
  
- [ ] **VAL-ACT-DISP-004:** Botón "Buscar" actualiza resultados
  - **Verificar:** Nueva búsqueda ejecuta, resultados se actualizan sin recargar página
  
- [ ] **VAL-ACT-DISP-005:** Indicador de carga visible
  - **Verificar:** Spinner/skeleton aparece durante búsqueda, desaparece al cargar resultados
  
- [ ] **VAL-ACT-DISP-006:** Link "Ocultar/Mostrar" funciona
  - **Verificar:** Colapsa y expande widget correctamente, estado se mantiene
  
- [ ] **VAL-ACT-DISP-007:** Variaciones móviles
  - **Verificar:** Widget colapsado por defecto en móviles, expansión en modal fullscreen

##### 🧪 Escenarios de Prueba

**Escenario 1: Modificar fechas desde widget persistente**
- **Prioridad:** 1 (Crítico)
- **Precondición:** Usuario en Disponibilidad con resultados cargados (destino X, rango de fechas X-Y, visitantes configurados)
- **Pasos:**
  1. Localizar widget de búsqueda persistente en parte superior
  2. Clic en campo "Fechas"
  3. Calendario se abre con rango actual seleccionado
  4. Seleccionar un nuevo rango de fechas
  5. Clic en "Aceptar"
  6. **Validar:** Campo "Fechas" actualiza el rango
  7. Clic en botón "Buscar"
  8. **Validar:** Spinner/skeleton aparece
  9. **Validar:** Resultados se actualizan con actividades para el nuevo rango
  10. **Validar:** Widget mantiene criterios actualizados
- **Resultado esperado:** Nueva búsqueda con fecha actualizada, resultados sin recargar página
- **Título ADO:** `[PROM] Actividades - Disponibilidad - Modificar fechas desde widget`

**Escenario 2: Ocultar y mostrar widget de búsqueda**
- **Prioridad:** 2 (Importante)
- **Precondición:** Usuario en Disponibilidad con resultados
- **Pasos:**
  1. Localizar link "Ocultar búsqueda"
  2. Clic en "Ocultar búsqueda"
  3. **Validar:** Widget se colapsa a barra mínima
  4. Scroll hacia abajo en resultados
  5. **Validar:** Barra mínima sigue visible (sticky)
  6. Clic en barra mínima o link "Mostrar búsqueda"
  7. **Validar:** Widget se expande mostrando todos los campos
- **Resultado esperado:** Widget colapsa/expande correctamente, estado sticky se mantiene
- **Título ADO:** `[PROM] Actividades - Disponibilidad - Ocultar mostrar widget`

---

#### 🔹 Funcionalidad: Filtros Laterales

##### 📖 Descripción Funcional
Panel lateral con controles para refinar los resultados de actividades por atributos como categoría, precio, duración, calificación, cancelación e inclusiones.

**Ubicación:** Panel lateral izquierdo en desktop; drawer/modal en móvil  
**Actualización:** Dinámica (sin recarga de página)

##### 🧩 Componentes

| Componente | Descripción | Tipo | Notas |
|------------|-------------|------|------|
| **Filtro: Categoría/Tipo** | Tour, excursión, entrada, experiencia, aventura, etc. | Multi-checkbox | ⚠️ Pendiente confirmar opciones disponibles |
| **Filtro: Precio** | Rango min-max en Puntos o Plata | Range Slider | Formato según configuración |
| **Filtro: Duración** | Menos de 4 horas, 4-8 horas, más de 8 horas, varios días | Multi-checkbox | ⚠️ Pendiente confirmar opciones disponibles |
| **Filtro: Calificación** | Rating mínimo (estrellas/puntaje) | Checkbox/Slider | ⚠️ Pendiente confirmar si está disponible |
| **Filtro: Horario/Momento del día** | Mañana, tarde, noche | Multi-checkbox | ⚠️ Pendiente confirmar si está disponible |
| **Filtro: Incluye** | Transporte, comida, guía, entradas, equipo, etc. | Multi-checkbox | ⚠️ Pendiente confirmar servicios disponibles |
| **Filtro: Cancelación** | Cancelación gratuita, reembolsable parcialmente, no reembolsable | Multi-checkbox | ⚠️ Pendiente confirmar opciones disponibles |
| **Limpiar filtros** | Resetear todos los filtros aplicados | Button/Link | Restaura estado inicial |

##### 💻 Comportamiento Esperado

- **Aplicación acumulativa:**
  - Dentro de una misma categoría: OR lógico
  - Entre categorías diferentes: AND lógico
- **Actualización en tiempo real:** Resultados se actualizan al aplicar filtros
- **Slider de precio:** Ajuste dinámico del rango y actualización al soltar (o con delay)
- **Limpiar filtros:** Remueve filtros activos y restaura resultados
- **Persistencia:** Filtros se mantienen al navegar a detalle y regresar (según comportamiento del portal)

**Variaciones móviles:**
- Botón flotante "Filtros" con badge de filtros activos
- Panel como modal/bottom sheet con secciones expandibles
- Botones de acción "Limpiar" y "Aplicar" en parte inferior
- Cerrar modal con swipe o tap en overlay

##### ✅ VALIDACIONES DE QA

- [ ] **VAL-ACT-FIL-001:** Aplicación de filtros actualiza resultados
  - **Verificar:** Al seleccionar un filtro, la lista se actualiza sin recargar página
- [ ] **VAL-ACT-FIL-002:** Limpiar filtros restaura estado
  - **Verificar:** "Limpiar filtros" remueve filtros activos y restablece resultados

##### 🧪 Escenarios de Prueba

[PENDIENTE: Agregar escenarios específicos de filtros]

---

#### 🔹 Funcionalidad: Cards de Actividades (Vista Lista)

##### 📖 Descripción Funcional

Listado de tarjetas individuales que muestran información resumida de cada actividad. Cada card permite acceder al detalle para revisar descripción completa, inclusiones, políticas y seleccionar la opción.

##### 🧩 Componentes

1. **Imagen de la actividad:**
   - Foto principal de la actividad en alta resolución
   - Posibilidad de galería (indicador "1/8" si hay múltiples fotos)

2. **Nombre de la actividad:**
   - Título destacado (negrita)
   - Ejemplo: "City Tour por San José - Día Completo"

3. **Categoría/Tipo:**
   - Badge o etiqueta: "Tour" | "Experiencia" | "Aventura" | etc.
   - Color distintivo por categoría

4. **Duración:**
   - Ícono de reloj ⏱️
   - Texto: "8 horas" | "Día completo" | "4-6 horas"

5. **Ubicación:**
   - Ícono de ubicación 📍
   - Texto: Ciudad principal de la actividad

6. **Calificación de participantes:**
   - Puntaje: 4.5/5 ⭐
   - Número de reseñas: "(89 opiniones)"
   - ⚠️ Pendiente confirmar si está disponible

7. **Incluye (destacados):**
   - Íconos con servicios: 🚌 Transporte, 🍽️ Comida, 👨‍🏫 Guía, 🎟️ Entradas
   - Máximo 4-5 íconos visibles

8. **Precio:**
   - Label: "Desde" (pequeño)
   - Precio por persona en Puntos o Plata
   - Ejemplo: "8,500 puntos/persona" o "USD $75/persona"
   - Nota: "Precio total para X participantes: XXX"

9. **Disponibilidad:**
   - Badge verde: "Disponible"
   - Badge amarillo: "Últimos lugares"
   - Badge rojo: "Agotado"
   - ⚠️ Pendiente confirmar indicadores

10. **Política de cancelación:**
    - Badge verde: "Cancelación gratuita hasta X horas antes"
    - Badge rojo: "No reembolsable"

11. **Botón de acción:**
    - Botón "Ver más" o "Ver detalles" (verde)
    - Clic redirige a detalle de la actividad

**Diseño Visual:**

- Card con borde gris claro y sombra suave
- Layout: Imagen izquierda | Información centro | Precio y botón derecha
- Espaciado uniforme entre elementos
- Íconos en color gris/verde con estilo minimalista

**Comportamiento esperado:**

- **Hover en card:** Sombra más pronunciada o borde destacado
- **Clic en imagen:** ⚠️ Pendiente definir: ¿Abre galería de fotos?
- **Clic en card completo:** ⚠️ Pendiente definir: ¿Abre modal de detalle o redirige a página?
- **Clic en botón "Ver más":** Navega a vista de detalle con descripción completa
- **Scroll:** Carga lazy de cards adicionales conforme usuario navega

##### ✅ VALIDACIONES DE QA

[PENDIENTE: Agregar validaciones específicas de cards de actividades]

##### 🧪 Escenarios de Prueba

[PENDIENTE: Agregar escenarios específicos de cards de actividades]

**Variaciones Móviles:**

- **Cards apiladas verticalmente:** Ocupan ancho completo
- **Layout reorganizado:** Imagen arriba, información abajo
- **Precio más prominente:** En parte superior o inferior destacada
- **Botón "Ver más":** Ocupa ancho completo en parte inferior del card
- **Touch targets:** Áreas de toque optimizadas para móvil
- **Galería de imágenes:** Swipe horizontal en imagen principal

---

## 💳 MÓDULO: CHECKOUT

> ⚠️ **Documentación en proceso**  
> Este módulo está siendo estandarizado. Se está trabajando en la documentación de: Datos de participantes, Contacto, Métodos de pago, Resumen de reserva, Solicitudes especiales.  
> **Estado:** 🔄 Pendiente de completar

---

## ✅ MÓDULO: CONFIRMACIÓN

> ⚠️ **Documentación en proceso**  
> Este módulo está siendo estandarizado. Se está trabajando en la documentación de: Confirmación exitosa, Número de reserva, Voucher descargable, Error en procesamiento.  
> **Estado:** 🔄 Pendiente de completar

---

## ✅ VALIDACIONES CRÍTICAS

> **Nota:** Estas validaciones complementan los "Pasos Obligatorios del Flujo E2E". No duplican los pasos, sino que detallan las validaciones específicas a verificar en cada punto.

### Validaciones por Módulo:

**Home/Login:**
✅ Campos obligatorios: Destino, fecha, participantes  
✅ Participantes: Mínimo 1 participante (típicamente 1 adulto)  
✅ Botón buscar: Habilitado solo con campos completos  
✅ Fecha: No permite selección de fechas pasadas  
✅ Modal de destinos: Búsqueda en tiempo real, lista de resultados  
✅ Calendario: Navegación mes/año, fecha seleccionada visible  
✅ Dropdown participantes: Controles +/- funcionales, rangos validados

**Disponibilidad:**
✅ Widget persistente: Resumen correcto de criterios de búsqueda  
✅ Filtros laterales: Actualización en tiempo real sin recargar  
✅ Cards de actividades: Información completa (nombre, categoría, duración, precio, incluye)  
✅ Carga lazy: Resultados adicionales al hacer scroll  
✅ Ordenamiento: ⚠️ Pendiente documentar opciones de orden (precio, popularidad, duración)

**Detalle de Actividad:**
⚠️ Pendiente documentar: Descripción completa, itinerario, qué incluye/no incluye, punto de encuentro, horarios disponibles

**Checkout:**
⚠️ Pendiente documentar: Datos de cada participante, contacto, métodos de pago

**Confirmación:**
⚠️ Pendiente documentar: Código de reserva, voucher, manejo de errores

**Admin:**
⚠️ Pendiente documentar: Reserva localizable, estados de procesamiento

### Validaciones Específicas del Modelo Slider (Puntos + Plata):

⚠️ **PENDIENTE CONFIRMAR:** ¿El slider aparece en disponibilidad, detalle o checkout?  
⚠️ **PENDIENTE CONFIRMAR:** ¿Ubicación exacta del slider?  
⚠️ **PENDIENTE CONFIRMAR:** Porcentaje mínimo de puntos requerido  
✅ **Validación de saldo:** Sistema debe verificar puntos disponibles  
✅ **Solicitud de pago:** Si hay copago en plata, se requiere método de pago  
⚠️ **PENDIENTE CONFIRMAR:** Tipo de emisión (automática/manual)  
⚠️ **PENDIENTE CONFIRMAR:** ¿Precio por persona o grupo? ¿Slider ajusta por persona o total?

### Validaciones de Experiencia de Usuario (UI/UX):

✅ **Modal de destinos:** Experiencia fluida de búsqueda y selección  
✅ **Calendario:** Navegación intuitiva, fecha visible claramente  
✅ **Dropdown participantes:** Controles +/- funcionales, límites validados  
✅ **Responsive:** Adaptación correcta a móviles (sticky buttons, modals fullscreen)  
✅ **Estados de carga:** Indicadores visuales durante búsqueda/filtrado  
✅ **Mensajes de error:** Claros y orientados a acción del usuario  
✅ **Accesibilidad:** Componentes navegables por teclado y lectores de pantalla

---

## 📝 FORMATO DE TÍTULO

```
[PROM] Actividades - [Módulo/Escenario] - [Variante]
```

**Ejemplos actualizados:**

- `[PROM] Actividades - Home - Búsqueda - San José - 2 pasajeros - Puntos + Plata`
- `[PROM] Actividades - Disponibilidad - Filtros - Duración + Cancelación - Puntos + Plata`
- `[PROM] Actividades - Disponibilidad - Selección de card - Actividad X - Solo Puntos`

---

## 🚀 PRÓXIMOS PASOS PARA COMPLETAR ESTE ARCHIVO

### Módulos Documentados:

✅ **Componentes Transversales** - Referencia a vuelos (Header, Tabs, Footer)  
✅ **Pasos Obligatorios del Flujo E2E** - 26 pasos documentados (pasos 1-15 completos, 16-26 pendientes)  
✅ **Módulo Home/Login** - Widget de búsqueda con 4 componentes + Modal destinos + Calendario + Dropdown participantes  
✅ **Módulo Disponibilidad** - 3 funcionalidades: Widget persistente, Filtros laterales, Cards de actividades

### Módulos Pendientes:

**1. Disponibilidad - Completar:**

- Vista de detalle de la actividad (modal o página)
- Galería de fotos de la actividad
- Descripción completa e itinerario
- Qué incluye / Qué no incluye
- Punto de encuentro y horarios disponibles
- Calendario de disponibilidad específica por fecha
- Slider Puntos + Plata (ubicación y comportamiento)
- Opciones de ordenamiento (precio, popularidad, duración)

**2. Checkout:**

- Resumen de reserva (actividad, fecha, participantes)
- Formulario de datos de cada participante (nombre, edad, documento)
- Datos de contacto (email, teléfono)
- Solicitudes especiales o requerimientos dietéticos
- Métodos de pago (integración con gateway)
- Términos y condiciones de la actividad

**3. Confirmación:**

- Confirmación exitosa (código de reserva, voucher PDF)
- Email de confirmación automático
- Información de contacto del proveedor/operador
- Instrucciones: punto de encuentro, qué llevar
- Políticas de cancelación
- Manejo de errores (tipos, mensajes, acciones de recuperación)

**4. Admin:**

- Validación de reserva en backend
- Estados de procesamiento
- Voucher disponible o no

### Información de Negocio Pendiente:

**Proveedor:**

- Confirmar si HotelBeds es único proveedor
- Identificar diferencias funcionales si hay múltiples proveedores
- Validar disponibilidad por país (CR, PA, HN, DO, GT, SV, NI)

**Reglas del Slider:**

- ⚠️ **CRÍTICO:** Confirmar reglas y ubicación del slider en Actividades (disponibilidad, detalle o checkout)
- Porcentaje mínimo de puntos requerido
- Fórmula de cálculo Puntos ↔ Plata (por persona o total)
- Ubicación del slider (disponibilidad, detalle, checkout)

**Políticas de Producto:**

- Reglas de edades por pasajero (edades obligatorias en el modal de visitantes)
- Máximo de participantes por actividad
- Políticas de cancelación por tipo de actividad
- Reembolsos parciales o totales según timing
- Requisitos especiales (fitness, restricciones médicas)

**Proceso de Reserva:**

- Definir si emisión es automática o manual
- Tiempos de confirmación esperados
- Estados de reserva durante el proceso
- Disponibilidad de voucher
- Proceso de cancelación de reservas confirmadas

**Categorías de Actividades:**

- Confirmar lista completa de categorías HotelBeds
- Subcategorías por tipo de actividad
- Iconografía y badges por categoría

---

## 📚 REFERENCIAS

**Guías relacionadas:**

- [PROM_QA_Assistant.agent.md](../../../../agents/PROM_QA_Assistant.agent.md) - Valores globales PROM (URL, país, modelo de negocio)
- [PROM_VUELOS.md](PROM_VUELOS.md) - Referencia para estructura y componentes transversales

---

## 🔄 CONTROL DE CAMBIOS

### Versión 1.0 - 2026-01-25

**Cambios principales:**

- ✅ **Restructuración completa según arquitectura híbrida estándar** (referencia: PROM_VUELOS.md)
- ✅ Cambiado título H1 de "FLUJO E2E OBLIGATORIO PARA ACTIVIDADES" a "PRODUCTO: ACTIVIDADES"
- ✅ Agregada H2 "Descripción General" con 6 características principales
- ✅ Aplicada jerarquía H1 → H2 → H3 → H4 → H5 consistente
- ✅ **Reorganizado CONTEXTO OPERATIVO:**
  - H3 Proveedores Disponibles
  - H3 Componentes Transversales con H4 (Header, Tabs, Footer)
  - H3 Flujo E2E Obligatorio
- ✅ **Módulo HOME/LOGIN:**
  - H3 Descripción del Módulo
  - H3 FUNCIONALIDADES (emoji 🎨)
  - Widget de Búsqueda con estructura completa H5:
    - 📖 Descripción Funcional (con lista de componentes DENTRO)
    - 💻 Comportamiento Esperado (integra Modal Destinos, Calendario y Dropdown Participantes)
    - ✅ VALIDACIONES DE QA (10 validaciones VAL-ACT-HOME-001 a 010)
    - 🧪 Escenarios de Prueba (5 escenarios)
- ✅ **Módulo DISPONIBILIDAD - Inicio:**
  - H3 Descripción del Módulo
  - H3 FUNCIONALIDADES
  - Widget de Búsqueda Persistente con estructura completa H5:
    - 📖 Descripción Funcional
    - 🧩 Componentes (tabla Markdown con 5 componentes)
    - 💻 Comportamiento Esperado
    - ✅ VALIDACIONES DE QA (7 validaciones VAL-ACT-DISP-001 a 007)
    - 🧪 Escenarios de Prueba (2 escenarios)
- ✅ Modal de Búsqueda de Destinos, Calendario y Dropdown integrados en Comportamiento Esperado (no H3 separados)
- ✅ "Descripción Funcional" con "Funcional", "Comportamiento Esperado" con "E" mayúscula
- ✅ Variaciones Móviles integradas en Comportamiento Esperado (no H5 separado)

**Pendiente para versión futura:**
- ⚠️ Completar Filtros Laterales y Cards de Actividades en DISPONIBILIDAD con misma estructura H5
- ⚠️ Documentar Módulos CHECKOUT y CONFIRMACIÓN con misma estructura
- ⚠️ Confirmar rangos de edad, límites de participantes, ubicación de slider P+P
- ⚠️ Confirmar categorías HotelBeds y políticas específicas de actividades

### Versión 0.3 - 2026-01-23

**Cambios principales:**

- ✅ Agregada URL Test Costa Rica (CR)
- ✅ Confirmado modelo de negocio: Puntos + Plata (Slider)
- ✅ Confirmado proveedor: HotelBeds
- ✅ Referenciados Componentes Transversales (ver PROM_VUELOS.md)
- ✅ Documentado Módulo Home/Login completo (Widget búsqueda + Modal destinos + Calendario + Dropdown participantes)
- ✅ Documentado Módulo Disponibilidad (Widget persistente, Filtros laterales, Cards de actividades)
- ✅ Agregados Pasos Obligatorios del Flujo E2E (26 pasos)
- ✅ Aplicada jerarquía de títulos consistente (H1 → H2 → H3)
- ✅ Eliminadas duplicaciones entre secciones
- ✅ Consolidadas Validaciones Críticas por módulo
- ✅ Reorganizados Próximos Pasos en categorías lógicas

### Versión 0.2 - 2026-01-20

**Cambios principales:**

- ✅ Identificado modelo de negocio B2B2C Transversal
- ✅ Agregados 7 países soportados (CR, PA, HN, DO, GT, SV, NI)

### Versión 0.1 - 2026-01-20

**Cambios principales:**

- ✅ Template inicial creado con estructura base
- ✅ Definidas secciones principales del documento
