# 🚗 PRODUCTO: AUTOS - PROMERICA REWARDS

> **📖 Información Global:** Ver [PROM_QA_Assistant.agent.md](../../../../agents/PROM_QA_Assistant.agent.md) para URL del portal, país activo, modelo de negocio y versión del marketplace.

---

## 📌 Descripción General

El producto **Autos** permite a los usuarios del programa Promerica Rewards buscar, comparar y reservar vehículos de renta utilizando el modelo de pago híbrido **Puntos + Plata (Slider)**. El sistema integra múltiples rentadoras (Hertz, Dollar, Thrifty) a través de Sabre y ofrece búsqueda avanzada por localidades con mapa interactivo.

**Características principales:**

- Búsqueda por aeropuertos y ciudades con mapa sincronizado
- Flexibilidad de devolución en mismo lugar o ubicación diferente (dropoff)
- Modelo de pago flexible con slider Puntos + Plata
- Múltiples categorías de vehículos (Standard, SUV, Premium, etc.)
- Integración con rentadoras Hertz, Dollar y Thrifty vía Sabre
- Soporte para códigos de descuento Hertz Gold y promocionales

---

## 📦 CONTEXTO OPERATIVO

### Proveedores Disponibles

⚠️ **PENDIENTE DE DEFINIR**

**Proveedores potenciales:**

- Sabre → Hertz, Dollar, Thrifty
- [Otros por confirmar]

### Componentes Transversales

> **Nota:** Estos componentes son compartidos por todos los productos del marketplace (Vuelos, Autos, Hoteles, Disney, Actividades). Ver detalle completo en [PROM_VUELOS.md](PROM_VUELOS.md#-componentes-transversales).

#### Header Global

Barra superior con navegación principal, branding personalizado de Promerica y acceso de usuario.

#### Tabs de Productos

Pestañas horizontales para navegación entre productos (Vuelos, **Autos**, Hoteles, Disney, Actividades).

#### Footer Global

Sección inferior con información institucional y canales de contacto personalizados por país.

### Flujo E2E Obligatorio

**Estos pasos deben incluirse en todos los casos de prueba para asegurar trazabilidad completa:**

⚠️ **RESTRICCIÓN CRÍTICA DE PRUEBAS:**

- **Para pruebas hasta Checkout (pasos 1-20):** Se pueden usar búsquedas de **3, 5 o 7 días** sin problema
- **Para pruebas con Confirmación (pasos 21-25):** **SOLO usar 1 día de renta**
- **Razón:** Reservas confirmadas de múltiples días que no se cancelen generan costos reales al cliente
- **Recomendación:** Probar flujo completo (checkout + validaciones) con múltiples días, y ejecutar confirmación solo con 1 día cuando sea estrictamente necesario

---

1. **Acceder al portal** → https://traveltest-club-promerica.preprodppm.com/es-cr | El portal carga correctamente y muestra la pantalla de inicio
2. **Realizar login** → Ingresar usuario y contraseña válidos | Login exitoso y acceso al home con tabs de productos visibles
3. **Navegar a Autos** → Clic en tab "Autos" | Widget de búsqueda de autos se muestra correctamente
4. **Seleccionar lugar de recogida** → Clic en campo "Recogida" o "Ver todas las localidades" | Modal de búsqueda por localidades se abre
5. **Buscar y seleccionar ubicación** → Escribir ciudad/aeropuerto en buscador del modal | Sistema filtra resultados y muestra lista + mapa sincronizado
6. **Confirmar ubicación de recogida** → Clic en botón "Seleccionar" de ubicación deseada | Modal se cierra y campo "Recogida" se actualiza con ubicación seleccionada
7. **Seleccionar lugar de devolución** → Clic en campo "Devolución" o usar toggle para cambiar a mismo lugar | Dropdown o modal de ubicaciones se muestra
8. **Confirmar ubicación de devolución** → Seleccionar ubicación (misma o diferente) | Campo "Devolución" se actualiza
9. **Seleccionar fechas y horas** → Clic en "Selecciona tus fechas" | Calendario mensual se abre con selectores de hora/minuto
10. **Confirmar rango de fechas** → Seleccionar fecha inicio, fecha fin, horas | Calendario se cierra y campo muestra rango completo (ej: "Mié, Oct 22 - 12:00 - Sáb, Oct 25 - 12:45")
11. **Aplicar descuentos (opcional)** → Expandir sección "Selecciona tus descuentos" | Campos de código Hertz y descuentos promocionales se muestran
12. **Ejecutar búsqueda** → Clic en botón "Buscar" verde | Sistema redirige a módulo de Disponibilidad con resultados
13. **Revisar widget de búsqueda persistente** → Verificar resumen de criterios en parte superior | Widget compacto muestra recogida, devolución, fechas, códigos
14. **Navegar por categorías de vehículos** → Clic en pestañas (Standard, Intermediate, SUV, etc.) | Resultados filtran por categoría seleccionada
15. **Aplicar filtros laterales** → Seleccionar tipo de auto, rentadora, transmisión | Resultados se actualizan dinámicamente
16. **Alternar vista Lista/Matriz** → Clic en botones de vista | Visualización cambia entre cards verticales y tabla comparativa
17. **Seleccionar vehículo** → Clic en card de resultado (vista lista) | Se abre modal de protecciones/seguros
18. **Seleccionar protección/seguro** → Elegir una opción en el modal | Modal se cierra y el flujo continúa con vehículo + protección seleccionada
19. **Ajustar slider Puntos + Plata** → ⚠️ Pendiente documentar ubicación y comportamiento | ⚠️ Pendiente documentar validación de saldo
20. **Continuar a Checkout** → Clic en botón de confirmación | ⚠️ Pendiente documentar validaciones de checkout

**⚠️ ADVERTENCIA: Los siguientes pasos (21-25) deben ejecutarse SOLO con búsquedas de 1 día para evitar costos reales:**

21. **Completar datos del conductor** → Llenar formulario con información requerida y licencia | ⚠️ Pendiente documentar campos específicos | 🚨 **Usar solo 1 día desde este punto**
22. **Seleccionar método de pago** → Ingresar datos de tarjeta si hay copago en plata | ⚠️ Pendiente documentar proceso de pago
23. **Confirmar reserva** → Clic en botón de confirmación final | ⚠️ Pendiente documentar proceso de emisión
24. **Validar confirmación** → Verificar código de reserva, voucher | ⚠️ Pendiente documentar datos mostrados
25. **Verificar en Admin** → Buscar reserva en aplicativo Admin | ⚠️ Pendiente documentar validaciones de backend

**Nota:** Los pasos 19-25 están pendientes de documentación completa según información de módulos Detalle, Checkout, Confirmación y Admin.

---

## 🏠 MÓDULO: HOME/LOGIN

### 📋 Descripción del Módulo

Página principal del marketplace donde el usuario accede al buscador de autos y navega entre productos disponibles. La interfaz es personalizable según el país configurado (Costa Rica en Test). Este módulo proporciona búsqueda avanzada por localidades con mapa interactivo y flexibilidad para configurar recogida y devolución en lugares diferentes (dropoff).

### 🎨 FUNCIONALIDADES

#### 🔹 Funcionalidad: Widget de Búsqueda de Autos

##### 📖 Descripción Funcional

Formulario principal que permite a los usuarios configurar búsquedas de autos de renta especificando ubicaciones de recogida y devolución (mismo lugar o diferente), fechas/horas precisas, y códigos de descuento opcionales. El widget incluye un modal avanzado de búsqueda por localidades con mapa interactivo sincronizado para selección precisa de ubicaciones.

**Ubicación:** Centro de la página de inicio, debajo del header y tabs de productos  
**Tipo de componente:** Formulario interactivo con modal de búsqueda avanzada  
**Acceso:** Disponible para todos los usuarios autenticados

##### 🧩 Componentes

1. **Selector "Recogida":**
   - Campo con ícono de ubicación
   - Placeholder: "Seleccionar recogida"
   - Link "Ver todas las localidades" para abrir modal completo

2. **Selector "Devolución":**
   - Campo con ícono de ubicación
   - Placeholder: "Seleccionar devolución"
   - Link para abrir modal o dropdown categorizado

3. **Toggle Recogida/Devolución:**
   - Interruptor visual con punto indicador rojo
   - Permite cambiar entre configurar recogida o devolución

4. **Selector de Fechas:** "Selecciona tus fechas"
   - Abre calendario mensual con navegación (mes/año)
   - Flechas izquierda/derecha para cambiar mes
   - Selectores de hora (00-23) y minuto (00-59) para cada fecha
   - Validación: No permite fechas pasadas
   - Indicadores visuales: día actual, rango seleccionado
   - Botones: "Cancelar" | "Aceptar" (verde)

5. **Descuentos Hertz:**
   - Sección expansible: "Selecciona tus descuentos"
   - Campo de texto: "Ingresa tu código Hertz"
   - Placeholder: "Sin hertz Gold"
   - Botón "Agregar" (verde)

6. **Descuentos Promocionales:**
   - Dropdown: "Selecciona tu descuento"
   - Opciones predefinidas de descuentos disponibles
   - Checkbox: "Tengo un código promocional"
   - Campo de texto condicional al activar checkbox
   - Botón "Agregar" (verde)

7. **Botón Buscar:**
   - Botón verde para ejecutar la búsqueda
   - Deshabilitado si faltan campos obligatorios

##### 💻 Comportamiento Esperado

- **Recogida:** Clic abre modal de búsqueda por localidades (búsqueda avanzada con mapa)
- **Devolución:** Clic despliega dropdown categorizado (acceso rápido) o link para modal completo
- Toggle permite alternar entre configurar recogida o devolución
- **Calendario:** Permite seleccionar rango de fechas + horas/minutos específicas
- **Descuentos Hertz:** Expansible, código opcional, se agrega con botón verde
- **Descuentos Promocionales:** Dropdown predefinido o campo manual si activa checkbox
- **Validación:** Recogida, devolución y fechas son obligatorias antes de buscar
- Al hacer clic en "Buscar" → Redirige a módulo de Disponibilidad con resultados filtrados

##### 📱 Variaciones Móviles

- **Toggle "Pago en línea":** Aparece en la parte superior del widget (no visible en desktop)
- **Modal de Recogida/Devolución:** Vista simplificada en pantalla completa con lista de aeropuertos y ciudades
- **Mapa:** Accesible mediante interacción adicional
- **Calendario:** Ocupa pantalla completa con navegación táctil
- **Selectores de hora/minutos:** Aparecen como ruedas nativas (picker wheels) debajo del calendario
- **Secciones de descuentos:** Se expanden en pantalla completa cuando el usuario interactúa
- **Botón "Buscar":** Permanece fijo (sticky) en la parte inferior de la pantalla

##### ✅ VALIDACIONES DE QA

Estas validaciones deben incluirse en todos los casos de prueba que involucren el Widget de Búsqueda:

- [ ] **VAL-AUT-HOME-001:** Recogida y devolución son obligatorias
  - **Verificar:** Botón "Buscar" deshabilitado si falta alguna ubicación
- [ ] **VAL-AUT-HOME-002:** Fechas y horas obligatorias
  - **Verificar:** No permite buscar sin seleccionar rango de fechas
- [ ] **VAL-AUT-HOME-006:** Dropoff diferente funciona
  - **Verificar:** Permite seleccionar devolución en ubicación diferente a recogida
- [ ] **VAL-AUT-HOME-007:** Códigos Hertz son opcionales
  - **Verificar:** Búsqueda funciona sin ingresar códigos de descuento
- [ ] **VAL-AUT-HOME-008:** Botón "Buscar" redirige a Disponibilidad
  - **Verificar:** URL cambia y se muestran resultados según búsqueda

##### 🧪 Escenarios de Prueba

**Escenario 1: Búsqueda mismo lugar - MIA a MIA - 1 día - Hertz - P+P**

- **Prioridad:** 1 (Crítico)
- **Rentadora:** Hertz
- **Modelo de pago:** Puntos + Plata (ejemplo 50% - según configuración)
- **Precondición:** Usuario autenticado con saldo de puntos suficiente
- **Pasos:**
  1. Login → Acceder al portal Promerica
  2. Navegar a tab "Autos"
  3. Clic en campo "Recogida" → Abre modal de localidades
  4. Escribir "MIA" en buscador
  5. **Validar:** Resultados filtrados para Miami
  6. Seleccionar "Miami International Airport (MIA)"
  7. **Validar:** Modal se cierra, campo Recogida muestra "Miami Intl (MIA)"
  8. Clic en campo "Devolución"
  9. **Validar:** Muestra opción "Mismo lugar de recogida"
  10. Seleccionar "Mismo lugar de recogida (Miami Intl)"
  11. **Validar:** Campo Devolución muestra "Miami Intl (MIA)"
  12. Clic en "Selecciona tus fechas"
  13. Seleccionar fecha HOY + 7 días, hora 10:00
  14. Seleccionar fecha HOY + 8 días (1 día renta), hora 10:00
  15. **Validar:** Calendario muestra "1 día de renta"
  16. Clic en "Aceptar"
  17. **Validar:** Botón "Buscar" habilitado (verde)
  18. Clic en botón "Buscar"
  19. **Validar:** Redirección a módulo Disponibilidad
  20. **Validar:** Widget persistente muestra "MIA → MIA • 1 día"
  21. **Validar:** Resultados con modelo P+P visibles
- **Resultado esperado:** Búsqueda exitosa mismo lugar con modelo P+P
- **Título ADO:** `[PROM] Autos - Home - Búsqueda mismo lugar - MIA a MIA - 1 día - Hertz - P+P`

**Escenario 2: Búsqueda dropoff diferente - MIA a JFK - 1 día - Dollar - P+P**

- **Prioridad:** 1 (Crítico)
- **Rentadora:** Dollar
- **Modelo de pago:** Puntos + Plata (ejemplo 70% - según configuración)
- **Precondición:** Usuario autenticado con saldo de puntos suficiente
- **Pasos:**
  1. Login → Acceder al portal Promerica
  2. Navegar a tab "Autos"
  3. Seleccionar Recogida: "Miami International Airport (MIA)"
  4. **Validar:** Campo Recogida actualizado
  5. Clic en campo "Devolución"
  6. Escribir "JFK" en buscador del dropdown/modal
  7. **Validar:** Resultados filtrados para Nueva York JFK
  8. Seleccionar "John F. Kennedy Intl Airport (JFK)"
  9. **Validar:** Campo Devolución muestra "JFK"
  10. **Validar:** Sistema identifica dropoff diferente
  11. Seleccionar fechas: HOY + 10 días (10:00) a HOY + 11 días (10:00)
  12. **Validar:** Muestra "1 día de renta • Dropoff diferente"
  13. Clic en "Buscar"
  14. **Validar:** Redirección a Disponibilidad
  15. **Validar:** Widget persistente muestra "MIA → JFK • 1 día"
  16. **Validar:** Resultados incluyen recargo por dropoff diferente
  17. **Validar:** Modelo P+P disponible con precio actualizado
- **Resultado esperado:** Búsqueda exitosa con dropoff diferente y recargo aplicado
- **Título ADO:** `[PROM] Autos - Home - Búsqueda dropoff diferente - MIA a JFK - 1 día - Dollar - P+P`

**Escenario 3: Validación campos obligatorios**

- **Prioridad:** 1 (Crítico)
- **Precondición:** Usuario autenticado en el portal
- **Pasos:**
  1. Login → Navegar a Autos
  2. **NO** seleccionar recogida
  3. **Validar:** Botón "Buscar" deshabilitado (gris)
  4. Seleccionar Recogida: MIA
  5. **Validar:** Botón sigue deshabilitado (falta devolución)
  6. Seleccionar Devolución: MIA (mismo lugar)
  7. **Validar:** Botón sigue deshabilitado (faltan fechas)
  8. Seleccionar fechas: HOY + 5 a HOY + 6 (1 día)
  9. **Validar:** Botón "Buscar" ahora habilitado (verde)
- **Resultado esperado:** Sistema valida campos obligatorios correctamente
- **Título ADO:** `[PROM] Autos - Home - Validación campos obligatorios - MIA`

---

#### 🔹 Funcionalidad: Modal de Búsqueda por Localidades

##### 📖 Descripción Funcional

Modal emergente que permite buscar y seleccionar ubicaciones mediante campo de búsqueda, filtros de ciudades, lista de resultados y mapa interactivo sincronizado.

##### 🧩 Componentes

- **Título del Modal:** "Buscar por localidades"
- **Botón Cerrar (X):** Esquina superior derecha
- **Campo de Búsqueda:**
  - Barra de texto con ícono de ubicación (izquierda) y lupa (derecha)
  - Placeholder: "Empieza tu búsqueda"
- **Tabs/Filtros de Ciudades:**
  - Pestañas horizontales que aparecen cuando hay resultados
  - Nombres de ciudades con resultados disponibles
  - Tab activo con fondo verde
- **Contador de Resultados:**
  - Formato: "X Resultados" (ej: "17 Resultados")
- **Lista de Resultados:**
  - Panel scrollable con formato: Número | Nombre | Dirección | Botón "Seleccionar" (verde)
  - Ejemplo: "1. Miami Beach - 16901 SOUTH DIXIE HIGHWAY"
- **Mapa Interactivo:**
  - Sincronizado con lista de resultados
  - Marcadores en ubicaciones disponibles
  - Zoom y navegación habilitados
  - Powered by: mapbox, OpenStreetMap
- **Mensaje de Estado Vacío:**
  - "Lo sentimos, no hemos encontrado ningún resultado."
  - "Te recomendamos a buscar de nuevo con otra ciudad."

##### 💻 Comportamiento Esperado

- **Apertura:** Clic en "Recogida" o "Devolución" del widget principal
- **Búsqueda:** Usuario escribe ciudad/localidad → Sistema filtra en tiempo real
- **Resultados encontrados:** Aparecen tabs de ciudades, contador y lista de ubicaciones
- **Sincronización:** Hover en lista resalta marcador en mapa | Clic en marcador resalta item en lista
- **Filtros:** Clic en tab de ciudad actualiza lista y mapa con ubicaciones de esa ciudad
- **Selección:** Clic en botón "Seleccionar" → Cierra modal y actualiza campo correspondiente
- **Sin resultados:** Muestra mensaje de estado vacío (sin tabs ni lista)
- **Cerrar:** Botón X o clic fuera → Cierra sin cambios

##### ✅ VALIDACIONES DE QA

Estas validaciones deben incluirse en casos que involucren la selección de localidades (Recogida/Devolución).

- [ ] **VAL-AUT-HOME-003:** Modal de localidades abre correctamente
  - **Verificar:** Clic en "Recogida" o "Ver todas las localidades" abre modal con buscador

- [ ] **VAL-AUT-HOME-004:** Búsqueda por localidades filtra en tiempo real
  - **Verificar:** Al escribir ciudad, resultados se filtran en tiempo razonable

- [ ] **VAL-AUT-HOME-005:** Mapa sincronizado con lista
  - **Verificar:** Hover/clic en lista resalta marcador y clic en marcador resalta item correspondiente

##### 🧪 Escenarios de Prueba

**Escenario 9: Home - Modal de localidades - Búsqueda y sincronización mapa-lista**

- **Prioridad:** 2 (Alta)
- **Precondición:** Usuario autenticado y en tab "Autos"
- **Pasos:**
  1.  Clic en campo "Recogida" o en "Ver todas las localidades"
  2.  **Validar:** Se abre el modal con buscador y lista
  3.  Escribir un término de búsqueda (ej.: ciudad/aeropuerto)
  4.  **Validar:** La lista se filtra y el mapa se actualiza acorde
  5.  Hacer hover/clic sobre un resultado en la lista
  6.  **Validar:** El marcador correspondiente se resalta en el mapa
  7.  Clic en un marcador del mapa
  8.  **Validar:** El item correspondiente se resalta en la lista
  9.  Clic en "Seleccionar" en un resultado
  10. **Validar:** El modal se cierra y el campo de ubicación se actualiza
- **Resultado esperado:** El modal permite búsqueda, sincronización mapa-lista y selección sin inconsistencias
- **Título ADO:** `[PROM] Autos - Home - Modal localidades - Búsqueda y sincronización`

##### 🔗 Trazabilidad (VAL → Escenarios)

- **VAL-AUT-HOME-001, VAL-AUT-HOME-002:** Escenario 3
- **VAL-AUT-HOME-003, VAL-AUT-HOME-004, VAL-AUT-HOME-005:** Escenario 9
- **VAL-AUT-HOME-006:** Escenario 2
- **VAL-AUT-HOME-007, VAL-AUT-HOME-008:** Escenario 1 (y Escenario 2)

---

## 📋 MÓDULO: DISPONIBILIDAD

### 📋 Descripción del Módulo

Módulo que muestra los resultados de búsqueda de autos disponibles según los criterios del usuario. Incluye widget persistente, categorías, filtros y dos vistas (lista/matriz).

---

#### 🔄 Flujo de Interacción General

**Estado inicial al cargar el módulo (desde Home):**

1. **Elementos visibles:**
   - Widget de Búsqueda Persistente: VISIBLE (compacto con resumen de criterios)
   - Categorías de Vehículos: VISIBLE (pestañas horizontales con Standard seleccionado por defecto)
   - Filtros: VISIBLES en sidebar izquierdo (Tipo de auto, Rentadora, Transmisión)
   - Cards de Resultados: Listado principal visible en Vista Lista (por defecto)
   - Botones de Vista: Lista (activo) y Matriz (inactivo)

2. **Interacción del usuario - Secuencia típica:**
   - Usuario puede EDITAR criterios desde Widget Persistente → Nueva búsqueda
   - Usuario puede CAMBIAR categoría (Standard, Vans, SUV, etc.) → Filtrado inmediato
   - Usuario puede APLICAR filtros laterales (Rentadora, Transmisión) → Actualización en tiempo real
   - Usuario puede ALTERNAR entre Vista Lista y Vista Matriz → Cambio de visualización
   - Usuario puede OCULTAR widget persistente → Maximiza espacio para resultados

3. **Selección de vehículo:**
   - **Vista Lista:** Clic en card → Abre Modal de Protecciones → Seleccionar protección → Checkout
   - **Vista Matriz:** Clic en celda (precio) → Selecciona vehículo + rentadora + protección → Checkout directamente

4. **En módulo CHECKOUT:**
   - Usuario ve resumen de vehículo + protección seleccionada
   - Usuario completa datos del conductor y licencia
   - Usuario ajusta Slider Puntos + Plata (si aplica)
   - Usuario procede al pago

**Nota importante:** El Modal de Protecciones se documenta aquí porque es parte del journey de Disponibilidad, aunque también puede influir en el flujo de checkout.

---

### 🎨 FUNCIONALIDADES

#### 🔹 Funcionalidad: Widget de Búsqueda Persistente

##### 📖 Descripción Funcional

Widget expandible que muestra los criterios de búsqueda activos y permite modificarlos sin salir de la página de resultados. Puede colapsarse para maximizar espacio de visualización.

**Ubicación:** Parte superior del módulo Disponibilidad  
**Tipo de componente:** Widget colapsable/expandible con resumen de búsqueda  
**Estado inicial:** Expandido (muestra todos los campos)

##### 🧩 Componentes

1. **Toggle "Pago en línea":** Switch verde/gris para activar/desactivar pago en línea

2. **Campo "Recogida":**
   - Muestra ubicación seleccionada (ej: "Miami Intl (MIA)")
   - Ícono de ubicación
   - Clic abre selector de ubicación

3. **Campo "Devolución":**
   - Muestra ubicación de devolución (ej: "Miami Intl (MIA)")
   - Ícono de ubicación
   - Clic abre selector de ubicación

4. **Selector de Fechas:**
   - Muestra rango con formato: "Mié, Oct 22 - 12:00 - Sáb, Oct 25 - 12:45"
   - Ícono de calendario
   - Clic abre calendario con selectores de hora

5. **Campo "Ingresa tu código Hertz":**
   - Input de texto con placeholder: "Sin hertz Gold"
   - Opcional, permite códigos de descuento

6. **Campo "Selecciona tu descuento":**
   - Dropdown con placeholder: "Descuento"
   - Opciones de descuentos promocionales

7. **Botón "Buscar":** Botón verde para ejecutar nueva búsqueda

8. **Link "Ocultar búsqueda":** Texto pequeño en la esquina superior derecha para colapsar widget

##### 💻 Comportamiento Esperado

**Widget persistente:** Permanece visible mientras el usuario navega los resultados

**Edición de criterios:** Clic en cualquier campo permite modificar búsqueda sin perder contexto

**Botón "Buscar":** Actualiza resultados con nuevos criterios sin recargar página

**Ocultar/Mostrar:**

- Link "Ocultar búsqueda" → Colapsa widget a barra compacta con resumen mínimo
- Barra compacta muestra: "MIA → MIA • 3 días" + ícono expandir
- Clic en barra compacta → Expande widget completo nuevamente

**Persistencia:** Campos mantienen últimos valores ingresados durante la sesión

##### 📱 Variaciones Móviles

- **Estado inicial:** Colapsado, muestra barra compacta con resumen
- **Barra compacta:** "MIA → MIA • 3 días" con ícono de editar (✏️)
- **Expansión:** Tap en barra → Widget se expande en sección superior
- **Widget expandido:**
  - Ocupa ~40% superior de pantalla
  - Fondo blanco con separador visual
  - Campos apilados verticalmente
- **Campos de ubicación:** Tap abre modal de localidades en pantalla completa
- **Selector de fechas:** Calendario fullscreen con selectores de hora nativos
- **Códigos Hertz/Descuentos:** Secciones expandibles con tap
- **Botón "Buscar":**
  - Verde, ancho completo
  - Sticky en parte inferior del widget
- **Botón "Ocultar búsqueda":**
  - Link en esquina superior derecha
  - Colapsa widget a barra compacta
- **Gestos:** Swipe hacia arriba en barra colapsa (opcional según implementación)

##### ✅ VALIDACIONES DE QA

- [ ] **VAL-AUT-DISP-001:** Widget persistente muestra criterios correctos
  - **Verificar:** Recogida, devolución, fechas/horas y descuentos reflejan la búsqueda ejecutada

- [ ] **VAL-AUT-DISP-002:** Widget persistente permite editar criterios
  - **Verificar:** Clic en Recogida/Devolución/Fechas permite editar y al presionar "Buscar" actualiza resultados

- [ ] **VAL-AUT-DISP-009:** Widget puede colapsarse/expandirse
  - **Verificar:** Link "Ocultar búsqueda" colapsa widget; clic en barra compacta lo expande

- [ ] **VAL-AUT-DISP-010:** Barra compacta muestra resumen correcto
  - **Verificar:** Formato "Origen → Destino • X días" con datos correctos

##### 🧪 Escenarios de Prueba

**Escenario 7: Disponibilidad - Widget persistente - Editar criterios y refrescar resultados**

- **Prioridad:** 2 (Alta)
- **Precondición:** Usuario autenticado
- **Pasos:**
  1.  Login → Acceder al portal Promerica
  2.  Navegar a tab "Autos" y ejecutar una búsqueda válida
  3.  **Validar:** Widget persistente visible con criterios actuales
  4.  Clic en campo "Recogida" del widget persistente y seleccionar una ubicación diferente
  5.  Clic en "Buscar"
  6.  **Validar:** Resultados se actualizan según el nuevo criterio sin recargar la página
- **Resultado esperado:** El widget permite editar y refrescar resultados correctamente
- **Título ADO:** `[PROM] Autos - Disponibilidad - Widget persistente - Editar criterios`

---

#### 🔹 Funcionalidad: Categorías de Vehículos

##### 📖 Descripción Funcional

Navegación por pestañas para filtrar rápidamente por categoría de auto.

##### 🧩 Componentes

1. **Pestañas horizontales con íconos:**
   - 🚗 **Standard** (activo - borde verde)
   - 🚐 **Vans**
   - 🚙 **Suv**
   - 🏎️ **Luxury**
   - 🏁 **Adrenaline**
   - ⭐ **Prestige**
   - 💎 **Dream**
   - 🌿 **Green**

2. **Indicadores visuales:**
   - Pestaña activa: Fondo blanco con borde verde en parte inferior
   - Pestañas inactivas: Fondo gris claro
   - Ícono de vehículo representativo en cada pestaña

3. **Controles de vista (esquina superior derecha):**
   - 📋 **Botón Lista** (3 líneas horizontales)
   - 🔲 **Botón Matriz** (cuadrícula 2x2)
   - Botón activo en verde

##### 💻 Comportamiento Esperado

- **Clic en pestaña:** Filtra resultados por categoría seleccionada
- **Visual feedback:** Pestaña activa se destaca con borde verde
- **Cambio de vista:** Botones Lista/Matriz alternan visualización de resultados
- **Estado persistente:** Categoría seleccionada se mantiene al cambiar vista

##### 📱 Variaciones Móviles

- **Scroll horizontal:** Pestañas se desplazan horizontalmente con swipe táctil
- **Indicador de scroll:** Puntos o barra indica que hay más pestañas fuera de vista
- **Botones de vista reducidos:** Iconos más pequeños pero mantienen funcionalidad
- **Pestañas compactas:** Reducción de padding sin sacrificar legibilidad
- **Touch feedback:** Animación rápida al tocar pestaña

##### ✅ VALIDACIONES DE QA

- [ ] **VAL-AUT-DISP-003:** Categorías filtran resultados y conservan estado
  - **Verificar:** Clic en categoría cambia resultados y la categoría se mantiene al cambiar de vista Lista/Matriz

##### 🧪 Escenarios de Prueba

**Escenario 8: Disponibilidad - Categorías - Filtrado por pestañas y persistencia al cambiar vista**

- **Prioridad:** 3 (Media)
- **Precondición:** Usuario autenticado
- **Pasos:**
  1.  Login → Acceder al portal Promerica
  2.  Navegar a tab "Autos" y ejecutar una búsqueda válida
  3.  Seleccionar una categoría diferente (ej.: "Vans")
  4.  **Validar:** Resultados cambian según la categoría seleccionada
  5.  Cambiar a vista matriz (🔲) y volver a vista lista (📋)
  6.  **Validar:** La categoría seleccionada se mantiene activa tras el cambio de vista
- **Resultado esperado:** Las categorías filtran y mantienen estado al alternar vistas
- **Título ADO:** `[PROM] Autos - Disponibilidad - Categorías - Filtrado y persistencia`

---

#### 🔹 Funcionalidad: Filtros

##### 📖 Descripción Funcional

Panel lateral de filtros para refinar búsqueda de autos según tipo, rentadora y transmisión.

##### 🧩 Componentes

1. **Título de Sección:** "Filtros" (texto destacado)

2. **Filtro: Tipo de auto**
   - Dropdown con placeholder: "Todas"
   - Opciones: Standard, Intermediate, SUV, etc.
   - Ícono de flecha desplegable

3. **Filtro: Rentadora**
   - Dropdown con placeholder: "Todas"
   - Opciones: Hertz, Dollar, Thrifty, etc.
   - Ícono de flecha desplegable

4. **Filtro: Transmisión**
   - Dropdown con placeholder: "Todas"
   - Opciones: Automática, Manual
   - Ícono de flecha desplegable

**Diseño Visual:**

- Panel fijo en lado izquierdo de la pantalla
- Fondo blanco con bordes suaves
- Espaciado vertical entre filtros
- Dropdowns con borde gris claro y esquinas redondeadas

##### 💻 Comportamiento Esperado

- **Clic en dropdown:** Despliega lista de opciones disponibles
- **Selección:** Al elegir opción → Actualiza resultados en tiempo real
- **Múltiples filtros:** Se aplican de forma acumulativa (filtro AND)
- **Resetear:** Seleccionar "Todas" vuelve al estado inicial del filtro
- **Persistencia:** Los filtros se mantienen al cambiar entre vista lista/matriz

##### 📱 Variaciones Móviles

- **Botón flotante "Filtros":** Ícono flotante (🔽) en esquina inferior derecha
- **Panel modal:** Filtros como modal/sheet desde el fondo (70-80% altura)
- **Filtros apilados verticalmente:** Cada filtro ocupa ancho completo
- **Dropdowns nativos:** Utilizan selectores nativos del sistema operativo
- **Contador de filtros activos:** Badge numérico en botón flotante
- **Botones de acción:** "Limpiar filtros" y "Aplicar" (verde) en parte inferior
- **Cerrar modal:** Swipe hacia abajo o tap en overlay oscuro

##### ✅ VALIDACIONES DE QA

- [ ] **VAL-AUT-DISP-004:** Filtros laterales aplican de forma acumulativa
  - **Verificar:** Tipo de auto + rentadora + transmisión aplican AND; seleccionar "Todas" resetea

##### 🧪 Escenarios de Prueba

**Escenario 4: Disponibilidad - Filtros acumulativos por rentadora y transmisión**

- **Prioridad:** 2 (Alta)
- **Precondición:** Usuario autenticado
- **Pasos:**
  1.  Login → Acceder al portal Promerica
  2.  Navegar a tab "Autos"
  3.  Ejecutar una búsqueda válida (recogida, devolución, fechas)
  4.  **Validar:** Se muestra módulo Disponibilidad y el widget persistente
  5.  En filtros, seleccionar una **Rentadora** (ej.: Hertz)
  6.  Seleccionar **Transmisión** (ej.: Automática)
  7.  **Validar:** Resultados se actualizan dinámicamente (sin recargar página)
  8.  Cambiar el filtro de Rentadora a "Todas"
  9.  **Validar:** Resultados vuelven a incluir múltiples rentadoras
- **Resultado esperado:** Filtros se aplican acumulativamente y se pueden resetear
- **Título ADO:** `[PROM] Autos - Disponibilidad - Filtros acumulativos - Rentadora + Transmisión`

---

#### 🔹 Funcionalidad: Cards de Resultados (Vista Lista)

##### 📖 Descripción Funcional

Tarjetas individuales que muestran información detallada de cada vehículo disponible.

##### 🧩 Componentes (por cada card)

1. **Ícono de información (i):** Esquina superior izquierda del card

2. **Imagen del vehículo:** Foto lateral del auto en alta resolución

3. **Categoría y Modelo:**
   - Título: "Economic" | "Compact" | "Intermediate" (negrita)
   - Subtítulo: "Ford Focus o Similar" (gris)

4. **Especificaciones con íconos:**
   - 👤 **Pasajeros:** Número (ej: 4)
   - 🚪 **Puertas:** Número (ej: 4)
   - 🧳 **Maletas:** Número (ej: 2)
   - ❄️ **A/C:** Ícono de aire acondicionado
   - ⚙️ **Transmisión:** Ícono de automático (A)

5. **Precio:**
   - Label: "Desde" (pequeño, parte superior derecha)
   - Precio: "USD $300" (grande, negrita)
   - ⚠️ **Nota (según configuración):** La visualización del precio bajo modelo Puntos + Plata puede variar (pendiente confirmar si se presenta en card)

6. **Logos de Rentadoras:**
   - Badges rectangulares con logos: Thrifty, Dollar, Hertz
   - Alineados horizontalmente en la parte inferior

**Diseño Visual:**

- Card con borde gris claro y sombra suave
- Espaciado uniforme entre elementos
- Íconos en color gris/negro con estilo minimalista
- Logos de rentadoras con bordes redondeados

##### 💻 Comportamiento Esperado

- **Hover en card:** Sombra más pronunciada o borde destacado
- **Clic en ícono (i):** Muestra tooltip con información adicional del vehículo
- **Clic en card completo:** Abre modal de selección de protecciones/seguros
- **Clic en logo rentadora:** Filtra resultados por esa compañía específica
- **Scroll:** Carga lazy de cards adicionales conforme usuario navega

##### 📱 Variaciones Móviles

- **Cards apiladas verticalmente:** Ocupan ancho completo con scroll vertical
- **Imagen más pequeña:** Proporción reducida para optimizar espacio
- **Layout reorganizado:** Información en dos columnas (specs izquierda, precio derecha)
- **Logos de rentadoras:** Lista horizontal scrollable si son muchos
- **Precio más prominente:** Tamaño aumentado para mejor visibilidad
- **Touch targets:** Áreas de toque más grandes para botones

##### ✅ VALIDACIONES DE QA

- [ ] **VAL-AUT-DISP-005:** Cards muestran información mínima requerida
  - **Verificar:** Categoría/modelo, specs (👤, 🚪, 🧳, ❄️A/C, ⚙️), precio y logos de rentadora

- [ ] **VAL-AUT-DISP-006:** Clic en card abre modal de protecciones
  - **Verificar:** Clic en card de vehículo abre el modal con info del vehículo y opciones de protección

##### 🧪 Escenarios de Prueba

**Escenario 10: Disponibilidad - Cards - Filtrado por logo de rentadora**

- **Prioridad:** 3 (Media)
- **Precondición:** Usuario autenticado y con resultados en Disponibilidad
- **Pasos:**
  1.  Identificar una card que muestre múltiples logos de rentadora
  2.  Clic en el logo de una rentadora (ej.: Hertz)
  3.  **Validar:** Los resultados se filtran para mostrar únicamente esa rentadora
  4.  Clic en el ícono de información (i) de una card
  5.  **Validar:** Se muestra tooltip con información adicional del vehículo
- **Resultado esperado:** El logo filtra resultados y el tooltip se presenta correctamente
- **Título ADO:** `[PROM] Autos - Disponibilidad - Cards - Filtrado por rentadora`

---

#### 🔹 Funcionalidad: Vista Matriz de Comparación

##### 📖 Descripción Funcional

Visualización alternativa que muestra múltiples vehículos en formato de tabla comparativa con precios por rentadora.

##### 🧩 Componentes

1. **Encabezado de Vehículos (3 columnas):**
   - Cada columna incluye:
     - Imagen del vehículo
     - Categoría (negrita)
     - Modelo (gris)
     - Especificaciones con íconos (👤 | 🚪 | 🧳 | ❄️A/C | ⚙️A)
     - Precio desde (ejemplo: "USD $300")

2. **Banner de Comparación de Precios:**
   - Texto de comparación
   - Fondo verde oscuro
   - Ubicación: debajo de los encabezados de vehículos

3. **Tabla de Protecciones por Rentadora:**
   - Fila de encabezados por tipo de protección (ej.: "Solo auto", "Protección Básica", "Protección Básica Plus", "Protección Full")
   - Íconos de información (❓) por tipo de protección
   - Filas por rentadora con logo + precios por celda

4. **Indicadores Visuales:**
   - Badge "Recomendado" (cuando aplique)
   - Bordes sutiles entre celdas

##### 💻 Comportamiento Esperado

- **Activación:** Clic en botón de vista matriz (🔲) en controles superiores
- **Cambio de vista:** Transición suave entre vista lista y vista matriz
- **Selección de celda:** Clic en cualquier precio selecciona vehículo + rentadora + protección
- **Ícono info (❓):** Hover o clic muestra tooltip con descripción de coberturas incluidas
- **Filtros activos:** Se mantienen al cambiar entre vista lista/matriz
- **Flujo:** Selección de celda → Redirige a Checkout con configuración completa (vehículo + rentadora + protección)

##### 📱 Variaciones Móviles

- Scroll horizontal para ver todas las columnas
- Encabezados de vehículos sticky (se mantienen visibles al scrollear)

##### ✅ VALIDACIONES DE QA

- [ ] **VAL-AUT-DISP-008:** Vista Matriz permite selección por celda
  - **Verificar:** Clic en precio/celda selecciona vehículo+rentadora+protección y redirige a Checkout

##### 🧪 Escenarios de Prueba

**Escenario 6: Disponibilidad - Vista matriz selecciona configuración por celda**

- **Prioridad:** 2 (Alta)
- **Precondición:** Usuario autenticado
- **Pasos:**
  1.  Login → Acceder al portal Promerica
  2.  Navegar a tab "Autos" y ejecutar una búsqueda válida
  3.  En controles superiores, activar vista matriz (🔲)
  4.  **Validar:** Se muestra tabla comparativa con rentadoras y tipos de protección
  5.  Clic en una celda de precio
  6.  **Validar:** Sistema selecciona vehículo + rentadora + protección y continúa a Checkout
- **Resultado esperado:** Vista matriz permite selección directa por celda
- **Título ADO:** `[PROM] Autos - Disponibilidad - Selección vista matriz - Por celda`

---

#### 🔹 Funcionalidad: Modal de Protecciones y Seguros

##### 📖 Descripción Funcional

Modal emergente que se activa al seleccionar un vehículo, permitiendo al usuario elegir entre diferentes niveles de protección y cobertura antes de continuar al checkout.

##### 🧩 Componentes

1. **Información del Vehículo (Header del modal):**
   - Categoría y modelo (ejemplo)
   - Especificaciones: 👤 | 🚪 | 🧳 | ❄️A/C | ⚙️A
   - Precio base (ejemplo)

2. **Opciones de Protección (4 cards):**
   - "Solo Auto"
   - "Protección Básica"
   - "Protección Básica Plus" (puede estar marcada como ⭐ Recomendado)
   - "Protección Full"
   - Cada opción presenta: lista de coberturas (bullets), precio (ejemplo) y botón "Ver detalle"

##### 💻 Comportamiento Esperado

- **Apertura:** Se activa al hacer clic en cualquier card de vehículo (vista lista)
- **Selección:** Clic en el card de una protección (excepto "Ver detalle") selecciona la opción y cierra el modal
- **Ver detalle:** Expande descripción completa de coberturas sin cerrar el modal
- **Cierre:** Clic fuera del modal o botón X (si existe) cierra sin seleccionar
- **Flujo:** Selección de protección → Redirige a Checkout con vehículo + protección elegida

##### ✅ VALIDACIONES DE QA

- [ ] **VAL-AUT-DISP-007:** Selección de protección continúa a Checkout
  - **Verificar:** Seleccionar una opción (excepto "Ver detalle") cierra modal y continúa el flujo con la selección aplicada

##### 🧪 Escenarios de Prueba

**Escenario 5: Disponibilidad - Selección en vista lista abre modal y continúa a Checkout**

- **Prioridad:** 1 (Crítico)
- **Precondición:** Usuario autenticado
- **Pasos:**
  1. Login → Acceder al portal Promerica
  2. Navegar a tab "Autos" y ejecutar una búsqueda válida
  3. **Validar:** Cards de resultados visibles
  4. Clic en un card de vehículo
  5. **Validar:** Se abre el Modal de Protecciones y Seguros
  6. Clic en una opción de protección (no en "Ver detalle")
  7. **Validar:** Modal se cierra
  8. **Validar:** El flujo continúa a Checkout con vehículo + protección seleccionada
- **Resultado esperado:** Selección en card → modal → checkout sin inconsistencias
- **Título ADO:** `[PROM] Autos - Disponibilidad - Selección vista lista - Modal protecciones`

##### 🔗 Trazabilidad (VAL → Escenarios)

- **VAL-AUT-DISP-001, VAL-AUT-DISP-002, VAL-AUT-DISP-009, VAL-AUT-DISP-010:** Escenario 7
- **VAL-AUT-DISP-003:** Escenario 8
- **VAL-AUT-DISP-004:** Escenario 4
- **VAL-AUT-DISP-005:** Escenario 10
- **VAL-AUT-DISP-006, VAL-AUT-DISP-007:** Escenario 5
- **VAL-AUT-DISP-008:** Escenario 6

---

#### 🔹 Funcionalidad: Slider Puntos + Plata

##### 📋 Referencia al Knowledge Base

> **📖 Documentación Completa:** [Knowledge_Base_Promerica.md - Modelo de Pago Slider Puntos + Plata](../../../../documentation/knowledge-bases/Knowledge_Base_Promerica.md#modelo-de-pago-slider-puntos--plata)

**Para casos de prueba del Slider en Autos, consultar el Knowledge Base para:**

- Descripción funcional completa
- Componentes del slider (visual, labels, displays)
- Comportamiento esperado (cálculos en tiempo real, validaciones automáticas)
- Estados del sistema (normal, error saldo, loading)
- Ejemplos de cálculo con diferentes porcentajes
- Validaciones de QA específicas del slider
- Escenarios de prueba detallados (ajuste exitoso, bloqueo por saldo)

**Resumen rápido:**

- **Función:** Ajustar dinámicamente proporción Puntos/Plata para pago de auto
- **Ubicación:** ⚠️ Pendiente confirmar (¿cards de resultados, modal de protecciones, checkout?)
- **Validación:** Tiempo real de saldo disponible
- **Rango:** Mínimo configurable hasta 100% puntos

**⚠️ Importante:**

- **Pendiente confirmar:** Ubicación exacta del slider en el flujo de autos
- **Pendiente confirmar:** Si aparece en disponibilidad o solo en checkout
- El slider es una funcionalidad transversal crítica del modelo de negocio Promerica
- Referirse siempre al Knowledge Base para información actualizada sobre tasas de conversión, porcentajes mínimos y reglas de negocio

---

## 💳 MÓDULO: CHECKOUT

> ⚠️ **Documentación en proceso**  
> Este módulo está siendo estandarizado. Se está trabajando en la documentación de: Datos del conductor, Licencia de conducir, Seguros y protecciones, Métodos de pago, Resumen de reserva.  
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
✅ Campos obligatorios: Recogida, devolución, fechas con horas  
✅ Botón buscar: Habilitado solo con campos completos  
✅ Fechas: No permite selección de fechas pasadas  
✅ Horas: Validación de rango lógico (recogida antes de devolución)  
✅ Modal de localidades: Búsqueda en tiempo real, sincronización mapa-lista  
✅ Descuentos: Opcionales, formato de código validado

**Disponibilidad:**
✅ Widget persistente: Resumen correcto de criterios de búsqueda  
✅ Categorías: Filtrado dinámico al cambiar pestaña  
✅ Filtros laterales: Actualización en tiempo real sin recargar  
✅ Vista Lista: Cards con toda información necesaria  
✅ Vista Matriz: Comparación lado a lado  
✅ Carga lazy: Resultados adicionales al hacer scroll

**Checkout:**
✅ **Validación completa permitida con múltiples días (3, 5, 7 días)** - No genera costos hasta confirmar
⚠️ Pendiente documentar: Datos conductor, licencia, seguros, métodos de pago

**Confirmación:**
🚨 **CRÍTICO: Ejecutar SOLO con búsquedas de 1 día** - Reservas confirmadas generan costos reales
⚠️ Pendiente documentar: Código de reserva, voucher, manejo de errores
⚠️ Validar proceso de cancelación para mitigar riesgos

**Admin:**
⚠️ Pendiente documentar: Reserva localizable, estados de procesamiento
⚠️ Validar funcionalidad de cancelación de reservas confirmadas

### Validaciones Específicas del Modelo Slider (Puntos + Plata):

⚠️ **PENDIENTE CONFIRMAR:** ¿El slider aparece en disponibilidad como en vuelos?  
⚠️ **PENDIENTE CONFIRMAR:** ¿Ubicación exacta del slider (cards, detalle, checkout)?  
⚠️ **PENDIENTE CONFIRMAR:** Porcentaje mínimo de puntos requerido  
✅ **Validación de saldo:** Sistema debe verificar puntos disponibles  
✅ **Solicitud de pago:** Si hay copago en plata, se requiere método de pago  
⚠️ **PENDIENTE CONFIRMAR:** Tipo de emisión (automática/manual)

### Validaciones de Experiencia de Usuario (UI/UX):

✅ **Modal de localidades:** Experiencia fluida de búsqueda y selección  
✅ **Calendario:** Selectores de hora/minuto intuitivos  
✅ **Responsive:** Adaptación correcta a móviles (sticky buttons, modals fullscreen)  
✅ **Estados de carga:** Indicadores visuales durante búsqueda/filtrado  
✅ **Sincronización mapa-lista:** Hover y clic mantienen coherencia visual  
✅ **Mensajes de error:** Claros y orientados a acción del usuario  
✅ **Accesibilidad:** Componentes navegables por teclado y lectores de pantalla

---

## 📝 FORMATO DE TÍTULO

```
[PROM] Autos - [Módulo/Escenario] - [Variante]
```

**Ejemplos actualizados:**

- `[PROM] Autos - Home - Búsqueda mismo lugar - MIA a MIA - 1 día - P+P`
- `[PROM] Autos - Disponibilidad - Filtros acumulativos - Rentadora + Transmisión`
- `[PROM] Autos - Disponibilidad - Selección vista lista - Modal protecciones`

---

## 🚀 PRÓXIMOS PASOS PARA COMPLETAR ESTE ARCHIVO

### Módulos Documentados:

✅ **Componentes Transversales** - Referencia a vuelos (Header, Tabs, Footer)  
✅ **Pasos Obligatorios del Flujo E2E** - 25 pasos documentados (pasos 1-16 completos, 17-25 pendientes)  
✅ **Módulo Home/Login** - Widget de búsqueda con 7 componentes + Modal de localidades  
✅ **Módulo Disponibilidad** - 6 funcionalidades: Widget persistente, Categorías, Filtros, Cards Lista, Vista Matriz, Modal de Protecciones

### Módulos Pendientes:

**1. Disponibilidad - Completar:**

- Detalle expandido del vehículo
- Slider Puntos + Plata (ubicación y comportamiento)

**2. Checkout:**

- Resumen de reserva
- Formulario de datos del conductor
- Licencia de conducir (validación y carga)
- Seguros y protecciones seleccionables
- Conductores adicionales
- Métodos de pago (integración con gateway)
- Términos y condiciones
- **✅ Permitido probar con 3, 5, 7 días sin confirmar**

**3. Confirmación:**

- 🚨 **RESTRICCIÓN: Probar SOLO con 1 día de renta**
- Confirmación exitosa (código de reserva, voucher PDF)
- Email de confirmación automático
- Manejo de errores (tipos, mensajes, acciones de recuperación)
- **Proceso de cancelación de reservas (prioritario documentar)**

**4. Admin:**

- Validación de reserva en backend
- Estados de procesamiento
- Voucher disponible o no
- **Funcionalidad de cancelación (mitigar costos)**

### Información de Negocio Pendiente:

**Proveedores:**

- Confirmar lista completa (Sabre → Hertz, Dollar, Thrifty confirmados)
- Identificar diferencias funcionales por rentadora
- Validar disponibilidad por país (CR, PA, HN, DO, GT, SV, NI)

**Reglas del Slider:**

- ⚠️ **CRÍTICO:** Confirmar si aplica slider en autos como en vuelos
- Porcentaje mínimo de puntos requerido
- Fórmula de cálculo Puntos ↔ Plata por rentadora
- Ubicación del slider (disponibilidad, detalle, checkout)

**Políticas de Producto:**

- Edad mínima/máxima del conductor
- Requisitos de licencia de conducir
- Políticas de combustible
- Seguros incluidos vs opcionales
- Conductores adicionales (límites y costos)
- Políticas de cancelación

**Proceso de Reserva:**

- Definir si emisión es automática o manual
- Tiempos de confirmación esperados
- Estados de reserva durante el proceso
- Disponibilidad de voucher
- **🚨 Proceso de cancelación de reservas confirmadas (prioritario para QA)**
- **Política de reembolso de puntos si se cancela**

**Estrategia de Pruebas:**

- **Flujo Checkout (pasos 1-20):** Probar con **3, 5, 7 días** - Cobertura completa sin riesgo
- **Flujo Confirmación (pasos 21-25):** Probar **SOLO con 1 día** - Minimizar costos reales
- **Casos de regresión:** Priorizar pruebas hasta checkout con múltiples escenarios de días
- **Casos de smoke:** Incluir confirmación con 1 día para validar integración completa

---

## 📚 REFERENCIAS

**Guías relacionadas:**

- [SHARED_QA_RULES.md](../../../../shared/SHARED_QA_RULES.md) - Fundamentos ISTQB y Azure DevOps
- [PROM_COMMON_RULES.md](../../../../shared/Reglas Marketplace/PROM_COMMON_RULES.md) - Reglas comunes Promerica
- [PROM_VUELOS.md](PROM_VUELOS.md) - Referencia para estructura y componentes transversales

---

## 🔄 CONTROL DE CAMBIOS

### Versión 1.1 - 2026-02-03

**Cambios principales:**

- ✅ **Módulo Disponibilidad:** Agregado Flujo de Interacción General con estados iniciales
- ✅ **Actualizado:** Widget de Búsqueda Persistente con funcionalidad colapsable/expandible
- ✅ **Completado:** Variaciones Móviles en Widget Persistente (gestos, estados, expansión)
- ✅ **Agregado:** Referencia al Slider Puntos + Plata en Knowledge Base
- ✅ **Nuevas validaciones:** VAL-AUT-DISP-009 (colapsar/expandir) y VAL-AUT-DISP-010 (barra compacta)
- ✅ **Actualizado:** Trazabilidad de validaciones a escenarios
- ✅ Total funcionalidades documentadas: 6 (Widget Persistente, Categorías, Filtros, Cards Lista, Vista Matriz, Modal Protecciones)

### Versión 1.0 - 2026-01-25

**Cambios principales:**

- ✅ Aplicada arquitectura híbrida (propósito dual: humanos + agente QA)
- ✅ Reorganizada jerarquía según estructura estándar de productos
- ✅ Módulo Home/LOGIN con estructura completa:
  - 📖 Descripción Funcional
  - 🧩 Componentes (tabla estructurada)
  - 💻 Comportamiento Esperado
  - ✅ Validaciones de QA (8 validaciones)
  - 🧪 Escenarios de Prueba (4 escenarios detallados)
- ✅ Módulo Disponibilidad con 6 funcionalidades documentadas
- ✅ Escenarios E2E con rutas reales:
  - **MIA → MIA:** Miami mismo lugar (Hertz, Thrifty)
  - **MIA → JFK:** Miami a Nueva York dropoff diferente (Dollar)
- ✅ Todos los escenarios con 1 día de renta, 1 conductor, modelo P+P
- ✅ Variaciones por rentadora: Hertz, Dollar, Thrifty
- ✅ Formato optimizado para generación de casos por agente
- ✅ Información completa para consulta humana

### Versión 0.3 - 2026-01-23

**Cambios principales:**

- ✅ Agregada URL Test Costa Rica (CR)
- ✅ Confirmado modelo de negocio: Puntos + Plata (Slider)
- ✅ Referenciados Componentes Transversales (ver PROM_VUELOS.md)
- ✅ Documentado Módulo Home/Login completo (Widget búsqueda con 7 componentes + Modal localidades)
- ✅ Documentado Módulo Disponibilidad (Widget persistente, Categorías, Filtros, Cards Lista, Vista Matriz parcial)
- ✅ Agregados Pasos Obligatorios del Flujo E2E (25 pasos)
- ✅ Aplicada jerarquía de títulos consistente (H1 → H2 → H3)
- ✅ Eliminadas duplicaciones entre secciones
- ✅ Consolidadas Validaciones Críticas por módulo
- ✅ Reorganizados Próximos Pasos en categorías lógicas
- 🚨 **Agregada restricción crítica de días:** Checkout con múltiples días permitido | Confirmación SOLO con 1 día
- ✅ Identificado proceso de cancelación como prioritario para mitigar costos

### Versión 0.2 - 2026-01-20

**Cambios principales:**

- ✅ Identificado modelo de negocio B2B2C Transversal
- ✅ Agregados 7 países soportados (CR, PA, HN, DO, GT, SV, NI)

### Versión 0.1 - 2026-01-20

**Cambios principales:**

- ✅ Template inicial creado con estructura base
- ✅ Definidas secciones principales del documento
