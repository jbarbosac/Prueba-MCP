# 🛫 PRODUCTO: VUELOS - PROMERICA REWARDS

> **📖 Información Global:** Ver [PROM_QA_Assistant.agent.md](../../../../agents/PROM_QA_Assistant.agent.md) para URL del portal, país activo, modelo de negocio y versión del marketplace.

---

## 📌 Descripción General

El producto **Vuelos** permite a los usuarios del programa Promerica Rewards buscar, comparar y reservar vuelos utilizando el modelo de pago híbrido **Puntos + Plata (Slider)**. El sistema integra múltiples proveedores de aerolíneas y permite a los usuarios ajustar dinámicamente la proporción de puntos y efectivo para el pago de sus reservas.

**Características principales:**

- Búsqueda de vuelos ida y vuelta o solo ida
- Filtrado por aerolíneas, precios, horarios y escalas
- Modelo de pago flexible con slider Puntos + Plata
- Validación de saldo de puntos en tiempo real
- Integración con múltiples proveedores (SABRE, Aggregators)

---

## 📦 CONTEXTO OPERATIVO

### Proveedores Disponibles

⚠️ **PENDIENTE DE DEFINIR**

**Proveedores potenciales:**

- AGGREGATOR - NETACTICA
- AGGREGATOR - SABRE
- SABRE EDIFACT
- [Otros por confirmar]

### Componentes Transversales

> **Nota:** Estos componentes son compartidos por todos los productos del marketplace (Vuelos, Autos, Hoteles, Disney, Actividades).

#### Header Global

**Descripción:** Barra superior con navegación principal, branding personalizado de Promerica y acceso de usuario.

**Componentes:**

- Logo de Promerica (branding personalizable según país)
- Menú desplegable "Beneficios" (con ícono dropdown)
- Menú desplegable "Viajes" (con ícono dropdown)
- Menú desplegable "Más" (con ícono dropdown)
- Link "Contáctenos"
- Indicador de país de operación (esquina superior derecha)
- Perfil de usuario con iniciales, nombre completo y dropdown

#### Tabs de Productos

**Descripción:** Pestañas horizontales para navegación entre productos.

**Componentes:**

- Tab "Vuelos" (activo con subrayado verde)
- Tab "Autos"
- Tab "Hoteles"
- Tab "Disney"
- Tab "Actividades"

#### Footer Global

**Descripción:** Sección inferior con información institucional y canales de contacto personalizados por país.

**Componentes:**

- Logo y texto descriptivo de Promerica
- Sección "Enlaces" (Información del programa, Términos, Política de privacidad)
- Sección "Canales de atención" (Email, Teléfono)
- Redes sociales (Facebook, Instagram, X/Twitter)
- Copyright con año y país

### Flujo E2E Obligatorio

**Estos pasos deben incluirse en todos los casos de prueba para asegurar trazabilidad completa:**

1. **Acceder al portal** → https://traveltest-club-promerica.preprodppm.com/es-cr | El portal carga correctamente y muestra la pantalla de inicio
2. **Realizar login** → Ingresar usuario y contraseña válidos | Login exitoso y acceso al home con tabs de productos visibles
3. **Navegar a Vuelos** → Clic en tab "Vuelos" o acceso directo desde home | Widget de búsqueda de vuelos se muestra correctamente
4. **Configurar búsqueda** → Seleccionar origen, destino, fechas, pasajeros, aerolínea (opcional), vuelos directos (opcional) | Todos los campos se llenan correctamente
5. **Ejecutar búsqueda** → Clic en botón "Buscar" | Sistema redirige a módulo de Disponibilidad con resultados
6. **Validar resumen de búsqueda** → Revisar ruta/fechas/pasajeros en barra de resumen | Resumen coincide con criterios ingresados
7. **Aplicar filtros** → Seleccionar filtros de aerolínea, precio, horarios, escalas, duración | Resultados se actualizan dinámicamente
8. **Seleccionar vuelo** → Clic en card de resultado o botón "Ver detalles" | Se muestra detalle expandido del vuelo con itinerario completo
9. **Ajustar slider Puntos + Plata** → Mover slider para definir combinación de pago | Cálculo se actualiza en tiempo real, validación de saldo de puntos
10. **Continuar a Checkout** → Clic en botón "Continuar con este vuelo" | ⚠️ Pendiente documentar validaciones de checkout
11. **Completar datos de pasajeros** → Llenar formulario con información requerida | ⚠️ Pendiente documentar campos y validaciones específicas
12. **Seleccionar método de pago** → Ingresar datos de tarjeta si hay copago en plata | ⚠️ Pendiente documentar proceso de pago
13. **Confirmar reserva** → Clic en botón de confirmación final | ⚠️ Pendiente documentar proceso de emisión
14. **Validar confirmación** → Verificar código de reserva (PNR), resumen de pago, voucher | ⚠️ Pendiente documentar datos mostrados
15. **Verificar en Admin** → Buscar reserva en aplicativo Admin | ⚠️ Pendiente documentar validaciones de backend

**Nota:** Los pasos 10-15 están pendientes de documentación completa según información de módulos Checkout, Confirmación y Admin.

---

## 🏠 MÓDULO: HOME/LOGIN

### 📋 Descripción del Módulo

Página principal del marketplace donde el usuario accede al buscador de vuelos y navega entre productos disponibles. La interfaz es personalizable según el país configurado (Costa Rica en Test). Este módulo es el punto de entrada para todas las búsquedas de vuelos y proporciona acceso a las funcionalidades principales del sistema.

### 🎨 FUNCIONALIDADES

#### 🔹 Funcionalidad: Widget de Búsqueda de Vuelos

##### 📖 Descripción Funcional

**Componentes:**

1. **Radio buttons tipo de viaje:**
   - "Ida y vuelta" (seleccionado por defecto)
   - "Solo ida"

2. **Toggle switch:** "Vuelos directos"
   - Posición derecha, color verde cuando activo
   - Filtra solo vuelos sin escalas

3. **Campo "Origen":**
   - Placeholder: "Selecciona un origen"
   - Ícono de ubicación (izquierda)
   - Autocompletado de aeropuertos al escribir

4. **Campo "Destino":**
   - Placeholder: "Selecciona un destino"
   - Ícono de ubicación (izquierda)
   - Autocompletado de aeropuertos al escribir

5. **Campo "Selecciona tus fechas":**
   - Placeholder único para ida y regreso
   - Ícono de calendario (izquierda)
   - Abre datepicker al hacer clic

6. **Dropdown "Pasajeros y clase":**
   - Valor default: "1 adulto"
   - Despliega opciones de adultos, niños, infantes y clase

7. **Dropdown "Aerolínea":**
   - Valor default: "Todas"
   - Lista de aerolíneas disponibles

8. **Botón "Buscar":**
   - Color: Verde oscuro (#00563F aproximadamente)
   - Ícono de lupa (opcional)
   - Activa búsqueda

##### 💻 Comportamiento Esperado

**Interacción con tipo de viaje:**

- Radio "Ida y vuelta" muestra selector de fecha de regreso
- Radio "Solo ida" oculta fecha de regreso y solo permite seleccionar fecha de ida

**Interacción con toggle:**

- Toggle "Vuelos directos" activo (verde) → Búsqueda filtra solo vuelos sin escalas
- Toggle inactivo → Búsqueda incluye vuelos con escalas

**Autocompletado:**

- Campos origen/destino muestran sugerencias al escribir (mínimo 3 caracteres)
- Resultados incluyen código IATA, nombre del aeropuerto y ciudad
- Selección mediante clic o teclas de navegación (↑↓ Enter)

**Validaciones del sistema:**

- Campo fechas previene selección de fechas pasadas
- Sistema valida que origen y destino sean diferentes
- Botón "Buscar" deshabilitado (gris) si faltan campos obligatorios
- Al completar todos los campos, botón se habilita (verde)

**Flujo de navegación:**

- Al hacer clic en "Buscar" con datos válidos → Redirige a módulo Disponibilidad
- Parámetros de búsqueda se pasan a la siguiente pantalla

**Variaciones móviles:**

- Selector de pasajeros usa contadores +/- verticales en lugar de dropdown
- Al seleccionar campos de texto, aparece teclado nativo con barra de búsqueda
- Botón "Buscar" permanece fijo (sticky) en la parte inferior al hacer scroll

##### ✅ VALIDACIONES DE QA

Estas validaciones deben incluirse en todos los casos de prueba que involucren el Widget de Búsqueda:

- [ ] **VAL-VUE-HOME-001:** Origen y destino son obligatorios
  - **Verificar:** Botón "Buscar" deshabilitado si falta origen o destino
- [ ] **VAL-VUE-HOME-002:** Fechas no pueden ser pasadas
  - **Verificar:** Datepicker bloquea fechas anteriores a hoy
- [ ] **VAL-VUE-HOME-003:** Origen y destino deben ser diferentes
  - **Verificar:** Sistema muestra error si se selecciona el mismo aeropuerto
- [ ] **VAL-VUE-HOME-004:** Autocompletado funciona correctamente
  - **Verificar:** Mínimo 3 caracteres, muestra código IATA + nombre + ciudad
- [ ] **VAL-VUE-HOME-005:** Toggle vuelos directos filtra correctamente
  - **Verificar:** Resultados en Disponibilidad solo muestran vuelos sin escalas
- [ ] **VAL-VUE-HOME-006:** Radio buttons cambian el formulario
  - **Verificar:** "Solo ida" oculta fecha de regreso, "Ida y vuelta" la muestra
- [ ] **VAL-VUE-HOME-007:** Dropdown pasajeros valida límites
  - **Verificar:** Sistema respeta límites de pasajeros por reserva
- [ ] **VAL-VUE-HOME-008:** Botón "Buscar" redirige a Disponibilidad
  - **Verificar:** URL cambia y se muestran resultados según búsqueda

##### 🧪 Escenarios de Prueba

**Escenario 1: Búsqueda exitosa ida y vuelta - 1 adulto - P+P**

- **Prioridad:** 1 (Crítico)
- **Modelo de pago:** Puntos + Plata (50%)
- **Precondición:** Usuario autenticado con saldo de puntos suficiente
- **Pasos:**
  1. Login → Acceder al portal Promerica
  2. Navegar a tab "Vuelos" (si no está activo)
  3. Seleccionar radio button "Ida y vuelta"
  4. Campo Origen: Escribir "MGA" y seleccionar "Managua (MGA)"
  5. Campo Destino: Escribir "MIA" y seleccionar "Miami (MIA)"
  6. Campo Fechas: Seleccionar ida en 7 días, regreso en 14 días
  7. Dropdown Pasajeros: Mantener "1 adulto" (default)
  8. **Validar:** Botón "Buscar" habilitado (verde)
  9. Clic en botón "Buscar"
  10. **Validar:** Redirección a módulo Disponibilidad
  11. **Validar:** Resumen muestra "MGA - MIA" con fechas correctas
- **Resultado esperado:** Búsqueda ejecutada, resultados con modelo P+P
- **Título ADO:** `[PROM] Vuelos - Home - Búsqueda ida y vuelta - MGA a MIA - 1 adulto - P+P`

**Escenario 2: Búsqueda exitosa - MGA a MIA - 2 adultos - P+P**

- **Prioridad:** 1 (Crítico)
- **Modelo de pago:** Puntos + Plata (70% puntos / 30% plata)
- **Precondición:** Usuario autenticado con saldo de puntos suficiente para 2 pasajeros
- **Pasos:**
  1. Login → Acceder al portal Promerica
  2. Navegar a tab "Vuelos"
  3. Seleccionar radio button "Ida y vuelta"
  4. Campo Origen: Escribir "MGA" y seleccionar "Managua (MGA)"
  5. Campo Destino: Escribir "MIA" y seleccionar "Miami (MIA)"
  6. Campo Fechas: Seleccionar ida en 10 días, regreso en 17 días
  7. Dropdown Pasajeros: Seleccionar "2 adultos"
  8. **Validar:** Botón "Buscar" habilitado (verde)
  9. Clic en botón "Buscar"
  10. **Validar:** Redirección a módulo Disponibilidad
  11. **Validar:** Resumen muestra "MGA - MIA • 2 adultos"
  12. **Validar:** Precios reflejan tarifa para 2 pasajeros
  13. **Validar:** Slider P+P disponible en resultados
- **Resultado esperado:** Búsqueda exitosa para 2 adultos con modelo P+P
- **Título ADO:** `[PROM] Vuelos - Home - Búsqueda ida y vuelta - MGA a MIA - 2 adultos - P+P`

**Escenario 3: Validación de campos obligatorios**

- **Prioridad:** 1 (Crítico)
- **Precondición:** Usuario autenticado en el portal
- **Pasos:**
  1. Login → Acceder al portal Promerica
  2. Navegar a tab "Vuelos"
  3. **NO** llenar campo Origen
  4. **Validar:** Botón "Buscar" deshabilitado (gris)
  5. Campo Origen: Seleccionar "Managua (MGA)"
  6. **Validar:** Botón "Buscar" sigue deshabilitado (falta destino)
  7. Campo Destino: Seleccionar "Miami (MIA)"
  8. **Validar:** Botón "Buscar" sigue deshabilitado (faltan fechas)
  9. Campo Fechas: Seleccionar ida y regreso
  10. **Validar:** Botón "Buscar" ahora habilitado (verde)
- **Resultado esperado:** Sistema valida campos obligatorios correctamente
- **Título ADO:** `[PROM] Vuelos - Home - Validación campos obligatorios - MGA a MIA`

**Escenario 4: Toggle vuelos directos - MGA a MEX**

- **Prioridad:** 2 (Importante)
- **Modelo de pago:** Puntos + Plata
- **Precondición:** Usuario autenticado, búsqueda lista para ejecutar
- **Pasos:**
  1. Login → Navegar a Vuelos
  2. Configurar búsqueda: MGA → MEX (Ciudad de México), fechas válidas, 1 adulto
  3. **Activar** toggle "Vuelos directos" (debe verse verde)
  4. Clic en "Buscar"
  5. En Disponibilidad, **validar:** Todos los resultados muestran "Sin escalas"
  6. **Validar:** Ningún resultado muestra "1 escala" o "2+ escalas"
  7. **Validar:** Slider P+P visible en resultados
- **Resultado esperado:** Solo vuelos directos MGA-MEX con modelo P+P
- **Título ADO:** `[PROM] Vuelos - Home - Toggle vuelos directos - MGA a MEX - P+P`

---

## 📋 MÓDULO: DISPONIBILIDAD

### 📋 Descripción del Módulo

Módulo que muestra los resultados de búsqueda de vuelos disponibles según los criterios configurados por el usuario en el Widget de Búsqueda. Proporciona funcionalidades de filtrado dinámico, ordenamiento múltiple, visualización detallada de itinerarios y el selector de modelo de pago Puntos + Plata (Slider). Este módulo es crítico para la experiencia de selección de vuelos.

### 🎨 FUNCIONALIDADES

#### � Flujo de Interacción General

**Estado inicial al cargar el módulo (desde Home):**

1. **Elementos visibles:**
   - Buscador Modificable: COLAPSADO (solo link "Modificar búsqueda" visible)
   - Resumen de Búsqueda: COLAPSADO (sidebar derecho con header y ruta/fecha resumida)
   - Filtros: COLAPSADOS (sidebar izquierdo con headers de filtros cerrados)
   - Ordenamiento: Visible en "Recomendado" por defecto
   - Cards de Resultados: Listado principal visible con todos los vuelos disponibles

2. **Interacción del usuario - Secuencia típica:**
   - Usuario puede EXPANDIR Resumen de Búsqueda para ver detalles completos de la búsqueda
   - Usuario puede EXPANDIR Filtros individuales para refinar resultados (actualización en tiempo real)
   - Usuario puede activar chip "Precios por aerolíneas" → Aparece sección de Inspiracionales
   - Usuario puede cambiar Ordenamiento → Resultados se reordenan inmediatamente
   - Usuario puede modificar búsqueda → Expande buscador completo

3. **Selección de vuelo:**
   - Usuario revisa Cards de Resultados
   - Clic en "Reservar" o "Elige tu tarifa" → Abre Modal de Upsell (si aplica)
   - Usuario selecciona tarifa (Basic/Classic/Flex) en modal
   - Sistema redirige a módulo CHECKOUT/RESUMEN

4. **En módulo CHECKOUT/RESUMEN:**
   - Usuario ve resumen de vuelo seleccionado
   - Link "Ver condiciones" → Abre Modal de Condiciones (Términos y Cancelaciones)
   - Usuario completa información y procede al pago

**Nota importante:** Los modales (Upsell y Condiciones) se documentan aquí porque son parte del journey de Disponibilidad, aunque Condiciones se accede principalmente desde Checkout.

---

#### 🔹 Funcionalidad: Buscador Modificable

##### 📖 Descripción Funcional

Buscador expandible que permite al usuario modificar los criterios de búsqueda sin salir de la página de resultados. Se despliega en el área central superior.

**Ubicación:** Área central superior del módulo Disponibilidad  
**Tipo de componente:** Buscador colapsable/expandible  
**Estado inicial:** Colapsado (solo muestra link "Modificar búsqueda")

##### 🧩 Componentes del buscador expandido

1. **Tipo de vuelo:**
   - Radio button "Ida y vuelta" (seleccionado con fondo verde)
   - Radio button "Solo ida"
   - Radio button "Multidestino"
   - Toggle switch "Vuelos directos" (verde activado)

2. **Campos de búsqueda:**
   - Input "Origen" con placeholder "Selecciona un origen" + ícono de avión
   - Input "Destino" con placeholder "Selecciona un destino" + ícono de avión
   - Input "Selecciona tus fechas" con ícono de calendario

3. **Selector de pasajeros:**
   - Dropdown "Pasajeros y clase" (ej: "1 adulto")

4. **Acciones:**
   - Botón verde "Buscar" (principal)
   - Link "Ocultar búsqueda" (esquina inferior derecha)

##### 💻 Comportamiento Esperado

**Estado oculto (colapsado):**

- Texto: "Modificar búsqueda" (visible en header/breadcrumb)
- Al estar oculto, maximiza espacio para resultados

**Activación:**

- Clic en "Modificar búsqueda" → Despliega buscador completo
- Campos interactivos: Todos los inputs son editables
- Validaciones: Campos obligatorios antes de permitir "Buscar"

**Nueva búsqueda:**

- Clic en "Buscar" → Recarga resultados con nuevos criterios
- Ocultar: Clic en "Ocultar búsqueda" → Colapsa buscador
- Persistencia: Mantiene últimos valores ingresados

**Variaciones Móviles:**

- **Estado inicial:** Colapsado, muestra solo link "Modificar búsqueda"
- **Activación:** Tap en "Modificar búsqueda" → Despliega modal/expansión
- **Modal expandido:**
  - Ocupa sección superior de la pantalla
  - Fondo blanco con controles apilados verticalmente
  - Radio buttons y toggle más grandes (optimizados para touch)
- **Campos:**
  - Inputs de Origen/Destino abren modals de selección en pantalla completa
  - Selector de fechas abre datepicker en pantalla completa
  - Dropdown "Pasajeros y clase" abre modal de selección
- **Botones:**
  - "Buscar" (verde, ancho completo)
  - "Ocultar búsqueda" (link, centrado debajo del botón)
- **Colapsar:** Tap en "Ocultar búsqueda" → Regresa a estado inicial
- **Validaciones:** Campos obligatorios destacados antes de permitir búsqueda

##### ✅ VALIDACIONES DE QA

- [ ] **VAL-VUE-DISP-BUSC-001:** Buscador se expande correctamente
  - **Verificar:** Clic en "Modificar búsqueda" despliega formulario completo
- [ ] **VAL-VUE-DISP-BUSC-002:** Campos mantienen valores previos
  - **Verificar:** Origen, destino, fechas y pasajeros se precargan con búsqueda actual
- [ ] **VAL-VUE-DISP-BUSC-003:** Nueva búsqueda actualiza resultados
  - **Verificar:** Cambios en criterios recargan resultados correctamente
- [ ] **VAL-VUE-DISP-BUSC-004:** Botón "Ocultar búsqueda" funciona
  - **Verificar:** Colapsa buscador y maximiza espacio para resultados

##### 🧪 Escenarios de Prueba

**Escenario 1: Modificar búsqueda desde Disponibilidad**

- **Prioridad:** 1 (Crítico)
- **Precondición:** Búsqueda ejecutada (MGA-MIA, 1 adulto) con resultados visibles
- **Pasos:**
  1-11. [Búsqueda completa desde Home hasta Disponibilidad] 12. Clic en link "Modificar búsqueda" 13. **Validar:** Buscador se expande mostrando formulario completo 14. **Validar:** Campos precargan valores actuales (MGA, MIA, fechas, 1 adulto) 15. Cambiar destino a "MEX - Ciudad de México" 16. Clic en "Buscar" 17. **Validar:** Resultados se actualizan mostrando vuelos MGA-MEX 18. **Validar:** Resumen de búsqueda refleja nueva ruta "MGA - MEX"
- **Resultado esperado:** Modificación exitosa sin perder contexto
- **Título ADO:** `[PROM] Vuelos - Disponibilidad - Buscador modificable funciona - MGA a MEX`

---

#### 🔹 Funcionalidad: Resumen de Búsqueda

##### 📖 Descripción Funcional

Panel lateral derecho que muestra un resumen compacto de la búsqueda activa. Permite colapsar/expandir para optimizar espacio y retornar al home.

**Ubicación:** Panel lateral derecho del módulo Disponibilidad  
**Tipo de componente:** Sidebar colapsable con información de búsqueda  
**Estado inicial:** Colapsado (muestra solo header, ruta y fecha resumida)

##### 🧩 Componentes

**Header colapsable:**

- Título: "Resumen de búsqueda"
- Flecha de colapsar/expandir (arriba/abajo)

**Contenido expandido:**

- Ruta con formato "De [Origen] a [Destino]"
- Fechas: "ida y vuelta, 1 viajero"
- **Sección Salida:**
  - Fecha completa (día, dd de mes de año)
  - Ruta con aeropuertos ([Ciudad] ([CÓDIGO]) - [Ciudad] ([CÓDIGO]))
- **Sección Regreso:**
  - Fecha completa
  - Ruta con aeropuertos
- **Sección Pasajeros:**
  - Cantidad y tipo (Adultos (X))
- **Sección Clases:**
  - Tipo de clase seleccionada

**Acciones:**

- Botón "← Volver al inicio" (outline verde)
- Link/checkbox: "Obtén ayuda en soporte@promerica..."
- Iconos flotantes de chat (S y P - verde y rosa)

**Contenido colapsado:**

- Header con título y flecha hacia abajo
- Ruta resumida: "De [Origen] a [Destino]"
- Fecha resumida: "ida y vuelta, 1 viajero"

##### 💻 Comportamiento Esperado

**Estado inicial:** Colapsado al cargar la página de disponibilidad (muestra solo header, ruta y fecha resumida)

**Expandir:** Clic en flecha → Despliega información completa (salida, regreso, pasajeros, clases)

**Colapsar:** Clic en flecha → Reduce panel mostrando solo ruta y fecha

**Volver al inicio:** Redirige al home del sitio (mantiene sesión activa)

**Persistencia:** Estado (expandido/colapsado) se mantiene durante la sesión

**Iconos de chat:** Visibles en ambos estados, acceso rápido a soporte

**Variaciones Móviles:**

- **Ubicación:** Posicionado en la parte superior de la pantalla, debajo del header
- **Estado inicial:** Colapsado por defecto al cargar (solo muestra ruta y fecha)
- **Header:** Muestra "De [Origen] a [Destino]" con flecha de colapsar/expandir
- **Botón "Volver al inicio":**
  - Aparece tanto en estado expandido como colapsado
  - Estilo: Botón outline verde con flecha ←
  - Acción: Redirige al home sin perder sesión
- **Contenido expandido:** Ocupa ancho completo de pantalla móvil, información apilada verticalmente
- **Iconos de chat:** No visibles en mobile (S y P ocultos)
- **Colapsar:** Tap en flecha → Reduce a una línea con ruta y fecha
- **Expandir:** Tap en flecha → Despliega información completa

##### ✅ VALIDACIONES DE QA

- [ ] **VAL-VUE-DISP-RESUM-001:** Resumen coincide con búsqueda original
  - **Verificar:** Datos en resumen = Datos configurados en Widget de Búsqueda
- [ ] **VAL-VUE-DISP-RESUM-002:** Estado colapsado/expandido funciona
  - **Verificar:** Clic en flecha alterna entre ambos estados
- [ ] **VAL-VUE-DISP-RESUM-003:** Botón "Volver al inicio" funciona
  - **Verificar:** Redirige al home sin perder sesión
- [ ] **VAL-VUE-DISP-RESUM-004:** Información completa en estado expandido
  - **Verificar:** Muestra salida, regreso, pasajeros y clases correctamente

##### 🧪 Escenarios de Prueba

**Escenario 1: Verificación de resumen de búsqueda - MGA a MIA**

- **Prioridad:** 1 (Crítico)
- **Precondición:** Búsqueda ejecutada desde Home (MGA-MIA, 1 adulto)
- **Pasos:**
  1-10. [Pasos de búsqueda desde Home según Escenario 1 de HOME] 11. En Disponibilidad, localizar panel Resumen de Búsqueda (derecha) 12. **Validar:** Estado inicial COLAPSADO (solo ruta y fecha visibles) 13. Clic en flecha para expandir 14. **Validar:** Sección Salida muestra fecha completa y aeropuertos 15. **Validar:** Sección Regreso muestra fecha completa y aeropuertos 16. **Validar:** Sección Pasajeros muestra "Adultos (1)" 17. **Validar:** Botón "Volver al inicio" visible 18. Clic en flecha para colapsar 19. **Validar:** Panel regresa a estado colapsado
- **Resultado esperado:** Resumen preciso y funcionalidad colapsar/expandir correcta
- **Título ADO:** `[PROM] Vuelos - Disponibilidad - Resumen colapsable - MGA a MIA - 1 adulto`

---

#### 🔹 Funcionalidad: Ordenamiento de Resultados

##### 📖 Descripción Funcional

Dropdown que permite al usuario ordenar los resultados de vuelos según diferentes criterios.

**Ubicación:** Encima del listado de resultados, generalmente a la derecha  
**Tipo de componente:** Dropdown selector  
**Actualización:** Inmediata (sin recarga)

##### 🧩 Componentes

**Dropdown selector con opciones:**

- "Recomendado" (por defecto)
- "Precio: menor a mayor"
- "Precio: mayor a menor"
- "Duración: menor a mayor"
- "Duración: mayor a menor"
- "Hora de salida: más temprano"
- "Hora de salida: más tarde"

##### 💻 Comportamiento Esperado

**Estado inicial:** "Recomendado" seleccionado por defecto

**Interacción:** Clic en dropdown → Muestra opciones disponibles

**Selección:** Clic en opción → Reordena resultados inmediatamente

**Persistencia:** Orden seleccionado se mantiene durante la sesión

**Indicador visual:** Opción activa destacada en el dropdown

**Variaciones Móviles:**

- **Posición:** Sticky en la parte superior, debajo del buscador colapsado
- **Dropdown expandido:**
  - Tap abre modal/sheet en parte inferior de pantalla
  - Opciones en lista vertical con altura de touch target (mínimo 48px)
  - Opción activa con marca visual (✓) y fondo destacado
- **Selección:** Tap en opción → Cierra modal y aplica ordenamiento
- **Indicador visual:** Texto del dropdown muestra opción activa actual
- **Animación:** Resultados se reordenan con transición suave
- **Accesibilidad:** Touch targets grandes, separación clara entre opciones

##### ✅ VALIDACIONES DE QA

- [ ] **VAL-VUE-DISP-ORDEN-001:** Reordenamiento inmediato
  - **Verificar:** Cards se reordenan en < 500ms sin recarga
- [ ] **VAL-VUE-DISP-ORDEN-002:** Ordenamiento por precio correcto
  - **Verificar:** Primer resultado tiene precio más bajo, último más alto
- [ ] **VAL-VUE-DISP-ORDEN-003:** Ordenamiento respeta filtros
  - **Verificar:** Solo reordena resultados filtrados visibles
- [ ] **VAL-VUE-DISP-ORDEN-004:** Indicador visual activo
  - **Verificar:** Criterio seleccionado está destacado

##### 🧪 Escenarios de Prueba

**Escenario 1: Ordenamiento por precio - MGA a MIA**

- **Prioridad:** 2 (Importante)
- **Precondición:** Resultados con diferentes precios visibles (MGA-MIA, 1 adulto)
- **Pasos:**
  1-11. [Búsqueda completa desde Home] 12. Localizar dropdown de ordenamiento 13. **Validar:** "Recomendado" seleccionado por defecto 14. Clic en dropdown 15. Seleccionar "Precio: menor a mayor" 16. **Validar:** Resultados se reordenan inmediatamente 17. Revisar primeras 3 cards 18. **Validar:** Precios en orden ascendente (más barato primero) 19. Scroll hasta el final 20. **Validar:** Último resultado tiene precio más alto
- **Resultado esperado:** Ordenamiento correcto por precio
- **Título ADO:** `[PROM] Vuelos - Disponibilidad - Ordenamiento por precio - MGA a MIA - 1 adulto`

---

#### 🔹 Funcionalidad: Filtros

##### 📖 Descripción Funcional

Panel lateral izquierdo con filtros colapsables que permiten refinar los resultados de vuelos. Cada filtro inicia cerrado y actualiza resultados en tiempo real.

**Ubicación:** Panel lateral izquierdo en desktop, drawer expandible en móvil  
**Tipo de componente:** Panel de filtros con controles múltiples  
**Actualización:** Dinámica (sin recarga de página)

**Ubicación:** Panel lateral izquierdo en desktop, drawer expandible en móvil  
**Tipo de componente:** Panel de filtros con controles múltiples  
**Actualización:** Dinámica (sin recarga de página)

##### 🧩 Componentes

1. **Precio puntos:**
   - Acordeón colapsable
   - Contenido: [Configuración de filtro por puntos]

2. **Precios por aerolíneas:**
   - Chip verde activo (puede desactivarse)
   - Al activar: Muestra cards de "Inspiracionales" con precios por aerolínea

3. **Horario de salida:**
   - Acordeón colapsable
   - **Contenido:**
     - Slider de rangos horarios con doble manija
     - Badges circulares "S" (verde) y "C" (azul) - indicadores visuales
     - Rangos numéricos: 00:00 a 23:59

4. **Horario de regreso:**
   - Acordeón colapsable
   - Mismo comportamiento que "Horario de salida"

5. **Escala:**
   - Acordeón colapsable
   - **Opciones (radio buttons):**
     - "Todos" (seleccionado por defecto)
     - "Directo"
     - "1 Escala"
     - "2 Escala"

6. **Familias tarifarias:**
   - Acordeón colapsable
   - **Opciones (radio buttons):**
     - "Todos" (seleccionado por defecto)
     - "Basic"
     - "Light"
     - "Mainbasic"
     - "Económica basic"
     - "Classic"
     - "Basic economy"
     - "Main"

7. **Equipaje:**
   - Acordeón colapsable
   - **Opciones (radio buttons):**
     - "Todos" (seleccionado por defecto)
     - "Artículo personal"
     - "Equipaje de mano"
     - "Equipaje en bodega"

##### 💻 Comportamiento Esperado

**Estado inicial:** Todos los filtros cerrados al cargar

**Interacción:** Clic en header del filtro → Expande/colapsa contenido

**Aplicación automática:** Cambios se aplican instantáneamente sin botón "Aplicar"

**Actualización dinámica:** Resultados se filtran en tiempo real

**Contador:** Texto "Total de vuelos encontrados: X de Y" se actualiza

**Persistencia:** Filtros aplicados se mantienen durante la sesión

**Chips activos:** "Precios por aerolíneas" con borde verde cuando está activo

**Variaciones Móviles:**

- **Activación:** Botón "Filtros" con ícono de embudo en parte superior de la pantalla
- **Modal pantalla completa:**
  - Header: "Filtros" con botón cerrar (X) en esquina superior derecha
  - Ocupa 100% del viewport
  - Fondo blanco sobre la vista de resultados
- **Filtros disponibles:**
  - Todos los filtros aparecen como acordeones colapsables
  - Sliders táctiles para rangos horarios
  - Radio buttons de mayor tamaño (optimizados para touch)
- **Estado inicial:** Todos los filtros cerrados
- **Interacción:** Tap en acordeón → Expande/colapsa
- **Aplicación:** Cambios se aplican automáticamente sin botón "Aplicar"
- **Cerrar:** Tap en X → Cierra modal y muestra resultados actualizados
- **Scroll:** Contenido scrollable si excede altura de pantalla

##### ✅ VALIDACIONES DE QA

- [ ] **VAL-VUE-DISP-FILT-001:** Actualización dinámica de resultados
  - **Verificar:** Resultados se actualizan sin recargar página (< 1 seg)
- [ ] **VAL-VUE-DISP-FILT-002:** Contador de resultados correcto
  - **Verificar:** Número mostrado coincide con cards visibles
- [ ] **VAL-VUE-DISP-FILT-003:** Filtros acumulativos funcionan
  - **Verificar:** Aplicar 2+ filtros reduce resultados progresivamente
- [ ] **VAL-VUE-DISP-FILT-004:** Botón "Limpiar filtros" resetea todo
  - **Verificar:** Todos los filtros se remueven, resultados completos se muestran
- [ ] **VAL-VUE-DISP-FILT-005:** Filtro aerolínea con logo visible
  - **Verificar:** Checkboxes muestran logo + nombre de aerolínea
- [ ] **VAL-VUE-DISP-FILT-006:** Filtro precio actualiza rango
  - **Verificar:** Solo vuelos dentro del rango se muestran

##### 🧪 Escenarios de Prueba

**Escenario 1: Aplicar filtro por aerolínea**

- **Prioridad:** 1 (Crítico)
- **Precondición:** Resultados de búsqueda mostrando múltiples aerolíneas
- **Pasos:**
  1-11. [Pasos de búsqueda completa hasta ver resultados] 12. Localizar panel de Filtros (izquierda en desktop) 13. En "Filtro por aerolínea", seleccionar checkbox de "Copa Airlines" 14. **Validar:** Resultados se actualizan automáticamente (< 1 seg) 15. **Validar:** TODOS los resultados mostrados son de Copa Airlines 16. **Validar:** Contador muestra "X vuelos encontrados" (reducido) 17. Scroll por todos los resultados visible 18. **Validar:** Ningún vuelo de otra aerolínea aparece
- **Resultado esperado:** Solo vuelos de Copa Airlines visibles
- **Título ADO:** `[PROM] Vuelos - Disponibilidad - Filtro aerolínea funciona correctamente`

**Escenario 2: Filtros acumulativos - MGA a MIA - 2 adultos - P+P**

- **Prioridad:** 1 (Crítico)
- **Modelo de pago:** Puntos + Plata (70%)
- **Precondición:** Búsqueda MGA-MIA con 2 adultos ejecutada
- **Pasos:**
  1. Login y buscar: MGA → MIA, ida y vuelta, 2 adultos
     2-11. [Completar búsqueda hasta ver resultados]
  2. Aplicar filtro: Expandir "Escala" y seleccionar "Directo"
  3. **Validar:** Solo vuelos directos visibles
  4. Aplicar filtro adicional: Expandir "Familias tarifarias" y seleccionar "Basic"
  5. **Validar:** Resultados se reducen nuevamente
  6. **Validar:** TODOS los vuelos son directos Y tarifa Basic
  7. **Validar:** Precio mostrado para 2 adultos con modelo P+P
  8. Hacer scroll completo por resultados
  9. **Validar:** Ningún vuelo con escalas o de otra familia tarifaria
- **Resultado esperado:** Filtros acumulativos correctos para 2 adultos
- **Título ADO:** `[PROM] Vuelos - Disponibilidad - Filtros acumulativos - MGA a MIA - 2 adultos - P+P`

---

#### 🔹 Funcionalidad: Inspiracionales por Aerolínea

##### 📖 Descripción Funcional

Sección horizontal con cards de aerolíneas que muestra precios iniciales. Aparece cuando el chip "Precios por aerolíneas" está activo.

**Ubicación:** Entre filtros y resultados, área central  
**Tipo de componente:** Carousel horizontal con cards  
**Activación:** Chip "Precios por aerolíneas" en panel de filtros

##### 🧩 Componentes

**Título:** "Precios por aerolínea" (chip verde con ícono de avión)

**Carousel de cards:**

- Navegación con flechas (< >)
- Scroll horizontal

**Estructura de cada card:**

1. **Card "Todas las aerolíneas"** (destacada con borde verde cuando seleccionada)
   - Texto: "Todas las aerolíneas"
   - Precio: "Desde USD $X,XXX"

2. **Cards de aerolíneas específicas:**
   - Logo de la aerolínea centrado
   - Nombre de aerolínea con código IATA (ej: "Latam Airlines (LA)")
   - Precio: "Desde USD $X,XXX"
   - Borde verde cuando está seleccionada

**Mensaje informativo:**

- Texto: "Los precios mostrados se encuentran sin cargos administrativos"
- Estilo: Texto pequeño, color gris

**Contador de resultados:**

- Formato: "Total de vuelos encontrados: X de Y"

##### 💻 Comportamiento Esperado

**Aparición:** Se muestra al activar chip "Precios por aerolíneas"

**Desaparición:** Se oculta al desactivar el chip

**Selección:** Clic en card → Filtra resultados por esa aerolínea

**"Todas las aerolíneas":** Muestra todos los resultados sin filtro de aerolínea

**Indicador visual:** Card seleccionada con borde verde

**Navegación:** Flechas permiten ver más aerolíneas si no caben en pantalla

**Precio actualizado:** Refleja la tarifa mínima disponible sin cargos

**Variaciones Móviles:**

- **Layout:** Carousel horizontal con scroll táctil (swipe)
- **Visualización:** Muestra 1.5 cards a la vez (indica que hay más contenido)
- **Cards:**
  - Tamaño optimizado para mobile
  - Logo de aerolínea centrado (más grande)
  - Texto y precio apilados verticalmente
- **Navegación:**
  - Swipe horizontal para navegar entre cards
  - Flechas < > ocultas, navegación por gestos touch
  - Dots indicadores en parte inferior
- **Selección:** Tap en card → Aplica filtro de aerolínea
- **Card activa:** Borde verde más grueso para mejor visibilidad
- **Mensaje informativo:** Texto reducido o abreviado para ahorrar espacio
- **Contador:** "Total de vuelos: X de Y" en tamaño más pequeño

##### ✅ VALIDACIONES DE QA

- [ ] **VAL-VUE-DISP-INSP-001:** Sección aparece al activar chip
  - **Verificar:** Activar "Precios por aerolíneas" muestra carousel
- [ ] **VAL-VUE-DISP-INSP-002:** Cards muestran aerolíneas disponibles
  - **Verificar:** Logos, nombres y precios correctos
- [ ] **VAL-VUE-DISP-INSP-003:** Selección filtra resultados
  - **Verificar:** Clic en card filtra solo esa aerolínea
- [ ] **VAL-VUE-DISP-INSP-004:** "Todas las aerolíneas" muestra todos
  - **Verificar:** Remueve filtro de aerolínea específica
- [ ] **VAL-VUE-DISP-INSP-005:** Navegación con flechas funciona
  - **Verificar:** Flechas permiten ver más aerolíneas

##### 🧪 Escenarios de Prueba

**Escenario 1: Activar y usar Inspiracionales - MGA a MIA**

- **Prioridad:** 2 (Importante)
- **Precondición:** Búsqueda MGA-MIA con resultados múltiples aerolíneas
- **Pasos:**
  1-11. [Búsqueda completa desde Home] 12. En panel de Filtros, activar chip "Precios por aerolíneas" 13. **Validar:** Aparece sección "Precios por aerolínea" con carousel 14. **Validar:** Card "Todas las aerolíneas" visible con precio 15. **Validar:** Cards de aerolíneas específicas con logos y precios 16. Clic en card de aerolínea específica (ej: Copa Airlines) 17. **Validar:** Card seleccionada con borde verde 18. **Validar:** Resultados filtran solo vuelos Copa Airlines 19. **Validar:** Contador actualiza "Total de vuelos encontrados: X de Y" 20. Clic en "Todas las aerolíneas" 21. **Validar:** Filtro se remueve, todos los resultados visibles
- **Resultado esperado:** Inspiracionales funcionales con filtrado correcto
- **Título ADO:** `[PROM] Vuelos - Disponibilidad - Inspiracionales por aerolínea - MGA a MIA`

---

#### 🔹 Funcionalidad: Cards de Resultados

##### 📖 Descripción Funcional

Listado vertical de vuelos disponibles. Cada card muestra información resumida del vuelo con opción de expandir detalles y desglose de precios por pasajero.

**Ubicación:** Área central de resultados, listado vertical  
**Tipo de componente:** Cards expandibles con información detallada  
**Carga:** Lazy loading (carga progresiva al hacer scroll)

##### 🧩 Componentes (por cada card)

**Header de la card:**

- Sección verde: "SALIDA" (IDA) o "REGRESO" (VUELTA)
- Ruta: "[ORIGEN] (CÓDIGO)" → "[DESTINO]" con flechas
- Fecha: "día, DD de mes de YYYY"
- Separador visual

**Información del vuelo:**

- **Logo de aerolínea:** Ícono identificador (izquierda superior)
- **Nombre de aerolínea:** Texto descriptivo
- **Badge de categoría:** "Económica" (verde)
- **Horarios:**
  - Hora de salida: "HH:MM"
  - Escala: "X escalas" con ciudad(es) de escala
  - Hora de llegada: "HH:MM"
- **Duración total:** "Xh XXm"
- **Ícono expandible:** Flecha abajo para ver itinerario detallado
- **Badge especial:** "Featured" (verde, opcional)
- **Mensaje promocional:** "Elige tu tarifa, mejora tu viaje" (enlace)

**Panel lateral derecho:**

- **Header:** "Valor pasajeros" con ícono expandible (^)
- **Precio destacado:** "USD $XXX" (tamaño grande, verde)
- **Desglose colapsable:**
  - Adultos: USD $XXX
  - Niños: USD $XXX (si aplica)
  - Otros cargos: USD $XX
  - Impuestos: USD $X,XXX.XX
  - Nota: "Incluido impuestos y fee de procesamiento"
- **Total final:**
  - Formato grande: "USD $X,XXX.XX"
  - Texto: "Impuestos incluidos"
- **Botón de acción:**
  - Botón verde "Reservar" (ancho completo)

##### 💻 Comportamiento Esperado

**Estado inicial:** Desglose de precios colapsado

**Expandir desglose:** Clic en "Valor pasajeros" → Despliega breakdown de costos

**Colapsar desglose:** Clic nuevamente → Oculta breakdown

**Ver itinerario:** Clic en flecha → Expande detalles de vuelo (escalas, aeropuertos, horarios)

**Elige tu tarifa:** Clic en enlace → Abre modal de Upsell (tarifas Basic/Classic/Flex)

**Botón Reservar:**

- Si NO tiene upsell → Redirige directamente a checkout
- Si tiene upsell → Abre modal de selección de tarifa primero

**Scroll infinito:** Al llegar al final de la lista, carga más resultados (si existen)

**Variaciones Móviles:**

- **Layout:** Cards apiladas verticalmente ocupando ancho completo
- **Estructura simplificada:**
  - Header de card sin separador visual fuerte
  - Logo de aerolínea en tamaño medio
  - Información de vuelo en formato compacto
- **Horarios y duración:** Layout horizontal optimizado con iconos más pequeños
- **Panel de precio:**
  - Aparece en la parte inferior de cada card
  - "Valor pasajeros" con flecha expandible
  - Precio destacado en verde
- **Desglose expandido:**
  - Tap en "Valor pasajeros" → Expande breakdown
  - Información apilada verticalmente
  - Texto e importes en tamaño legible para mobile
- **Botón "Reservar":**
  - Ancho completo de la card
  - Tamaño más grande (min 44px altura - touch target)
  - Fijo en la parte inferior de cada card
- **Ver itinerario:** Tap en flecha → Expande detalles en accordion
- **Badge "Featured":** Posicionado en esquina, tamaño reducido
- **Link "Elige tu tarifa":** Texto más pequeño, táctil fácil

##### ✅ VALIDACIONES DE QA

- [ ] **VAL-VUE-DISP-CARD-001:** Cards muestran información completa
  - **Verificar:** Todos los componentes visibles y legibles
- [ ] **VAL-VUE-DISP-CARD-002:** Hover destaca la card
  - **Verificar:** Borde o sombra aparece al pasar mouse
- [ ] **VAL-VUE-DISP-CARD-003:** Clic abre detalle expandido
  - **Verificar:** Cualquier área de la card abre el detalle
- [ ] **VAL-VUE-DISP-CARD-004:** Lazy loading funciona
  - **Verificar:** Más cards cargan al llegar al final del scroll
- [ ] **VAL-VUE-DISP-CARD-005:** Precio Puntos + Plata visible
  - **Verificar:** Formato claro con separadores de miles
- [ ] **VAL-VUE-DISP-CARD-006:** Logo de aerolínea correcto
  - **Verificar:** Logo coincide con aerolínea del vuelo

##### 🧪 Escenarios de Prueba

**Escenario 1: Visualización correcta de cards con desglose**

- **Prioridad:** 1 (Crítico)
- **Precondición:** Búsqueda MGA-MIA con resultados disponibles
- **Pasos:**
  1-11. [Búsqueda completa hasta resultados] 12. Localizar primera card de resultado 13. **Validar:** Header muestra "SALIDA" o "REGRESO" 14. **Validar:** Ruta con códigos IATA visible 15. **Validar:** Logo y nombre de aerolínea visible 16. **Validar:** Horarios de salida y llegada visibles 17. **Validar:** Duración total mostrada (formato "Xh Ym") 18. **Validar:** Badge de escalas visible 19. **Validar:** Panel lateral "Valor pasajeros" presente 20. **Validar:** Precio destacado en verde (USD $XXX) 21. Clic en "Valor pasajeros" 22. **Validar:** Desglose se expande (Adultos, Impuestos, Total) 23. **Validar:** Botón "Reservar" verde visible
- **Resultado esperado:** Card con información completa y desglose funcional
- **Título ADO:** `[PROM] Vuelos - Disponibilidad - Card con desglose - MGA a MIA`

---

#### 🔹 Funcionalidad: Modal de Upsell - Selección de Tarifas (V2)

##### 📖 Descripción Funcional

Modal que permite al usuario comparar y seleccionar entre diferentes categorías de tarifas (Basic, Classic, Flex) con sus respectivos beneficios y precios.

**Ubicación:** Modal central sobre página de Disponibilidad  
**Tipo de componente:** Modal comparativo con carousel de tarifas  
**Acceso:** Link "Elige tu tarifa, mejora tu viaje" desde card de vuelo o botón "Reservar"

##### 🧩 Estructura del modal

**Header:**

- Título principal: "Elige tu tarifa, mejora tu viaje"
- Subtítulo: "Disfruta tu tarifa con más espacio, ventanas asientos y beneficios adicionales"
- **Información del vuelo:**
  - Fechas (ej: "sáb, 19 oct a sáb, 26 oct")
  - Ruta: "[Ciudad] - [Ciudad]"
  - Nota: "ida y regreso a [Ciudad]"
- Botón cerrar (X) en esquina superior derecha

**Columnas de tarifas (3 opciones en carousel):**

1. **Basic** (Entrada)
   - Precio: "USD $X,XXX.XX"
   - **Beneficios con iconos:**
     - ✅ Verde: Artículo personal normal 1 maleta (incluido)
     - 🟠 Naranja: Maleta en bodega (costo adicional)
     - ⚪ Gris: Modificaciones antes y después del viaje (no incluido)
     - ⚪ Gris: Prioridad antes y después del viaje (no incluido)
   - **Desglose de precio (expandible):**
     - Dropdown muestra: Adultos, Niños, Otros cargos, Impuestos
     - Nota: "Total sin tasas ni cargos incluidos"
   - Botón: "Continuar" (outline blanco)

2. **Classic** (Recomendada)
   - Precio: "USD $X,XXX.XX"
   - **Beneficios con iconos:**
     - ✅ Verde: Artículo personal normal 1 maleta
     - ✅ Verde: Maleta en bodega de XX kg (XX lbs)
     - ✅ Verde: Kits
     - ✅ Verde: Maleta en bodega de XX kg (XX lbs)
     - ✅ Verde: Modificaciones antes y después del viaje
     - ✅ Verde: Prioridad antes y después del viaje
   - **Desglose de precio expandible**
   - Botón: "Seleccionar" (verde sólido - destacado)

3. **Flex** (Premium)
   - Precio: "USD $X.X"
   - **Beneficios con iconos:**
     - ✅ Verde: Todos los beneficios incluidos
   - **Desglose de precio expandible**
   - Botón: "Seleccionar" (verde)

**Navegación:**

- Dots indicadores en parte inferior (mostrar posición)
- Flechas laterales para navegar entre tarifas (si aplica)

##### 💻 Comportamiento Esperado

**Activación:**

- Clic en "Elige tu tarifa, mejora tu viaje" desde card de vuelo
- Clic en botón "Reservar" en vuelos con upsell disponible

**Comparación:** Usuario puede ver diferencias de precio y beneficios lado a lado

**Desglose expandible:** Clic en precio → Dropdown muestra breakdown detallado

**Selección:**

- Clic en "Continuar" (Basic) → Procede con tarifa básica
- Clic en "Seleccionar" (Classic/Flex) → Procede con tarifa seleccionada

**Cierre:**

- Botón X → Cierra modal sin cambios
- Clic fuera del modal → Cierra sin selección

**Redireccionamiento:** Tras seleccionar → Redirige a checkout con tarifa elegida

**Iconos visuales:**

- ✅ Verde = Incluido
- 🟠 Naranja = Costo adicional
- ⚪ Gris = No incluido

**Variaciones Móviles:**

- **Modal pantalla completa:** Ocupa 100% del viewport
- **Header:**
  - Título en tamaño más pequeño pero legible
  - Subtítulo puede ser multilinea
  - Botón X grande (mínimo 44x44px)
- **Layout de tarifas:**
  - **Vista inicial compacta:** Muestra solo una tarifa (generalmente "Basic")
  - **Botón "Ver tarifas ∨":** Expande para mostrar las 3 opciones en carousel
- **Carousel de tarifas:**
  - Muestra 1 tarifa completa a la vez
  - Swipe horizontal para navegar
  - Dots indicadores en parte inferior
- **Card de tarifa:**
  - Ocupa ~90% del ancho de pantalla
  - Beneficios con iconos grandes y texto legible
  - Lista vertical de beneficios con separación clara
- **Desglose de precio:**
  - Dropdown expandible por tap
  - Información apilada verticalmente
  - Fuentes en tamaño mobile-friendly
- **Botones:**
  - "Continuar" / "Seleccionar" en ancho completo
  - Altura mínima 48px (touch target)
  - Espaciado generoso entre elementos
- **Scroll:** Contenido scrollable si excede altura de pantalla
- **Cierre:** Tap en X o swipe hacia abajo (gesto modal)

##### ✅ VALIDACIONES DE QA

- [ ] **VAL-VUE-DISP-UPSE-001:** Modal se abre correctamente
  - **Verificar:** Abre desde link o botón Reservar, muestra 3 tarifas
- [ ] **VAL-VUE-DISP-UPSE-002:** Información de vuelo correcta
  - **Verificar:** Header muestra fechas y ruta correctas
- [ ] **VAL-VUE-DISP-UPSE-003:** Beneficios por tarifa visibles
  - **Verificar:** Iconos verdes/naranjas/grises según inclusión
- [ ] **VAL-VUE-DISP-UPSE-004:** Desglose de precio funciona
  - **Verificar:** Dropdown expande y muestra breakdown detallado
- [ ] **VAL-VUE-DISP-UPSE-005:** Selección redirige a checkout
  - **Verificar:** Botón "Seleccionar" procede con tarifa elegida
- [ ] **VAL-VUE-DISP-UPSE-006:** Navegación entre tarifas
  - **Verificar:** Flechas o swipe permiten ver todas las opciones

##### 🧪 Escenarios de Prueba

**Escenario 1: Seleccionar tarifa Classic - MGA a MIA**

- **Prioridad:** 1 (Crítico)
- **Precondición:** Búsqueda MGA-MIA con vuelos que tienen upsell
- **Pasos:**
  1-11. [Búsqueda completa hasta Disponibilidad] 12. Localizar card con link "Elige tu tarifa, mejora tu viaje" 13. Clic en el link 14. **Validar:** Modal se abre mostrando 3 tarifas (Basic, Classic, Flex) 15. **Validar:** Header muestra ruta "MGA - MIA" y fechas 16. **Validar:** Tarifa Basic muestra ícono naranja en "Maleta en bodega" 17. **Validar:** Tarifa Classic muestra todos los beneficios con íconos verdes 18. Clic en precio de Classic para expandir desglose 19. **Validar:** Dropdown muestra Adultos, Impuestos, Total 20. Clic en botón "Seleccionar" de tarifa Classic 21. **Validar:** Redirige a módulo Checkout con tarifa Classic seleccionada
- **Resultado esperado:** Upsell funcional con selección correcta
- **Título ADO:** `[PROM] Vuelos - Disponibilidad - Upsell tarifa Classic - MGA a MIA`

---

#### 🔹 Funcionalidad: Modal de Condiciones - Términos y Cancelaciones (V2)

##### 📖 Descripción Funcional

Modal informativo que muestra las condiciones de cambios y cancelación de vuelos, organizado por segmento y tipo de política.

**Ubicación:** Modal central bloqueante  
**Tipo de componente:** Modal informativo con scroll  
**Acceso:** Link "Ver condiciones" desde módulo CHECKOUT/RESUMEN (antes de confirmar pago)

##### 🧩 Estructura del modal

**Header:**

- Título principal: "Condiciones de cambios y cancelación de viajes"
- Subtítulo con contexto: "[Aerolínea] | [Origen] - [Destino]"

**Cuerpo del modal (estructura de contenido):**

**Organización por segmento de vuelo:**

- Cada segmento tiene su propio header: "[Aerolínea] | [Ciudad] - [Ciudad]"

**Bloques de información (formato bullets):**

1. **Cambios en las fechas del viaje:**
   - Bullets (•) con políticas específicas de cambio
   - Costos, plazos y condiciones

2. **Cambios en las fechas del viaje (tarifas especiales):**
   - Si aplican tarifas diferenciadas por categoría

3. **Cambios en las fechas después del inicio del viaje:**
   - Políticas post-inicio de viaje

4. **Modificación y cancelación antes del inicio del vuelo:**
   - Bullets con políticas de cancelación
   - Plazos y restricciones

5. **Devolución y cancelación después del inicio del vuelo:**
   - Políticas de reembolso
   - Bullets con condiciones específicas

**Secciones adicionales:**

6. **Tiempos de presentación en el aeropuerto:**
   - Lista numerada (1, 2, 3...)
   - Ej: "1. Presentarse XX horas antes en vuelos internacionales"

7. **Recomendaciones:**
   - Lista numerada con sugerencias
   - Verificación de documentos, requisitos, etc.

**Nota destacada:**

- Texto en negritas: "PARA TENER EN CUENTA"
- Párrafo adicional con información importante

**Footer del modal:**

- **Información del emisor:**
  - "Boleto: Agente"
  - Copyright: "©2023 Banco Grupo Promerica"
- **Acción:**
  - Botón verde "Aceptar" (cierra modal)

##### 💻 Comportamiento Esperado

**Activación:**

- **Principal:** Desde módulo de CHECKOUT/RESUMEN (antes de confirmar pago) mediante link "Ver condiciones"
- **Secundario:** Link "Ver condiciones" disponible en páginas de vuelo (si existe)
- **Contexto:** Usuario ya seleccionó vuelo y tarifa, está revisando términos antes de pagar

**Scroll:** Contenido scrollable si excede altura del viewport

**Lectura:** Modal informativo, no requiere aceptación obligatoria

**Cierre:**

- Botón "Aceptar" → Cierra modal
- Botón X (si existe) → Cierra modal

**Accesibilidad:** Modal bloqueante (focus trap) hasta cerrar

**Estructura clara:** Información organizada por segmento y tipo de política

**Variaciones Móviles:**

- **Modal pantalla completa:** Ocupa 100% del viewport
- **Header:**
  - Título en tamaño legible para mobile
  - Subtítulo puede ocupar 2 líneas si es necesario
  - Botón X grande en esquina superior derecha
- **Contenido:**
  - Texto en tamaño base mobile (16px mínimo para legibilidad)
  - Párrafos con espaciado generoso
  - Bullets con indentación clara
  - Listas numeradas con números destacados
- **Secciones:**
  - Headers de segmento en negrita y tamaño mayor
  - Separadores visuales entre secciones
  - Bloques de información con padding adecuado
- **Nota destacada "PARA TENER EN CUENTA":**
  - Fondo gris claro o borde destacado
  - Texto en negrita
  - Separado visualmente del resto
- **Footer:**
  - Información del emisor en tamaño reducido
  - Copyright en una o dos líneas
  - Botón "Aceptar" grande (ancho ~80%, centrado, altura 48px)
- **Scroll:** Contenido completamente scrollable
- **Accesibilidad:** Modal con focus trap, no permite interacción con fondo

##### ✅ VALIDACIONES DE QA

- [ ] **VAL-VUE-COND-001:** Modal se abre desde link "Ver condiciones"
  - **Verificar:** Abre desde CHECKOUT/RESUMEN correctamente
- [ ] **VAL-VUE-COND-002:** Header muestra información correcta
  - **Verificar:** Aerolínea, origen y destino correctos
- [ ] **VAL-VUE-COND-003:** Contenido organizado por segmento
  - **Verificar:** Cada segmento tiene su header y políticas
- [ ] **VAL-VUE-COND-004:** Secciones de políticas visibles
  - **Verificar:** Cambios, cancelaciones, tiempos de presentación
- [ ] **VAL-VUE-COND-005:** Nota "PARA TENER EN CUENTA" destacada
  - **Verificar:** Visualmente diferenciada del resto del contenido
- [ ] **VAL-VUE-COND-006:** Botón "Aceptar" cierra modal
  - **Verificar:** Regresa a pantalla de CHECKOUT/RESUMEN

##### 🧪 Escenarios de Prueba

**Escenario 1: Revisar condiciones antes de pagar - MGA a MIA**

- **Prioridad:** 1 (Crítico)
- **Precondición:** Usuario en CHECKOUT/RESUMEN con vuelo MGA-MIA seleccionado
- **Pasos:**
  1-21. [Flujo completo hasta CHECKOUT/RESUMEN] 22. Localizar link "Ver condiciones" 23. Clic en "Ver condiciones" 24. **Validar:** Modal se abre en pantalla completa 25. **Validar:** Header muestra "Aerolínea | MGA - MIA" 26. **Validar:** Contenido organizado por segmentos (SALIDA y REGRESO) 27. **Validar:** Secciones visibles: Cambios, Cancelaciones, Tiempos 28. Scroll completo del contenido 29. **Validar:** Nota "PARA TENER EN CUENTA" destacada 30. **Validar:** Footer con copyright y botón "Aceptar" 31. Clic en "Aceptar" 32. **Validar:** Modal se cierra, regresa a CHECKOUT/RESUMEN
- **Resultado esperado:** Modal de condiciones completo y funcional
- **Título ADO:** `[PROM] Vuelos - Condiciones - Modal términos y cancelaciones - MGA a MIA`

---

#### 🔹 Funcionalidad: Slider Puntos + Plata

> **📋 Referencia:** La documentación completa del Slider Puntos + Plata (modelo de pago híbrido) se encuentra en [Knowledge_Base_Promerica.md](../../../../documentation/knowledge-bases/Knowledge_Base_Promerica.md#modelo-de-pago-slider-puntos--plata) para consulta centralizada.
>
> **Nota para QA:** Al crear casos de prueba relacionados con el Slider, consultar el Knowledge Base para:

##### � Referencia al Knowledge Base

> **📖 Documentación Completa:** [Knowledge_Base_Promerica.md - Modelo de Pago Slider Puntos + Plata](../../../../documentation/knowledge-bases/Knowledge_Base_Promerica.md#modelo-de-pago-slider-puntos--plata)

**Para casos de prueba del Slider, consultar el Knowledge Base para:**

- Descripción funcional completa
- Componentes del slider (visual, labels, displays)
- Comportamiento esperado (cálculos en tiempo real, validaciones automáticas)
- Estados del sistema (normal, error saldo, loading)
- Ejemplos de cálculo con diferentes porcentajes
- Validaciones de QA específicas del slider
- Escenarios de prueba detallados (ajuste exitoso, bloqueo por saldo)

**Resumen rápido:**

- **Función:** Ajustar dinámicamente proporción Puntos/Plata para pago de vuelo
- **Ubicación:** Cards de resultados y detalle expandido
- **Validación:** Tiempo real de saldo disponible
- **Rango:** Mínimo configurable hasta 100% puntos

**⚠️ Importante:** El slider es una funcionalidad transversal crítica del modelo de negocio Promerica. Referirse siempre al Knowledge Base para información actualizada sobre tasas de conversión, porcentajes mínimos y reglas de negocio

---

## 💳 MÓDULO: CHECKOUT

### 📋 Descripción del Módulo

> ⚠️ **Documentación en proceso**  
> Este módulo está siendo estandarizado según la estructura definida por el equipo.  
> Se está trabajando en la documentación de: Formulario de pasajeros, Datos de contacto, Servicios adicionales, Métodos de pago, Resumen de reserva.  
> **Estado:** 🔄 Pendiente de completar

---

## ✅ MÓDULO: CONFIRMACIÓN

### 📋 Descripción del Módulo

> ⚠️ **Documentación en proceso**  
> Este módulo está siendo estandarizado según la estructura definida por el equipo.  
> Se está trabajando en la documentación de: Confirmación exitosa, Número de reserva (PNR), Voucher descargable, Error en procesamiento.  
> **Estado:** 🔄 Pendiente de completar

---

## 📝 ANEXOS PARA QA

> **Nota:** Estas validaciones complementan los "Pasos Obligatorios del Flujo E2E". No duplican los pasos, sino que detallan las validaciones específicas a verificar en cada punto.

### Validaciones por Módulo:

**Home/Login:**
✅ Campos obligatorios: Origen, destino, fechas, pasajeros  
✅ Botón buscar: Habilitado solo con campos completos  
✅ Fechas: No permite selección de fechas pasadas  
✅ Autocompletado: Origen y destino muestran sugerencias al escribir  
✅ Validación: Origen y destino deben ser diferentes

**Disponibilidad:**
✅ Lista de vuelos con precios en Puntos + Plata  
✅ Filtros: Actualización dinámica sin recargar página  
✅ Carga lazy: Cards adicionales cargan al hacer scroll  
✅ Ordenamiento: Reordenamiento inmediato de resultados  
✅ Detalle expandido: Modal con información completa del vuelo

**Checkout:**
⚠️ Pendiente documentar: Datos de pasajeros, contacto, métodos de pago

**Confirmación:**
⚠️ Pendiente documentar: Código de reserva (PNR), resumen de pago, voucher

**Admin:**
⚠️ Pendiente documentar: Reserva localizable, estados de emisión

### Validaciones Específicas del Modelo Slider (Puntos + Plata):

✅ **Visibilidad:** Slider presente en cards de resultados y detalle expandido  
✅ **Cálculo dinámico:** Actualización en tiempo real al mover slider  
✅ **Fórmula:** Puntos + Plata = Total del vuelo  
✅ **Validación de saldo:** Sistema verifica puntos disponibles antes de continuar  
✅ **Solicitud de pago:** Si hay copago en plata, se requiere método de pago  
⚠️ **Pendiente definir:** Porcentaje mínimo de puntos requerido  
⚠️ **Pendiente definir:** Tipo de emisión (automática/manual) según combinación de pago

### Validaciones de Experiencia de Usuario (UI/UX):

✅ **Responsive:** Adaptación correcta a móviles (sticky buttons, teclado nativo)  
✅ **Estados de carga:** Indicadores visuales durante búsqueda/procesamiento  
✅ **Mensajes de error:** Claros y orientados a acción del usuario  
✅ **Accesibilidad:** Componentes navegables por teclado y lectores de pantalla

---

### Formato de Título en Azure DevOps

> **Fuente:** Mantener consistencia con la convención global definida en `PROM_QA_Assistant.agent.md`.

```
[PROM] Vuelos - [Módulo/Funcionalidad] - [Escenario] - [Variante]
```

**Notas:**

- La **Variante** puede incluir ruta, tipo de vuelo, pasajeros, clase, modelo de pago y proveedor (si aplica y está confirmado).
- Evitar fijar valores ⚠️ _Pendiente/TBD_ (ej. proveedor) dentro del título.

**Ejemplos:**

- `[PROM] Vuelos - Home - Búsqueda ida y vuelta - MGA a MIA - 1 adulto - P+P`
- `[PROM] Vuelos - Disponibilidad - Resumen correcto - MGA a MIA - 1 adulto`
- `[PROM] Vuelos - Disponibilidad - Slider bloqueado - Saldo insuficiente - MGA a MEX`

---

### Próximos Pasos para Completar Este Archivo

### Módulos Documentados:

✅ **Componentes Transversales** - Header, Tabs, Footer  
✅ **Pasos Obligatorios del Flujo E2E** - 14 pasos documentados (pasos 1-8 completos, 9-14 pendientes)  
✅ **Módulo Home/Login** - Widget de búsqueda con 8 componentes  
✅ **Módulo Disponibilidad** - 5 funcionalidades: Resumen, Filtros, Cards, Ordenamiento, Detalle expandido

### Módulos Pendientes:

**1. Checkout:**

- Resumen de reserva
- Formulario de datos de pasajeros (campos específicos, validaciones)
- Datos de contacto
- Servicios adicionales (asientos, equipaje, seguros)
- Métodos de pago (integración con gateway)
- Términos y condiciones

**2. Confirmación:**

- Confirmación exitosa (PNR, código, voucher PDF)
- Email de confirmación automático
- Manejo de errores (tipos, mensajes, acciones de recuperación)

**3. Admin:**

- Validación de reserva en backend
- Estados de emisión y seguimiento
- Proceso de emisión automática/manual

### Información de Negocio Pendiente:

**Proveedores:**

- Confirmar lista completa de proveedores de vuelos
- Identificar diferencias funcionales por proveedor
- Validar disponibilidad por país (CR, PA, HN, DO, GT, SV, NI)

**Reglas del Slider:**

- Porcentaje mínimo de puntos requerido
- Fórmula de cálculo Puntos ↔ Plata por proveedor
- Validación de saldo disponible
- Comportamiento cuando saldo es insuficiente

**Políticas de Producto:**

- Rangos de edad por tipo de pasajero (Adultos/Niños/Infantes)
- Clases disponibles (Económica confirmada, Ejecutiva/Primera por confirmar)
- Políticas de equipaje por aerolínea
- Opciones de equipaje adicional y costos
- Fees de procesamiento (si aplican)
- Servicios adicionales disponibles (asientos, seguros)

**Proceso de Emisión:**

- Definir si es automática o manual
- Condiciones para cada tipo de emisión
- Tiempos de emisión esperados
- Estados de reserva durante el proceso

---

## 📚 REFERENCIAS

**Guías relacionadas:**

- [SHARED_QA_RULES.md](../../../../shared/SHARED_QA_RULES.md) - Fundamentos ISTQB y Azure DevOps
- [PROM_COMMON_RULES.md](../../../../shared/Reglas Marketplace/PROM_COMMON_RULES.md) - Reglas comunes Promerica

---

## 🔄 CONTROL DE CAMBIOS

### Versión 1.1 - 2026-02-03

**Cambios principales:**

- ✅ **Módulo Disponibilidad:** Agregado Flujo de Interacción General con estados iniciales
- ✅ **Nueva funcionalidad:** Buscador Modificable colapsable/expandible
- ✅ **Actualizado:** Resumen de Búsqueda (panel lateral derecho con estado colapsable)
- ✅ **Reordenado:** Ordenamiento de Resultados (movido antes de Filtros)
- ✅ **Actualizado:** Filtros con nueva estructura de acordeones colapsables
- ✅ **Nueva funcionalidad:** Inspiracionales por Aerolínea (carousel con chips y cards)
- ✅ **Actualizado:** Cards de Resultados con desglose de precios expandible
- ✅ **Nueva funcionalidad:** Modal de Upsell V2 (selección de tarifas Basic/Classic/Flex)
- ✅ **Nueva funcionalidad:** Modal de Condiciones (términos y cancelaciones)
- ✅ **Refactorizado:** Slider Puntos + Plata movido al Knowledge Base con referencia
- ✅ **Completado:** Variaciones Móviles en todas las funcionalidades
- ✅ **Eliminado:** Detalle Expandido de Vuelo (reemplazado por nuevo diseño de cards)
- ✅ Total funcionalidades documentadas: 9 (vs 6 en v1.0)

### Versión 1.0 - 2026-01-25

**Cambios principales:**

- ✅ Aplicada arquitectura híbrida (propósito dual: humanos + agente QA)
- ✅ Reorganizada jerarquía según estructura estándar de productos
- ✅ Módulo Home/Login con estructura completa
- ✅ Módulo Disponibilidad con 6 funcionalidades documentadas
- ✅ Cada funcionalidad incluye validaciones QA y escenarios de prueba
- ✅ Formato optimizado para generación de casos por agente

### Versión 0.3 - 2026-01-23

**Cambios principales:**

- ✅ Agregada URL Test Costa Rica (CR)
- ✅ Confirmado modelo de negocio: Puntos + Plata (Slider)
- ✅ Documentados Componentes Transversales (Header, Tabs, Footer)
- ✅ Documentado Módulo Home/Login completo (Widget búsqueda con 8 componentes)
- ✅ Documentado Módulo Disponibilidad completo (5 funcionalidades)
- ✅ Agregados Pasos Obligatorios del Flujo E2E (15 pasos)
- ✅ Reorganizada jerarquía de títulos (H1 → H2 → H3)
- ✅ Eliminadas duplicaciones entre secciones
- ✅ Consolidadas Validaciones Críticas por módulo
- ✅ Reorganizados Próximos Pasos en categorías lógicas

### Versión 0.2 - 2026-01-20

**Cambios principales:**

- ✅ Identificado modelo de negocio B2B2C Transversal
- ✅ Agregados 7 países soportados (CR, PA, HN, DO, GT, SV, NI)
- ✅ Documentado patrón de URLs por país

### Versión 0.1 - 2026-01-20

**Cambios principales:**

- ✅ Template inicial creado con estructura base
- ✅ Definidas secciones principales del documento
