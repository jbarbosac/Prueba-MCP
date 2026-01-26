# 🎡 PRODUCTO: DISNEY - PROMERICA REWARDS

> **📖 Información Global:** Ver [PROM_QA_Assistant.agent.md](../../../../agents/PROM_QA_Assistant.agent.md) para URL del portal, país activo, modelo de negocio y versión del marketplace.

---

## 📌 Descripción General

El producto **Disney** permite a los usuarios del programa Promerica Rewards buscar, seleccionar y reservar tickets para parques temáticos de Disney utilizando el modelo de pago híbrido **Puntos + Plata (Slider)**. El sistema integra proveedores especializados en tickets Disney, ofreciendo opciones de tickets base, Park Hopper y Park Hopper Plus con selección flexible de parques y fechas.

**Características principales:**
- Selección de parques Disney (Magic Kingdom, Epcot, Hollywood Studios, Animal Kingdom)
- Múltiples tipos de tickets (Base, Park Hopper, Park Hopper Plus)
- Selección de fechas de visita (1 día o múltiples días)
- Configuración de visitantes por rangos de edad Disney
- Modelo de pago flexible con slider Puntos + Plata
- Vouchers digitales bilingües con códigos QR

---

## 📦 CONTEXTO OPERATIVO

### Proveedores Disponibles

⚠️ **PENDIENTE CONFIRMAR PARA PROMERICA**

**Proveedores conocidos en otros modelos:**

- **DerbySoft** (usado en Pichincha Miles)
- **OffLine** (usado en BGR Miles)

⚠️ **Acción requerida:** Validar cuál proveedor utiliza Promerica Rewards

### Componentes Transversales

> **Nota:** Estos componentes son compartidos por todos los productos del marketplace (Vuelos, Autos, Hoteles, **Disney**, Actividades). Ver detalle completo en [PROM_VUELOS.md](PROM_VUELOS.md#-componentes-transversales).

#### Header Global

Barra superior con navegación principal, branding personalizado de Promerica y acceso de usuario.

#### Tabs de Productos

Pestañas horizontales para navegación entre productos (Vuelos, Autos, Hoteles, **Disney**, Actividades).

#### Footer Global

Sección inferior con información institucional y canales de contacto personalizados por país.

### Flujo E2E Obligatorio

**Estos pasos deben incluirse en todos los casos de prueba para asegurar trazabilidad completa:**

1. **Acceder al portal** → https://traveltest-club-promerica.preprodppm.com/es-cr | El portal carga correctamente y muestra la pantalla de inicio
2. **Realizar login** → Ingresar usuario y contraseña válidos | Login exitoso y acceso al home con tabs de productos visibles
3. **Navegar a Disney** → Clic en tab "Disney" | Widget de búsqueda/selección de Disney se muestra correctamente
4. **Seleccionar parque(s)** → Clic en selector de parques o checkboxes | ⚠️ Pendiente documentar: ¿Dropdown, checkboxes múltiples, o cards?
5. **Confirmar parque(s) seleccionado(s)** → Seleccionar uno o múltiples parques según tipo de ticket | Sistema valida selección
6. **Seleccionar fechas de visita** → Clic en campo "Fechas" o calendario | Calendario se abre
7. **Confirmar rango de fechas** → Seleccionar fecha inicio (y fecha fin si son múltiples días) | Calendario se cierra y campo muestra fechas
8. **Seleccionar tipo de ticket** → Clic en dropdown "Tipo de ticket" | ⚠️ Pendiente documentar: Opciones (Base, Hopper, Hopper Plus)
9. **Confirmar tipo de ticket** → Seleccionar opción deseada | Campo se actualiza con tipo seleccionado
10. **Configurar visitantes** → Clic en campo "Visitantes" o "Personas" | Dropdown de visitantes se abre
11. **Ajustar cantidades por edad** → Seleccionar adultos y niños según rangos de edad | ⚠️ Pendiente documentar rangos de edad Disney
12. **Confirmar visitantes** → Clic en "Listo" o fuera del dropdown | Dropdown se cierra y campo muestra resumen (ej: "2 adultos, 1 niño")
13. **Ejecutar búsqueda** → Clic en botón "Buscar" o "Ver opciones" verde | Sistema redirige a módulo de Disponibilidad/Opciones
14. **Revisar opciones de tickets disponibles** → ⚠️ Pendiente documentar vista de disponibilidad | ⚠️ Pendiente documentar si muestra diferentes proveedores
15. **Ver detalle de ticket** → Clic en opción de ticket | ⚠️ Pendiente documentar: ¿Abre modal o expande información?
16. **Ajustar slider Puntos + Plata** → ⚠️ Pendiente documentar ubicación del slider | ⚠️ Pendiente documentar validación de saldo
17. **Seleccionar ticket** → Clic en botón "Seleccionar" o "Continuar" | Sistema valida selección
18. **Continuar a Checkout** → Clic en botón de confirmación | ⚠️ Pendiente documentar validaciones de checkout
19. **Completar datos de visitantes** → Llenar formulario con información de cada visitante | ⚠️ Pendiente documentar campos específicos (nombre, edad, país)
20. **Agregar información de contacto** → Ingresar email y teléfono | ⚠️ Pendiente documentar validaciones
21. **Seleccionar método de pago** → Ingresar datos de tarjeta si hay copago en plata | ⚠️ Pendiente documentar proceso de pago
22. **Confirmar reserva** → Clic en botón de confirmación final | ⚠️ Pendiente documentar proceso de emisión
23. **Validar confirmación** → Verificar código de reserva, voucher | ⚠️ Pendiente documentar datos mostrados
24. **Verificar voucher en Admin** → Buscar reserva en aplicativo Admin | ⚠️ Pendiente documentar: Voucher disponible (PDF bilingüe típicamente)
25. **Validar información del voucher** → ⚠️ Pendiente documentar: Parques, fechas, nombres visitantes, QR, instrucciones | ⚠️ Pendiente documentar idiomas

**Nota:** Los pasos 14-25 están pendientes de documentación completa según información de módulos Disponibilidad, Detalle, Checkout, Confirmación y Admin.

---

## 🏠 MÓDULO: HOME/LOGIN

### 📋 Descripción del Módulo

Página principal del marketplace donde el usuario accede al selector/buscador de tickets Disney y navega entre productos disponibles. La interfaz es personalizable según el país configurado (Costa Rica en Test). Este módulo proporciona selección de parques, fechas de visita, tipos de tickets y configuración de visitantes.

### 🎨 FUNCIONALIDADES

#### 🔹 Funcionalidad: Widget de Selección de Tickets Disney

##### 📖 Descripción Funcional

Formulario principal para configurar tickets de Disney con selectores de parques, fechas, tipo de ticket y visitantes. Permite selección flexible según el tipo de ticket elegido y valida configuraciones antes de buscar opciones disponibles.

**Ubicación:** Centro de la página de inicio, debajo del header y tabs de productos  
**Tipo de componente:** Formulario interactivo con selectores especializados  
**Acceso:** Disponible para todos los usuarios autenticados

⚠️ **IMPORTANTE:** La interfaz exacta de Disney puede variar significativamente según el proveedor (DerbySoft vs OffLine). Documentamos estructura genérica hasta confirmar proveedor específico.

##### 🧩 Componentes

1. **Selector de Parques:**
   - Formato: ⚠️ Pendiente confirmar (Dropdown, Checkboxes, o Cards)
   - Opciones: Magic Kingdom, Epcot, Hollywood Studios, Animal Kingdom
   - Selección: Única (Base) o múltiple (Hopper/Hopper Plus) según tipo de ticket

2. **Selector de Fechas:**
   - Campo con ícono de calendario
   - Placeholder: "Selecciona tus fechas"
   - Comportamiento: Fecha única (1 día) o rango (múltiples días)
   - Clic abre calendario mensual interactivo

3. **Selector "Tipo de Ticket":**
   - Dropdown o Radio buttons
   - Opciones esperadas:
     - Base (un parque por día)
     - Park Hopper (múltiples parques por día)
     - Park Hopper Plus (múltiples parques + parques acuáticos)
   - ⚠️ Pendiente confirmar opciones disponibles en Promerica

4. **Selector "Visitantes":**
   - Campo con ícono de personas
   - Placeholder: "Visitantes"
   - Clic abre dropdown con controles +/- por rango de edad Disney
   - Muestra resumen: "X adulto(s), Y niño(s)"

5. **Botón "Buscar"/"Ver Opciones":**
   - Color: Verde institucional (#00563F)
   - Texto: "Buscar" en blanco, centrado
   - Estado deshabilitado (gris) si faltan campos obligatorios
   - Habilitado (verde) cuando todos los campos están completos

##### 💻 Comportamiento Esperado

**Interacción con selector de parques:**
- Selección condicional según tipo de ticket seleccionado:
  - **Base:** Permite seleccionar 1 solo parque
  - **Park Hopper:** Permite seleccionar múltiples parques (checkbox múltiple)
  - **Park Hopper Plus:** Múltiples parques + acceso a parques acuáticos
- Formato de selector ajusta según proveedor confirmado (Dropdown, Checkboxes, o Cards)
- Cambiar tipo de ticket resetea selección de parques si la selección actual es incompatible

**Interacción con selector de fechas (Calendario Disney):**
- Clic en campo abre calendario mensual interactivo
- **Componentes del calendario:**
  - Navegación de mes/año: Flechas < > para cambiar mes, selector de mes y año en encabezado
  - Vista desktop (según UI): Calendario dual (dos meses lado a lado)
  - Grilla de días: Días de la semana (L, M, M, J, V, S, D), días del mes con estado visual
  - Indicadores visuales:
    - Día actual destacado
    - Fechas pasadas deshabilitadas (gris)
    - Fecha inicio seleccionada (verde)
    - Rango seleccionado (verde claro) si son múltiples días
    - Fecha fin seleccionada (verde)
  - Botones de acción: "Cancelar" (cierra sin cambios) y "Aceptar" (verde, confirma selección)
- **Comportamiento de selección:**
  - **1 día:** Un solo clic selecciona fecha única
  - **Múltiples días:** Primer clic = fecha inicio, segundo clic = fecha fin, muestra rango visual entre fechas
- **Validaciones:**
  - No permite fechas pasadas (botón bloqueado/gris)
  - Si son múltiples días, fecha fin debe ser posterior a fecha inicio
- ⚠️ Pendiente confirmar si muestra disponibilidad/precios por fecha
- Botón "Cancelar" cierra calendario sin aplicar cambios
- Botón "Aceptar" actualiza campo principal y cierra calendario

**Interacción con tipo de ticket:**
- Dropdown o Radio buttons según proveedor confirmado
- Opciones esperadas:
  - **Base:** Un parque por día
  - **Park Hopper:** Múltiples parques el mismo día
  - **Park Hopper Plus:** Múltiples parques + parques acuáticos
- Selección de tipo afecta:
  - Opciones de parques disponibles (1 o múltiples)
  - Precio final del ticket
  - Restricciones de visita
- Cambiar tipo de ticket condiciona selector de parques

**Interacción con selector de visitantes (Dropdown Visitantes Disney):**
- Clic en campo abre dropdown/modal con controles de cantidad por edad
- **Controles por categoría de edad:**
  - **Adultos:** (mayores de 10 años)
    - Label: "Adultos" (mayores de 10 años)
    - Controles: Botón "-" | Número | Botón "+"
    - Rango: Mínimo 1, máximo ⚠️ por definir
  - **Niños:** (de 3 a 9 años)
    - Label: "Niños" (de 3 a 9 años)
    - Controles: Botón "-" | Número | Botón "+"
    - Rango: Mínimo 0, máximo ⚠️ por definir
    - ⚠️ Pendiente validar si requiere edad específica de cada niño
  - **Menores de 3 años (entrada gratuita):** No se cuentan en pasajeros/visitantes (sin selección en el widget)
  - **Botón "Listo":** Botón verde para confirmar configuración
- **Comportamiento de controles:**
  - Botones +/- ajustan cantidades por edad
  - Botones se deshabilitan al alcanzar mínimo/máximo
  - Validación: Mínimo 1 visitante total (típicamente al menos 1 adulto)
- ⚠️ Pendiente definir si solicita edad exacta de cada niño para validación de políticas Disney
- Al cerrar dropdown, campo principal actualiza con resumen: "X adulto(s), Y niño(s)"

**Validaciones del sistema:**
- **Todos los campos son obligatorios** antes de poder buscar
- **Parques:** Validación condicional según tipo de ticket seleccionado
- **Fechas:** No permite fechas pasadas, rango lógico si son múltiples días
- **Visitantes:** Mínimo 1 visitante (típicamente al menos 1 adulto)
- **Botón "Buscar":**
  - Deshabilitado (gris) si faltan campos obligatorios
  - Habilitado (verde) cuando todos los campos están completos
- Al hacer clic en "Buscar" → Redirige a módulo Disponibilidad/Opciones con criterios seleccionados

**Variaciones móviles:**
- **Layout:** Campos apilados verticalmente, cada campo ocupa ancho completo
- **Selector de parques:** Vista optimizada según formato (cards en scroll horizontal si aplica)
- **Calendario:** Pantalla completa con navegación táctil optimizada
- **Dropdown visitantes:** Modal de pantalla completa con controles +/- grandes y áreas táctiles amplias
- **Botón "Buscar":** Sticky en la parte inferior, siempre visible durante scroll
- **Botón "Listo" del dropdown:** Sticky en parte inferior del modal

##### ✅ VALIDACIONES DE QA

Estas validaciones deben incluirse en todos los casos de prueba que involucren el Widget de Selección:

- [ ] **VAL-DIS-HOME-001:** Todos los campos son obligatorios
  - **Verificar:** Botón "Buscar" deshabilitado (gris) si falta algún campo, habilitado (verde) solo con todos completos
  
- [ ] **VAL-DIS-HOME-002:** Selección de parques según tipo de ticket
  - **Verificar:** Base = 1 solo parque, Hopper = múltiples parques, selección se ajusta correctamente
  
- [ ] **VAL-DIS-HOME-003:** Calendario no permite fechas pasadas
  - **Verificar:** Fechas anteriores a hoy están deshabilitadas (gris) y no seleccionables
  
- [ ] **VAL-DIS-HOME-004:** Rango de fechas lógico
  - **Verificar:** Si múltiples días, fecha fin debe ser posterior a fecha inicio, rango visual verde claro entre fechas
  
- [ ] **VAL-DIS-HOME-005:** Tipo de ticket condiciona selector de parques
  - **Verificar:** Cambiar tipo de ticket actualiza opciones de parques y resetea selección incompatible
  
- [ ] **VAL-DIS-HOME-006:** Dropdown visitantes valida límites
  - **Verificar:** Botones +/- respetan mínimos/máximos por categoría, mínimo 1 visitante total
  
- [ ] **VAL-DIS-HOME-007:** Resumen de visitantes correcto
  - **Verificar:** Campo muestra "X adulto(s), Y niño(s)" actualizado correctamente al cerrar dropdown
  
- [ ] **VAL-DIS-HOME-008:** Botón "Buscar" redirige correctamente
  - **Verificar:** Clic en "Buscar" redirige a módulo Disponibilidad/Opciones con criterios seleccionados
  
- [ ] **VAL-DIS-HOME-009:** Calendario funciones correctas
  - **Verificar:** Navegación mes/año con flechas, selección visual (verde inicio/fin, verde claro rango), botones "Cancelar" y "Aceptar" funcionan correctamente
  
- [ ] **VAL-DIS-HOME-010:** Variaciones móviles
  - **Verificar:** Layout apilado vertical, calendario pantalla completa, dropdown visitantes modal fullscreen, botones sticky en móviles

##### 🧪 Escenarios de Prueba

**Escenario 1: Búsqueda exitosa de tickets Disney - Ticket Base 1 parque**
- **Precondición:** Usuario autenticado en home Disney
- **Pasos:**
  1. Seleccionar 1 parque (ej: Magic Kingdom)
  2. Seleccionar fecha única (1 día adelante)
  3. Seleccionar tipo "Base"
  4. Configurar 2 adultos en dropdown visitantes
  5. Clic en "Buscar"
- **Resultado esperado:** Redirige a Disponibilidad con opciones de tickets Base para Magic Kingdom, fecha seleccionada, 2 adultos

**Escenario 2: Búsqueda exitosa - Ticket Park Hopper múltiples parques y días**
- **Precondición:** Usuario autenticado en home Disney
- **Pasos:**
  1. Seleccionar tipo "Park Hopper"
  2. Seleccionar 3 parques (Magic Kingdom, Epcot, Hollywood Studios)
  3. Seleccionar rango de fechas (3 días adelante)
  4. Configurar 2 adultos + 2 niños en dropdown visitantes
  5. Clic en "Buscar"
- **Resultado esperado:** Redirige a Disponibilidad con opciones de tickets Hopper para 3 parques, 3 días, 2 adultos + 2 niños

**Escenario 3: Validación de campos obligatorios**
- **Precondición:** Usuario en home Disney
- **Pasos:**
  1. Dejar campos vacíos
  2. Intentar hacer clic en "Buscar"
- **Resultado esperado:** Botón "Buscar" deshabilitado (gris), no permite búsqueda

**Escenario 4: Validación de fechas pasadas**
- **Precondición:** Usuario en home Disney
- **Pasos:**
  1. Abrir calendario
  2. Intentar seleccionar fecha pasada
- **Resultado esperado:** Fechas pasadas bloqueadas (gris), no seleccionables

**Escenario 5: Cambio de tipo de ticket resetea parques incompatibles**
- **Precondición:** Usuario en home Disney
- **Pasos:**
  1. Seleccionar tipo "Park Hopper"
  2. Seleccionar 3 parques
  3. Cambiar tipo a "Base"
- **Resultado esperado:** Selector de parques se ajusta a selección única, resetea selección múltiple previa

---

## 📋 MÓDULO: DISPONIBILIDAD/OPCIONES

### Descripción del Módulo

Módulo que muestra las opciones de tickets Disney disponibles según los criterios del usuario (parques, fechas, tipo de ticket, visitantes). Permite comparar diferentes opciones, ajustar Puntos + Plata (ubicación ⚠️ pendiente confirmar), y seleccionar un ticket para continuar al checkout.

⚠️ **IMPORTANTE:** La estructura exacta de este módulo depende del proveedor integrado (DerbySoft vs OffLine). Se documenta estructura esperada genérica hasta confirmar proveedor específico de Promerica.

**Características principales:**
- Widget de búsqueda persistente para modificar criterios
- Visualización de opciones de tickets con información detallada
- Comparación de precios entre opciones
- Slider Puntos + Plata (ubicación ⚠️ pendiente confirmar)
- Filtros disponibles (⚠️ pendiente confirmar si existen para Disney)

### FUNCIONALIDADES

#### 🔹 Funcionalidad: Widget de Búsqueda Persistente

##### 📖 Descripción Funcional

**Ubicación:** Parte superior del módulo Disponibilidad, debajo del header
**Tipo:** Componente de resumen compacto con campos editables
**Acceso:** Visible en todo momento durante navegación de opciones

Widget que muestra resumen de criterios de búsqueda seleccionados en HOME y permite modificarlos sin salir del módulo. Optimiza experiencia al evitar retroceder a HOME para ajustar búsqueda.

##### 🧩 Componentes

| Componente | Descripción | Tipo | Funcionalidad/Editable |
|------------|-------------|------|------------------------|
| **Parques seleccionados** | Muestra parque(s) Disney seleccionado(s) | Text/Badge | - Formato: Badge o texto compacto<br>- Ej: "Magic Kingdom" o "3 parques"<br>- Clic abre selector para editar<br>- Editable |
| **Fechas de visita** | Muestra fecha única o rango seleccionado | Date display | - Formato: "DD MMM" o "DD-DD MMM YYYY"<br>- Ej: "15 Ene" o "15-18 Ene 2024"<br>- Clic abre calendario para editar<br>- Editable |
| **Tipo de ticket** | Muestra tipo de ticket seleccionado | Text/Badge | - Formato: Badge o texto<br>- Ej: "Base", "Park Hopper"<br>- Clic abre dropdown para editar<br>- Editable |
| **Visitantes** | Muestra cantidad de visitantes por categoría | Text | - Formato: "X adulto(s), Y niño(s)"<br>- Ej: "2 adultos, 1 niño"<br>- Clic abre dropdown para editar<br>- Editable |
| **Botón "Buscar"** | Ejecuta nueva búsqueda con criterios modificados | Button (CTA verde) | - Botón principal verde<br>- Deshabilitado si criterios incompletos<br>- Ejecuta búsqueda y actualiza opciones<br>- Clic mantiene en Disponibilidad con nuevos resultados |

##### 💻 Comportamiento Esperado

**Interacción con campos editables:**
- Cada campo del widget es clicable y abre el control correspondiente para editar
- **Parques:** Clic abre selector (dropdown/checkboxes/cards según proveedor) para cambiar parques
- **Fechas:** Clic abre calendario interactivo para cambiar fecha única o rango
- **Tipo de ticket:** Clic abre dropdown para cambiar entre Base/Hopper/Hopper Plus
- **Visitantes:** Clic abre dropdown con controles +/- para ajustar cantidad por edad
- Modificar cualquier campo no ejecuta búsqueda automáticamente, requiere clic en "Buscar"

**Validaciones del sistema:**
- Widget mantiene criterios válidos en todo momento
- Cambiar tipo de ticket condiciona selector de parques (Base = 1, Hopper = múltiples)
- Fechas no permite selección de fechas pasadas
- Mínimo 1 visitante requerido
- Botón "Buscar" deshabilitado (gris) si se edita campo pero queda incompleto
- Botón "Buscar" habilitado (verde) cuando todos los criterios son válidos

**Comportamiento de búsqueda:**
- Al hacer clic en "Buscar" con criterios modificados:
  - Muestra indicador de carga (spinner/skeleton)
  - Ejecuta nueva consulta al backend con criterios actualizados
  - Actualiza lista de opciones de tickets en la misma página
  - Scroll automático a inicio de resultados
  - Mantiene usuario en módulo Disponibilidad (no redirige a HOME)

**Variaciones móviles:**
- Widget puede colapsar a línea única con resumen: "3 parques • 15-18 Ene • 2 adultos"
- Clic expande widget completo para editar
- Botón "Buscar" sticky en parte inferior al editar
- Controles de edición (calendario, dropdown) en modal de pantalla completa

##### ✅ VALIDACIONES DE QA

- [ ] **VAL-DIS-DISP-001:** Widget visible en todo momento
  - **Verificar:** Widget persistente en parte superior, no desaparece al hacer scroll
  
- [ ] **VAL-DIS-DISP-002:** Campos editables funcionan correctamente
  - **Verificar:** Clic en cada campo abre control correspondiente para editar
  
- [ ] **VAL-DIS-DISP-003:** Criterios se actualizan correctamente
  - **Verificar:** Cambios en campos se reflejan en widget antes de buscar
  
- [ ] **VAL-DIS-DISP-004:** Botón "Buscar" condicional
  - **Verificar:** Deshabilitado si criterios incompletos, habilitado con criterios válidos
  
- [ ] **VAL-DIS-DISP-005:** Nueva búsqueda actualiza resultados
  - **Verificar:** Clic en "Buscar" ejecuta consulta y actualiza opciones sin cambiar módulo
  
- [ ] **VAL-DIS-DISP-006:** Indicador de carga visible
  - **Verificar:** Spinner/skeleton aparece durante búsqueda, desaparece al cargar resultados
  
- [ ] **VAL-DIS-DISP-007:** Variaciones móviles
  - **Verificar:** Widget colapsable en móviles, controles en modal fullscreen

##### 🧪 Escenarios de Prueba

**Escenario 1: Modificar fechas desde widget persistente**
- **Precondición:** Usuario en Disponibilidad con resultados cargados
- **Pasos:**
  1. Clic en campo "Fechas" del widget
  2. Seleccionar nuevo rango de fechas en calendario
  3. Clic en "Aceptar"
  4. Clic en botón "Buscar"
- **Resultado esperado:** Nueva búsqueda con fechas actualizadas, lista de opciones se actualiza sin salir de Disponibilidad

**Escenario 2: Cambiar tipo de ticket y parques**
- **Precondición:** Usuario en Disponibilidad con ticket Base seleccionado (1 parque)
- **Pasos:**
  1. Clic en campo "Tipo de ticket"
  2. Seleccionar "Park Hopper"
  3. Clic en campo "Parques"
  4. Seleccionar 3 parques adicionales
  5. Clic en "Buscar"
- **Resultado esperado:** Widget actualiza a Park Hopper + múltiples parques, opciones muestran tickets Hopper para los nuevos parques

---

#### 🔹 Funcionalidad: Cards/Lista de Opciones de Tickets

##### 📖 Descripción Funcional

**Ubicación:** Área principal del módulo Disponibilidad, debajo del widget persistente
**Tipo:** Lista vertical de cards con información de cada opción de ticket
**Acceso:** Visible tras ejecutar búsqueda desde HOME o modificar criterios en widget persistente

Visualización de diferentes opciones de tickets Disney disponibles según criterios seleccionados. Cada card presenta información completa del ticket (tipo, parques, duración, precio) y permite seleccionar para continuar al checkout.

⚠️ **PENDIENTE CONFIRMAR:**
- Layout exacto (cards, tabla, lista)
- Precio mostrado: ¿Por persona o total del grupo?
- Ubicación del slider Puntos + Plata: ¿En cada card o global?
- Filtros disponibles (si aplica)

##### 🧩 Componentes

| Componente | Descripción | Tipo | Funcionalidad/Editable |
|------------|-------------|------|------------------------|
| **Nombre del ticket** | Título descriptivo del ticket | Text/Heading | - Formato: "[Parque(s)] - [Días] - [Tipo]"<br>- Ej: "Magic Kingdom - 1 Día - Base"<br>- Ej: "Multi Parque - 3 Días - Hopper"<br>- No editable |
| **Parques incluidos** | Lista o íconos de parques Disney incluidos | Icon/List | - Formato visual según tipo:<br>  • Base: Ícono único del parque<br>  • Hopper/Plus: Múltiples íconos o lista<br>- Ejemplos: Magic Kingdom, Epcot, Hollywood Studios, Animal Kingdom<br>- No editable |
| **Duración** | Número de días válido y rango de fechas | Text/Date | - Formato: "X día(s)"<br>- Fechas: "Del DD MMM al DD MMM YYYY"<br>- Ej: "3 días • Del 15 al 18 Ene 2024"<br>- No editable |
| **Tipo de ticket** | Badge indicando categoría del ticket | Badge | - Opciones: "Base" \| "Park Hopper" \| "Park Hopper Plus"<br>- Código de color según tipo<br>- No editable |
| **Precio** | Valor en Puntos, Plata, o combinación P+P | Text/Number | - Formato: "XX,XXX Puntos" o "$XX,XXX" o combinación<br>- ⚠️ Pendiente confirmar: ¿Por persona o total grupo?<br>- ⚠️ Pendiente confirmar: Ubicación de slider P+P<br>- Editable si slider P+P disponible |
| **Información adicional** | Qué incluye el ticket, restricciones, validez | Text/Link | - Sección desplegable o link "Ver más"<br>- Contenido: Qué incluye, restricciones, políticas<br>- No editable, solo informativo |
| **Botón de acción** | Selecciona el ticket para continuar | Button (CTA verde) | - Texto: "Seleccionar" o "Ver más"<br>- Botón principal verde<br>- Clic redirige a checkout (si "Seleccionar") o abre modal con detalles (si "Ver más") |

##### 💻 Comportamiento Esperado

**Visualización de opciones:**
- Lista vertical de cards, cada card representa una opción de ticket disponible
- ⚠️ Pendiente confirmar si hay orden específico (precio, popularidad, recomendación)
- Si no hay opciones disponibles: Mensaje "No se encontraron opciones para los criterios seleccionados" + sugerencias (cambiar fechas, parques, etc.)

**Interacción con cards:**
- Hover en card: Resaltado visual (sombra, borde)
- Clic en "Ver más" o información adicional: Abre modal/desplegable con detalles completos del ticket
- Clic en "Seleccionar": Guarda ticket seleccionado y redirige a módulo Checkout

**Slider Puntos + Plata (si aplica):**
- ⚠️ Pendiente confirmar ubicación exacta:
  - Opción A: Slider global arriba de cards, afecta precio mostrado en todos
  - Opción B: Slider individual en cada card
- Deslizar ajusta proporción Puntos/Plata dinámicamente
- Muestra desglose: "XX,XXX Puntos + $XX,XXX Plata"
- Validación de saldo de puntos disponibles del usuario

**Información detallada del ticket:**
- **Qué incluye:**
  - Acceso a parque(s) especificado(s)
  - Días válidos de visita
  - Beneficios según tipo (Hopper: cambio de parque mismo día, Plus: parques acuáticos)
- **Restricciones:**
  - Validez del ticket (fechas límite de uso)
  - Edad de visitantes (Adulto, Niño, Infante según políticas Disney)
  - Políticas de cancelación/cambios
  - Requisitos de ingreso (documentos, QR, etc.)

**Variaciones móviles:**
- Cards apiladas verticalmente, ancho completo
- Información compactada, "Ver más" expande detalles en modal fullscreen
- Botón "Seleccionar" sticky en parte inferior al ver detalles
- Scroll infinito o paginación según cantidad de opciones

##### ✅ VALIDACIONES DE QA

- [ ] **VAL-DIS-OPC-001:** Opciones muestran información correcta
  - **Verificar:** Nombre, parques, duración, tipo, precio coinciden con criterios de búsqueda
  
- [ ] **VAL-DIS-OPC-002:** Precio mostrado es consistente
  - **Verificar:** Precio en formato correcto (Puntos/Plata/P+P), ⚠️ confirmar si es por persona o total
  
- [ ] **VAL-DIS-OPC-003:** Botón "Seleccionar" funciona
  - **Verificar:** Clic guarda ticket y redirige a Checkout con información correcta
  
- [ ] **VAL-DIS-OPC-004:** Slider P+P ajusta precio dinámicamente (si aplica)
  - **Verificar:** Deslizar slider actualiza desglose Puntos + Plata, valida saldo disponible
  
- [ ] **VAL-DIS-OPC-005:** Información adicional accesible
  - **Verificar:** "Ver más" abre modal/desplegable con detalles completos del ticket
  
- [ ] **VAL-DIS-OPC-006:** Mensaje si no hay opciones
  - **Verificar:** Si no hay resultados, muestra mensaje claro con sugerencias
  
- [ ] **VAL-DIS-OPC-007:** Variaciones móviles
  - **Verificar:** Cards en scroll vertical, detalles en modal fullscreen, botón sticky

##### 🧪 Escenarios de Prueba

**Escenario 1: Selección de ticket Base 1 parque**
- **Precondición:** Usuario en Disponibilidad con opciones cargadas
- **Pasos:**
  1. Revisar card "Magic Kingdom - 1 Día - Base"
  2. Verificar precio, parques, duración
  3. Clic en "Seleccionar"
- **Resultado esperado:** Redirige a Checkout con ticket Base seleccionado, información correcta

**Escenario 2: Ver información adicional de ticket Hopper Plus**
- **Precondición:** Usuario en Disponibilidad con opciones cargadas
- **Pasos:**
  1. Localizar card "Multi Parque - 3 Días - Hopper Plus"
  2. Clic en "Ver más" o ícono de información
  3. Revisar detalles: Qué incluye, restricciones, validez
- **Resultado esperado:** Modal/desplegable muestra información completa del ticket Hopper Plus

**Escenario 3: Ajustar Puntos + Plata con slider (si aplica)**
- **Precondición:** Usuario en Disponibilidad, slider P+P visible
- **Pasos:**
  1. Deslizar slider a 70% Puntos / 30% Plata
  2. Verificar desglose actualizado en card
  3. Clic en "Seleccionar"
- **Resultado esperado:** Checkout muestra precio con proporción 70% Puntos / 30% Plata seleccionada

---

## 💳 MÓDULO: CHECKOUT

> ⚠️ **Documentación en proceso**  
> Este módulo está siendo estandarizado. Se está trabajando en la documentación de: Datos de visitantes (nombre, edad, país), Contacto, Métodos de pago, Resumen de reserva.  
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
✅ Campos obligatorios: Parques, fechas, tipo de ticket, visitantes  
✅ Visitantes: Mínimo 1 visitante (típicamente 1 adulto)  
✅ Botón buscar: Habilitado solo con campos completos  
✅ Fechas: No permite selección de fechas pasadas  
✅ Tipo de ticket: Condiciona selección de parques (Base = 1, Hopper = múltiples)  
✅ Calendario: Navegación mes/año, rango visual si son múltiples días  
✅ Dropdown visitantes: Controles +/- funcionales, rangos validados

**Disponibilidad/Opciones:**
⚠️ Pendiente documentar: Layout de opciones, información mostrada, slider ubicación
✅ Resumen de criterios correcto en widget persistente (esperado)
✅ Opciones de tickets con información completa (esperado)
✅ Precio claro por persona o total según configuración

**Detalle de Ticket:**
⚠️ Pendiente documentar: Descripción completa, qué incluye, restricciones, validez

**Checkout:**
⚠️ Pendiente documentar: Datos de cada visitante (nombre, edad, país), contacto, métodos de pago

**Confirmación:**
⚠️ Pendiente documentar: Código de reserva, voucher, manejo de errores

**Admin:**
✅ **CRÍTICO Disney:** Validar disponibilidad de voucher PDF  
⚠️ Pendiente documentar: Formato del voucher (bilingüe típicamente)  
⚠️ Pendiente documentar: Contenido del voucher (QR, parques, fechas, instrucciones)  
⚠️ Pendiente documentar: Estados de procesamiento

### Validaciones Específicas del Modelo Slider (Puntos + Plata):

⚠️ **PENDIENTE CONFIRMAR:** ¿El slider aparece en disponibilidad, detalle o checkout?  
⚠️ **PENDIENTE CONFIRMAR:** ¿Ubicación exacta del slider?  
⚠️ **PENDIENTE CONFIRMAR:** Porcentaje mínimo de puntos requerido  
✅ **Validación de saldo:** Sistema debe verificar puntos disponibles  
✅ **Solicitud de pago:** Si hay copago en plata, se requiere método de pago  
⚠️ **PENDIENTE CONFIRMAR:** Tipo de emisión (automática/manual)  
⚠️ **PENDIENTE CONFIRMAR:** ¿Precio por persona o total? ¿Slider ajusta por persona o total?

### Validaciones de Experiencia de Usuario (UI/UX):

✅ **Selector de parques:** Lógica condicional según tipo de ticket  
✅ **Calendario:** Navegación intuitiva, rango visual claro si son múltiples días  
✅ **Dropdown visitantes:** Controles +/- funcionales, límites validados  
✅ **Responsive:** Adaptación correcta a móviles (sticky buttons, modals fullscreen)  
✅ **Estados de carga:** Indicadores visuales durante búsqueda  
✅ **Mensajes de error:** Claros y orientados a acción del usuario  
✅ **Accesibilidad:** Componentes navegables por teclado y lectores de pantalla

### Validaciones Específicas de Disney:

✅ **Voucher bilingüe (esperado):** Inglés + Español  
✅ **Código QR (esperado):** Para ingreso a parques  
✅ **Nombres de visitantes:** Deben coincidir con documentos de identidad  
✅ **Rangos de edad:** Validación según políticas Disney  
⚠️ **Pendiente documentar:** Proceso de canje/activación de tickets

---

## 📝 FORMATO DE TÍTULO

```
[PROM] Disney - [Módulo/Escenario] - [Variante]
```

**Ejemplos actualizados:**

- `[PROM] Disney - Home - Búsqueda - 1 día - 2 adultos - Puntos + Plata`
- `[PROM] Disney - Home - Búsqueda - 3 días - 2 adultos 2 niños - Solo Puntos`
- `[PROM] Disney - Disponibilidad - Selección de opción - Hopper Plus - 4 adultos - Puntos + Plata`

---

## 🚀 PRÓXIMOS PASOS PARA COMPLETAR ESTE ARCHIVO

### Módulos Documentados:

✅ **Componentes Transversales** - Referencia a vuelos (Header, Tabs, Footer)  
✅ **Pasos Obligatorios del Flujo E2E** - 25 pasos documentados (pasos 1-13 completos, 14-25 pendientes)  
✅ **Módulo Home/Login** - Widget de búsqueda con 5 componentes + Calendario + Dropdown visitantes (estructura genérica)

### Módulos Pendientes:

**1. CRÍTICO - Confirmar Proveedor:**

- ✅ Validar si es DerbySoft, OffLine u otro
- Basado en proveedor, ajustar toda la documentación de disponibilidad y checkout
- Diferencias conocidas:
  - **DerbySoft:** Interfaz más estructurada, voucher automático
  - **OffLine:** Proceso más manual, voucher puede requerir gestión adicional

**2. Módulo Disponibilidad/Opciones - Completar:**

- Layout específico de opciones de tickets
- Presentación de precios (por persona vs total)
- Información detallada por tipo de ticket
- Slider Puntos + Plata (ubicación y comportamiento)
- Comparación de opciones si hay múltiples
- Filtros (si aplica)

**3. Módulo Detalle de Ticket - Documentar:**

- Descripción completa del ticket
- Parques incluidos con detalles
- Qué incluye / Qué no incluye
- Restricciones y políticas Disney
- Validez del ticket (días consecutivos vs flexibles)
- Condiciones de uso

**4. Checkout:**

- Resumen de reserva (parques, fechas, tipo, visitantes)
- Formulario de datos de cada visitante:
  - Nombre completo
  - Edad o fecha de nacimiento
  - País de origen
  - ⚠️ Validar si requiere documento de identidad
- Datos de contacto (email, teléfono)
- Métodos de pago (integración con gateway)
- Términos y condiciones Disney

**5. Confirmación:**

- Confirmación exitosa (código de reserva)
- Voucher PDF (bilingüe típicamente)
- Email de confirmación automático
- Instrucciones de canje/uso de tickets
- Políticas de cancelación Disney
- Manejo de errores (tipos, mensajes, acciones de recuperación)

**6. Admin:**

- Validación de reserva en backend
- Estados de procesamiento
- **CRÍTICO:** Disponibilidad de voucher PDF
- Contenido del voucher:
  - Código QR para ingreso
  - Parques seleccionados
  - Fechas válidas
  - Nombres de visitantes
  - Instrucciones en inglés/español
  - Información de contacto Disney

### Información de Negocio Pendiente:

**Proveedor:**

- ⚠️ **CRÍTICO:** Confirmar proveedor para Promerica (DerbySoft vs OffLine)
- Identificar diferencias funcionales según proveedor
- Validar disponibilidad por país (CR, PA, HN, DO, GT, SV, NI)

**Reglas del Slider:**

- ⚠️ **CRÍTICO:** Confirmar reglas y ubicación del slider en Disney (disponibilidad, detalle o checkout)
- Porcentaje mínimo de puntos requerido
- Fórmula de cálculo Puntos ↔ Plata (por persona o total grupo)
- Ubicación del slider (disponibilidad, detalle, checkout)

**Políticas de Disney:**

- Rangos de edad por categoría (adultos, niños; menores de 3 años con entrada gratuita)
- Edades específicas con impacto en precio
- Máximo de visitantes por reserva
- Políticas de cancelación específicas Disney
- Validez de tickets (días consecutivos vs flexibles)
- Restricciones de uso (un parque por día vs hopper)

**Proceso de Reserva:**

- Definir si emisión es automática o manual
- Tiempos de confirmación esperados
- Estados de reserva durante el proceso
- Disponibilidad y formato de voucher
- Proceso de activación de tickets
- Proceso de cancelación de reservas confirmadas

**Parques Disney disponibles:**

- Confirmar lista completa según destino
- Magic Kingdom, Epcot, Hollywood Studios, Animal Kingdom (Orlando)
- Disneyland Park, California Adventure (California)
- ⚠️ Validar qué destinos están disponibles en Promerica

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
- ✅ Aplicada jerarquía H1 → H2 → H3 → H4 → H5 consistente
- ✅ **Módulo HOME/LOGIN:**
  - Widget de Selección de Tickets con estructura completa H5:
    - 📖 Descripción Funcional
    - 🧩 Componentes (tabla Markdown con 5 componentes)
    - 💻 Comportamiento Esperado (integra Calendario y Dropdown Visitantes)
    - ✅ VALIDACIONES DE QA (10 validaciones VAL-DIS-HOME-001 a 010)
    - 🧪 Escenarios de Prueba (5 escenarios)
- ✅ **Módulo DISPONIBILIDAD/OPCIONES:**
  - Widget de Búsqueda Persistente con estructura completa H5:
    - 📖 Descripción Funcional
    - 🧩 Componentes (tabla Markdown con 5 componentes)
    - 💻 Comportamiento Esperado
    - ✅ VALIDACIONES DE QA (7 validaciones VAL-DIS-DISP-001 a 007)
    - 🧪 Escenarios de Prueba (2 escenarios)
  - Cards/Lista de Opciones de Tickets con estructura completa H5:
    - 📖 Descripción Funcional
    - 🧩 Componentes (tabla Markdown con 7 componentes)
    - 💻 Comportamiento Esperado
    - ✅ VALIDACIONES DE QA (7 validaciones VAL-DIS-OPC-001 a 007)
    - 🧪 Escenarios de Prueba (3 escenarios)
- ✅ Componentes convertidos de listas a tablas Markdown
- ✅ "Calendario de Fechas Disney" y "Dropdown Visitantes Disney" integrados en Comportamiento Esperado (no secciones separadas)
- ✅ Descripción Funcional con "Funcional", Comportamiento Esperado con "E" mayúscula
- ✅ Variaciones Móviles integradas en Comportamiento Esperado (no H5 separado)

**Pendiente para versión futura:**
- ⚠️ Confirmar proveedor específico (DerbySoft vs OffLine) para completar detalles de implementación
- ⚠️ Documentar Módulos CHECKOUT y CONFIRMACIÓN con misma estructura
- ⚠️ Confirmar rangos de edad, límites de visitantes, ubicación de slider P+P
- ⚠️ Validar políticas específicas de Disney y disponibilidad por país

### Versión 0.3 - 2026-01-23

**Cambios principales:**

- ✅ Agregada URL Test Costa Rica (CR)
- ✅ Confirmado modelo de negocio: Puntos + Plata (Slider)
- ⚠️ Identificados proveedores potenciales: DerbySoft, OffLine (pendiente confirmar cuál usa Promerica)
- ✅ Referenciados Componentes Transversales (ver PROM_VUELOS.md)
- ✅ Documentado Módulo Home/Login (Widget búsqueda genérico + Calendario + Dropdown visitantes)
- ✅ Agregados Pasos Obligatorios del Flujo E2E (25 pasos)
- ✅ Aplicada jerarquía de títulos consistente (H1 → H2 → H3)
- ✅ Consolidadas Validaciones Críticas por módulo
- ✅ Reorganizados Próximos Pasos con prioridad en confirmar proveedor
- ⚠️ Marcado como CRÍTICO: Confirmar proveedor para completar documentación de disponibilidad y checkout

### Versión 0.2 - 2026-01-20

**Cambios principales:**

- ✅ Identificado modelo de negocio B2B2C Transversal
- ✅ Agregados 7 países soportados (CR, PA, HN, DO, GT, SV, NI)

### Versión 0.1 - 2026-01-20

**Cambios principales:**

- ✅ Template inicial creado con estructura base
- ✅ Definidas secciones principales del documento
