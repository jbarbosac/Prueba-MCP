# 🏨 PRODUCTO: HOTELES - PROMERICA REWARDS

> **📖 Información Global:** Ver [PROM_QA_Assistant.agent.md](../../../../agents/PROM_QA_Assistant.agent.md) para URL del portal, país activo, modelo de negocio y versión del marketplace.

---

## 📌 Descripción General

El producto **Hoteles** permite a los usuarios del programa Promerica Rewards buscar, comparar y reservar alojamientos utilizando el modelo de pago híbrido **Puntos + Plata (Slider)**. El sistema integra HotelBeds como proveedor principal, ofreciendo búsqueda por destinos a nivel mundial con filtrado avanzado por estrellas, precios, servicios y tipos de propiedad.

**Características principales:**
- Búsqueda de hoteles por ciudad, país o región
- Selección flexible de fechas con calendario mensual
- Configuración de habitaciones múltiples y huéspedes por habitación
- Modelo de pago flexible con slider Puntos + Plata
- Filtrado avanzado por categorías, servicios y tipos de alojamiento
- Integración con HotelBeds para inventario global

---

## 📦 CONTEXTO OPERATIVO

### Proveedores Disponibles

**Proveedor confirmado:**

- **HotelBeds** (proveedor principal para hoteles)

⚠️ **Pendiente validar:** Si existen proveedores adicionales o alternativas

### Componentes Transversales

> **Nota:** Estos componentes son compartidos por todos los productos del marketplace (Vuelos, Autos, **Hoteles**, Disney, Actividades). Ver detalle completo en [PROM_VUELOS.md](PROM_VUELOS.md#-componentes-transversales).

#### Header Global

Barra superior con navegación principal, branding personalizado de Promerica y acceso de usuario.

#### Tabs de Productos

Pestañas horizontales para navegación entre productos (Vuelos, Autos, **Hoteles**, Disney, Actividades).

#### Footer Global

Sección inferior con información institucional y canales de contacto personalizados por país.

### Flujo E2E Obligatorio

**Estos pasos deben incluirse en todos los casos de prueba para asegurar trazabilidad completa:**

1. **Acceder al portal** → https://traveltest-club-promerica.preprodppm.com/es-cr | El portal carga correctamente y muestra la pantalla de inicio
2. **Realizar login** → Ingresar usuario y contraseña válidos | Login exitoso y acceso al home con tabs de productos visibles
3. **Navegar a Hoteles** → Clic en tab "Hoteles" | Widget de búsqueda de hoteles se muestra correctamente
4. **Seleccionar destino** → Clic en campo "Destino" | Modal de búsqueda de destinos se abre con buscador
5. **Buscar y seleccionar destino** → Escribir ciudad/país en buscador | Sistema filtra resultados y muestra lista de destinos
6. **Confirmar destino** → Clic en destino deseado de la lista | Modal se cierra y campo "Destino" se actualiza con selección
7. **Seleccionar fechas** → Clic en "Check-in" o "Check-out" | Calendario mensual se abre
8. **Confirmar rango de fechas** → Seleccionar fecha inicio y fecha fin | Calendario se cierra y campos muestran fechas seleccionadas
9. **Configurar habitaciones y huéspedes** → Clic en campo "Habitaciones y huéspedes" | Dropdown expansible se abre
10. **Ajustar cantidad** → Seleccionar número de habitaciones, adultos y niños | Campos se actualizan con cantidades seleccionadas
11. **Confirmar configuración** → Clic en "Listo" o fuera del dropdown | Dropdown se cierra y campo muestra resumen (ej: "2 personas, 1 habitación")
12. **Ejecutar búsqueda** → Clic en botón "Buscar" verde | Sistema redirige a módulo de Disponibilidad con resultados
13. **Revisar widget de búsqueda persistente** → Verificar resumen de criterios en parte superior | Widget compacto muestra destino, fechas, habitaciones
14. **Navegar por lista de hoteles** → Scroll por resultados | Cards de hoteles se muestran con información básica
15. **Aplicar filtros laterales** → Seleccionar estrellas, precio, servicios, tipo de hotel | Resultados se actualizan dinámicamente
16. **Ver detalle de hotel** → Clic en card o botón "Ver más" | ⚠️ Pendiente documentar: ¿Abre modal de detalle o redirige a nueva página?
17. **Revisar habitaciones disponibles** → ⚠️ Pendiente documentar vista de habitaciones | ⚠️ Pendiente documentar opciones de habitación
18. **Ajustar slider Puntos + Plata** → ⚠️ Pendiente documentar ubicación del slider | ⚠️ Pendiente documentar validación de saldo
19. **Seleccionar habitación** → Clic en botón de selección | ⚠️ Pendiente documentar comportamiento
20. **Continuar a Checkout** → Clic en botón de confirmación | ⚠️ Pendiente documentar validaciones de checkout
21. **Completar datos de huéspedes** → Llenar formulario con información de contacto | ⚠️ Pendiente documentar campos específicos
22. **Seleccionar método de pago** → Ingresar datos de tarjeta si hay copago en plata | ⚠️ Pendiente documentar proceso de pago
23. **Confirmar reserva** → Clic en botón de confirmación final | ⚠️ Pendiente documentar proceso de emisión
24. **Validar confirmación** → Verificar código de reserva, voucher | ⚠️ Pendiente documentar datos mostrados
25. **Verificar en Admin** → Buscar reserva en aplicativo Admin | ⚠️ Pendiente documentar validaciones de backend

**Nota:** Los pasos 16-25 están pendientes de documentación completa según información de módulos Detalle, Checkout, Confirmación y Admin.

---

## 🏠 MÓDULO: HOME/LOGIN

### 📋 Descripción del Módulo

Página principal del marketplace donde el usuario accede al buscador de hoteles y navega entre productos disponibles. La interfaz es personalizable según el país configurado (Costa Rica en Test). Este módulo proporciona búsqueda por destinos globales con modal especializado y configuración flexible de habitaciones/huéspedes.

### 🎨 FUNCIONALIDADES

> 🔗 **Componentes Transversales:** Para Header, Tabs de Productos y Footer ver sección [Componentes Transversales](#componentes-transversales)

---

#### 🔹 Funcionalidad: Widget de Búsqueda de Hoteles

##### 📖 Descripción Funcional

Formulario principal para búsqueda de hoteles con diseño limpio y moderno. Permite configurar destino, fechas de estancia (check-in/check-out) y cantidad de habitaciones con huéspedes. Incluye modal especializado para búsqueda de destinos y controles numéricos para gestión de habitaciones.

**Ubicación:** Centro de la página de inicio, debajo del header y tabs de productos  
**Tipo de componente:** Formulario interactivo con modal de destinos y controles numéricos  
**Acceso:** Disponible para todos los usuarios autenticados

##### 🧩 Componentes

1. **Campo "Destino":**
   - Label: "Destino"
   - Placeholder: "Selecciona un destino"
   - Ícono de ubicación (verde) posicionado a la derecha del campo
   - Campo obligatorio para realizar búsqueda

2. **Campo "Selecciona tus fechas":**
   - Label: "Selecciona tus fechas"
   - Placeholder inicial: "Selecciona tus fechas"
   - Ícono de calendario posicionado a la derecha
   - Después de selección muestra formato: "Vie, 31 Oct - Vie, 7 Nov"

3. **Dropdown "Habitaciones":**
   - Label: "Habitaciones"
   - Valor por defecto: "1 persona, 1 habitación"
   - Ícono chevron-down indicando desplegable

4. **Botón "Buscar":**
   - Color de fondo: Verde institucional (#00563F)
   - Texto: "Buscar" en color blanco, centrado
   - Ancho completo (full-width)
   - Bordes redondeados
   - Efecto hover: cambio de opacidad
   - Estado deshabilitado si faltan campos obligatorios

##### 💻 Comportamiento Esperado

**Comportamiento del campo "Destino":**
- Al hacer clic despliega modal "¿A dónde quieres ir?"
- **Modal incluye:**
  - Botón Cerrar (X) en esquina superior derecha
  - Campo de búsqueda con ícono de lupa
  - Placeholder: "Ciudad, hotel, punto de interés"
  - Lista scrollable de resultados con formato: "Nombre | Tipo (Ciudad/Hotel) | País"
  - Ejemplos: "San José | Ciudad | Costa Rica", "Miami Area - FL - Estados Unidos (MIA)"
  - Sugerencias populares cuando el campo está vacío (opcional)
  - Mensaje de estado vacío: "No se encontraron resultados para tu búsqueda"
- Búsqueda filtra resultados en tiempo real mientras el usuario escribe
- Borde con enfoque verde al seleccionar
- Permite selección con clic o tecla Enter
- Clic en destino → Cierra modal y actualiza campo "Destino"
- Botón X o clic fuera → Cierra sin cambios

**Comportamiento del campo "Fechas":**
- Al hacer clic abre calendario interactivo
- **Navegación del calendario:**
  - Flechas simples < > con visualización de mes/año (ej: "ENE 2024")
  - Flechas dobles << >> para saltar múltiples meses
  - Calendario en formato grid con días de semana: L, M, M, J, V, S, D
- **Indicadores visuales:**
  - Día actual destacado
  - Fechas pasadas deshabilitadas (no se pueden seleccionar)
  - Check-in seleccionado resaltado en verde (#00563F)
  - Rango entre fechas con conexión gráfica en verde claro
  - Check-out seleccionado resaltado en verde (#00563F)
- **Proceso de selección:**
  - Primer clic: Establece check-in
  - Segundo clic: Establece check-out (debe ser posterior al check-in)
  - Rango visual muestra días entre check-in y check-out resaltados
- **Validaciones:**
  - Restricción: no permite seleccionar fechas pasadas
  - Validación automática: Check-out debe ser posterior a check-in
  - Cálculo automático de número de noches
- **Botones del modal:**
  - "Cancelar": cierra sin guardar cambios
  - "Aceptar": confirma selección, actualiza campo con formato "Vie, 31 Oct - Vie, 7 Nov" y cierra calendario

**Comportamiento del dropdown "Habitaciones":**
- Al hacer clic abre modal de configuración con fondo blanco
- Permite configurar múltiples habitaciones (Habitación 1, Habitación 2, etc.)
- **Controles por cada habitación:**
  - **Sección Adultos:**
    - Contador numérico con botones - / +
    - Valor editable en el centro
    - Texto informativo: "Desde 18 años"
    - Validación: mínimo 1 adulto por habitación
  - **Sección Niños:**
    - Contador numérico con botones - / +
    - Valor editable en el centro
    - Texto informativo: "0 a 17 años" con ícono de información (i)
    - Rango: 0 a múltiples niños
    - **Dropdown condicional "Edad del niño":**
      - Aparece solo si se agrega al menos 1 niño
      - Label: "Edad del niño"
      - Placeholder: "Selecciona la edad"
      - Opciones: edades de 0 a 17 años
      - Se replica por cada niño agregado
- **Botón "Agregar habitación":**
  - Estilo: texto verde (#00563F) con borde, sin fondo
  - Permite añadir habitaciones adicionales
  - Cada nueva habitación replica la estructura completa de controles
- **Incremento/Decremento:** Botones +/- ajustan cantidades
- **Límites:** Botones se deshabilitan al alcanzar mínimo/máximo
- **Botones de acción del modal:**
  - "Cancelar": descarta cambios y cierra modal sin aplicar
  - "Aplicar": guarda configuración, actualiza texto del dropdown en formato "{X} persona(s), {Y} habitación(es)" y cierra modal

**Validaciones del sistema:**
- Destino es campo obligatorio
- Fechas son obligatorias con check-in anterior a check-out
- Mínimo 1 habitación con 1 adulto
- Botón "Buscar" se habilita solo cuando todos los campos requeridos estén completos
- Al presionar "Buscar" → Redirige al módulo de Disponibilidad con parámetros de búsqueda

**Variaciones móviles:**
- Layout vertical: Los campos se apilan verticalmente en lugar de horizontal para optimizar espacio
- Campo "Destino": Se despliega modal de pantalla completa con resultados de autocompletado
- Campo "Fechas": Abre datepicker de pantalla completa con teclado numérico virtual en la parte inferior
- Selector de habitaciones: Abre modal de pantalla completa con contadores +/- más grandes para facilitar interacción táctil
- Botón "Buscar": Permanece fijo (sticky) en la parte inferior de la pantalla móvil, siempre visible al hacer scroll

##### ✅ VALIDACIONES DE QA

Estas validaciones deben incluirse en todos los casos de prueba que involucren el Widget de Búsqueda:

- [ ] **VAL-HOT-HOME-001:** Destino y fechas son obligatorios
  - **Verificar:** Botón "Buscar" deshabilitado si falta destino o fechas
  
- [ ] **VAL-HOT-HOME-002:** Check-out posterior a check-in
  - **Verificar:** Sistema valida que check-out sea al menos 1 día después
  
- [ ] **VAL-HOT-HOME-003:** No permite fechas pasadas
  - **Verificar:** Calendario bloquea días anteriores a hoy
  
- [ ] **VAL-HOT-HOME-004:** Modal de destinos abre correctamente
  - **Verificar:** Clic en "Destino" abre modal con buscador
  
- [ ] **VAL-HOT-HOME-005:** Búsqueda de destinos filtra en tiempo real
  - **Verificar:** Al escribir ciudad, resultados se filtran (< 1 seg)
  
- [ ] **VAL-HOT-HOME-006:** Configuración de habitaciones funciona
  - **Verificar:** Botones +/- ajustan cantidades, mínimos/máximos respetados
  
- [ ] **VAL-HOT-HOME-007:** Resumen de huéspedes actualiza
  - **Verificar:** Campo muestra "X persona(s), Y habitación(es)" (X = adultos + niños)
  
- [ ] **VAL-HOT-HOME-008:** Botón "Buscar" redirige a Disponibilidad
  - **Verificar:** URL cambia y se muestran resultados según búsqueda

##### 🧪 Escenarios de Prueba

[PENDIENTE: Agregar escenarios específicos de hoteles]

---

## 📋 MÓDULO: DISPONIBILIDAD

### 📋 Descripción del Módulo

Módulo que muestra los resultados de búsqueda de hoteles disponibles según los criterios del usuario. Incluye widget persistente con resumen de búsqueda, panel lateral con filtros avanzados, y listado de hoteles en formato cards. Este módulo permite refinar la búsqueda mediante múltiples criterios y comparar opciones antes de seleccionar un hotel específico.

### 🎨 FUNCIONALIDADES

#### 🔹 Funcionalidad: Widget de Búsqueda Persistente

##### 📖 Descripción Funcional

Resumen compacto de criterios de búsqueda que permanece visible en la parte superior del módulo de disponibilidad, permitiendo modificar la búsqueda sin volver al módulo Home.

**Ubicación:** Parte superior del módulo Disponibilidad, encima de los resultados  
**Tipo de componente:** Barra informativa con acción de edición  
**Persistencia:** Visible durante toda la navegación en Disponibilidad

##### 🧩 Componentes

| Componente | Descripción | Tipo | Editable |
|------------|-------------|------|----------|
| **Destino** | Ciudad o región seleccionada (ej: "San José, Costa Rica") | Text | ✅ |
| **Check-in** | Fecha de entrada con formato corto (ej: "22 Oct") | Text | ✅ |
| **Check-out** | Fecha de salida con formato corto (ej: "25 Oct") | Text | ✅ |
| **Habitaciones y huéspedes** | Resumen (ej: "2 personas, 1 habitación") | Text | ✅ |
| **Botón Buscar** | Botón verde para ejecutar nueva búsqueda | Button | ✅ |
| **Link ocultar** | "Ocultar búsqueda" para colapsar widget | Link | ✅ |

##### 💻 Comportamiento Esperado

**Visualización:**
- Widget permanece visible mientras el usuario navega los resultados (sticky)
- Formato compacto optimizado para no ocupar demasiado espacio vertical

**Interacción con campos:**
- Clic en "Destino" → Abre mismo modal que en HOME con búsqueda en tiempo real
- Clic en fechas → Abre mismo calendario que en HOME con validaciones
- Clic en "Habitaciones y huéspedes" → Abre mismo dropdown que en HOME con controles +/-
- Botón "Buscar" → Actualiza resultados con nuevos criterios sin recargar página completa

**Comportamiento de colapsar:**
- Clic en "Ocultar búsqueda" → Colapsa widget para optimizar espacio de resultados
- Widget colapsado muestra solo resumen en una línea
- Clic en resumen colapsado → Expande widget nuevamente

**Variaciones móviles:**

- **Widget persistente:** Permanece visible mientras el usuario navega los resultados (sticky)
- **Edición de criterios:** Tap en cualquier campo abre su modal correspondiente (destino/fechas/huéspedes)
- **Botón "Buscar":** Ejecuta nueva búsqueda y actualiza resultados sin recargar página completa
- **Ocultar/Mostrar:** Permite colapsar el widget para optimizar espacio de resultados
- **Expansión:** Widget puede abrirse en vista completa en móvil (según comportamiento del portal)

##### ✅ VALIDACIONES DE QA

[PENDIENTE: Agregar validaciones específicas del widget persistente]

##### 🧪 Escenarios de Prueba

[PENDIENTE: Agregar escenarios específicos del widget persistente]

---

#### 🔹 Funcionalidad: Filtros Laterales

##### 📖 Descripción Funcional

Panel lateral interactivo con múltiples categorías de filtros para refinar la búsqueda de hoteles según precio, estrellas, tipo de alojamiento, servicios y políticas de cancelación. Los filtros se aplican de forma acumulativa y actualizan resultados en tiempo real.

**Ubicación:** Panel lateral izquierdo en desktop, drawer expandible en móvil  
**Tipo de componente:** Panel de filtros con controles múltiples  
**Actualización:** Dinámica (sin recarga de página)

##### 🧩 Componentes

| Componente | Descripción | Tipo | Funcionalidad |
|------------|-------------|------|---------------|
| **Filtro precio** | Rango deslizante min-max en Puntos o Plata | Range Slider | Definir rango de precios |
| **Filtro estrellas** | Checkboxes: ★ 1, ★★ 2, ★★★ 3, ★★★★ 4, ★★★★★ 5 | Multi-checkbox | Filtrar por categoría de hotel |
| **Filtro tipo de alojamiento** | Checkboxes: Hotel, Resort, Apartamento, etc. | Multi-checkbox | Filtrar por tipo de propiedad |
| **Filtro servicios/amenidades** | Checkboxes: Wi-Fi, Piscina, etc. | Multi-checkbox | Filtrar por servicios disponibles |
| **Filtro políticas de cancelación** | Checkboxes: Cancelación gratuita, No reembolsable, etc. | Multi-checkbox | Filtrar por condiciones de tarifa |
| **Limpiar filtros** | Link o botón secundario | Button/Link | Resetear filtros a estado inicial |

- **Filtro: Estrellas del hotel**
  - Checkboxes con estrellas visuales: ★ 1, ★★ 2, ★★★ 3, ★★★★ 4, ★★★★★ 5
  - Selección múltiple permitida
  - Contador de resultados por categoría (opcional)

- **Filtro: Tipo de alojamiento**
  - Checkboxes: Hotel, Resort, Apartamento, Hostal, Villa, etc.
  - Selección múltiple permitida
  - ⚠️ Pendiente confirmar tipos exactos disponibles en HotelBeds

- **Filtro: Servicios/Amenidades**
  - Checkboxes: Wi-Fi gratuito, Piscina, Estacionamiento, Desayuno incluido, Gimnasio, Spa, Restaurante, etc.
  - Selección múltiple permitida
  - ⚠️ Pendiente confirmar servicios exactos disponibles

- **Filtro: Políticas de cancelación**
  - Checkboxes: Cancelación gratuita, No reembolsable, Prepago requerido
  - Selección múltiple permitida
  - ⚠️ Pendiente confirmar opciones exactas disponibles

- **Botón "Limpiar filtros":**
  - Link o botón secundario para resetear todos los filtros aplicados

##### 💻 Comportamiento Esperado

**Aplicación de filtros:**
- Filtros se aplican de forma acumulativa
  - Dentro de misma categoría: OR lógico (ej: 3 estrellas O 4 estrellas)
  - Entre categorías diferentes: AND lógico (ej: 4 estrellas Y Piscina Y Cancelación gratuita)
- Actualización de resultados en tiempo real sin recargar página completa (< 1 segundo)
- Contador dinámico muestra cantidad de hoteles disponibles

**Interacción:**
- Clic en checkbox → Filtro se aplica inmediatamente
- Movimiento de slider de precio → Actualiza al soltar (onMouseUp) o con delay (300ms)
- Indicador visual de filtros activos (checkboxes marcados, slider en posición, badge numérico)

**Persistencia:**
- Filtros se mantienen al navegar detalle de hotel y regresar
- Al modificar búsqueda principal, filtros se resetean
- Estado de filtros visible claramente

**Botón limpiar:**
- Remueve todos los filtros aplicados
- Restaura vista a resultados completos sin filtros
- Resetea todos los controles a su estado inicial

**Variaciones móviles:**
- Botón flotante "Filtros": Ícono flotante (🔽) en esquina inferior derecha
- Panel modal: Filtros se abren como modal/bottom sheet desde el fondo
- Filtros apilados verticalmente: Secciones expandibles/colapsables por categoría
- Contador de filtros activos: Badge numérico en botón flotante indicando cantidad aplicada
- Botones de acción fijos: "Limpiar filtros" (secundario) y "Aplicar" (verde primario) en parte inferior del modal
- Cerrar modal: Swipe hacia abajo o tap en overlay oscuro
- Scroll dentro del modal: Permite navegar todos los filtros disponibles

##### ✅ VALIDACIONES DE QA

[PENDIENTE: Agregar validaciones específicas de filtros]

##### 🧪 Escenarios de Prueba

[PENDIENTE: Agregar escenarios específicos de filtros]

---

#### 🔹 Funcionalidad: Cards de Hoteles (Vista Lista)

##### 📖 Descripción Funcional

Listado vertical de tarjetas individuales que muestran información resumida y relevante de cada hotel disponible. Cada card permite acceso rápido al detalle completo del hotel con habitaciones y precios.

##### 🧩 Componentes

**Por cada card:**

- **Imagen del hotel:**
  - Foto principal en alta resolución
  - Indicador de galería: "1/10" si hay múltiples fotos
  - Proporción 16:9 o 4:3 según diseño

- **Nombre del hotel:**
  - Título destacado en negrita
  - Ubicación debajo: "Ciudad, País" (gris, texto más pequeño)

- **Estrellas:**
  - Visualización gráfica: ★★★★ (dorado/amarillo)
  - Número de estrellas según categoría oficial del hotel

- **Servicios destacados (íconos):**
  - 📶 Wi-Fi gratuito
  - 🏊 Piscina
  - 🅿️ Estacionamiento
  - 🍳 Desayuno incluido
  - Máximo 4-5 íconos visibles (los más relevantes)

- **Calificación de huéspedes:**
  - Puntaje numérico: 8.5/10 (ejemplo)
  - Label descriptivo: "Muy bueno" | "Excelente" | "Fabuloso"
  - Número de reseñas: "(124 opiniones)"
  - ⚠️ Pendiente confirmar disponibilidad de calificaciones

- **Precio:**
  - Label: "Desde" (texto pequeño)
  - Precio por noche en Puntos o Plata
  - Ejemplos: "12,000 puntos/noche" o "USD $150/noche"
  - Precio total de estadía (opcional, texto secundario)

- **Política de cancelación:**
  - Badge verde: "Cancelación gratuita" si aplica
  - Badge rojo: "No reembolsable" si aplica
  - Texto pequeño con detalles adicionales

- **Botón de acción:**
  - Botón "Ver habitaciones" o "Ver más" (verde primario)
  - Posicionado en esquina inferior derecha del card

##### 💻 Comportamiento Esperado

**Visualización:**
- Cards se muestran en lista vertical con scroll
- Layout: Imagen izquierda | Información centro | Precio esquina superior derecha
- Espaciado uniforme entre cards con borde gris claro y sombra suave

**Interacción:**
- Hover en card (desktop): Sombra más pronunciada o borde destacado
- Clic en imagen: ⚠️ Pendiente definir: ¿Abre galería de fotos o redirige a detalle?
- Clic en nombre/card completo: ⚠️ Pendiente definir: ¿Abre modal de detalle o redirige a página?
- Clic en botón "Ver habitaciones": Navega a vista de detalle con habitaciones disponibles y precios

**Carga de resultados:**
- Scroll infinito: Carga lazy de cards adicionales conforme usuario navega (load more)
- Indicador de carga mientras se obtienen más resultados
- Sin resultados: Mensaje "No se encontraron hoteles con los criterios seleccionados. Intenta ajustar los filtros."

**Ordenamiento:**
- ⚠️ Pendiente documentar opciones de ordenamiento disponibles
- Posibles opciones: Precio (menor a mayor), Estrellas (mayor a menor), Calificación (mayor a menor), Recomendados

**Variaciones móviles:**
- Cards apiladas verticalmente: Ocupan ancho completo de la pantalla
- Layout reorganizado: Imagen en parte superior, información debajo
- Precio más prominente: Destacado en esquina superior derecha o inferior
- Botón "Ver habitaciones": Ocupa ancho completo en parte inferior del card
- Touch targets optimizados: Áreas de toque ampliadas para mejor UX móvil
- Galería de imágenes: Swipe horizontal sobre imagen principal para ver más fotos
- Servicios en una fila: Íconos en línea horizontal con scroll si exceden espacio
##### ✅ VALIDACIONES DE QA

[PENDIENTE: Agregar validaciones específicas de cards de hoteles]

##### 🧪 Escenarios de Prueba

[PENDIENTE: Agregar escenarios específicos de cards de hoteles]
---

## 💳 MÓDULO: CHECKOUT

> ⚠️ **Documentación en proceso**  
> Este módulo está siendo estandarizado. Se está trabajando en la documentación de: Datos de huéspedes, Contacto, Métodos de pago, Resumen de reserva, Políticas del hotel.  
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
✅ Campos obligatorios: Destino, check-in, check-out  
✅ Habitaciones/huéspedes: Mínimo 1 habitación y 1 adulto  
✅ Botón buscar: Habilitado solo con campos completos  
✅ Fechas: Check-out posterior a check-in, no fechas pasadas  
✅ Modal de destinos: Búsqueda en tiempo real, lista de resultados  
✅ Calendario: Navegación mes/año, rango visual correcto

**Disponibilidad:**
✅ Widget persistente: Resumen correcto de criterios de búsqueda  
✅ Filtros laterales: Actualización en tiempo real sin recargar  
✅ Cards de hoteles: Información completa (nombre, estrellas, servicios, precio)  
✅ Carga lazy: Resultados adicionales al hacer scroll  
✅ Ordenamiento: ⚠️ Pendiente documentar opciones de orden (precio, estrellas, etc.)

**Detalle de Hotel:**
⚠️ Pendiente documentar: Galería de fotos, descripción completa, ubicación en mapa, habitaciones disponibles

**Checkout:**
⚠️ Pendiente documentar: Datos de huéspedes, contacto, métodos de pago

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
⚠️ **PENDIENTE CONFIRMAR:** ¿Precio por noche o total? ¿Slider ajusta por noche o estadía completa?

### Validaciones de Experiencia de Usuario (UI/UX):

✅ **Modal de destinos:** Experiencia fluida de búsqueda y selección  
✅ **Calendario:** Navegación intuitiva, rango visual claro  
✅ **Dropdown habitaciones:** Controles +/- funcionales, límites validados  
✅ **Responsive:** Adaptación correcta a móviles (sticky buttons, modals fullscreen)  
✅ **Estados de carga:** Indicadores visuales durante búsqueda/filtrado  
✅ **Mensajes de error:** Claros y orientados a acción del usuario  
✅ **Accesibilidad:** Componentes navegables por teclado y lectores de pantalla

---

## 📝 FORMATO DE TÍTULO

```
[PROM] Hoteles - [Módulo/Escenario] - [Variante]
```

**Ejemplos actualizados:**

- `[PROM] Hoteles - Home - Búsqueda - HotelBeds - 2 personas - 1 habitación - Puntos + Plata`
- `[PROM] Hoteles - Disponibilidad - Filtros - 4★ + Piscina + Cancelación gratuita - Puntos + Plata`
- `[PROM] Hoteles - Home - Búsqueda - HotelBeds - 1 persona - 1 habitación - Solo Puntos`

---

## 🚀 PRÓXIMOS PASOS PARA COMPLETAR ESTE ARCHIVO

### Módulos Documentados:

✅ **Componentes Transversales** - Referencia a vuelos (Header, Tabs, Footer)  
✅ **Pasos Obligatorios del Flujo E2E** - 25 pasos documentados (pasos 1-15 completos, 16-25 pendientes)  
✅ **Módulo Home/Login** - Widget de búsqueda con 5 componentes + Modal destinos + Calendario + Dropdown  
✅ **Módulo Disponibilidad** - 3 funcionalidades: Widget persistente, Filtros laterales, Cards de hoteles

### Módulos Pendientes:

**1. Disponibilidad - Completar:**

- Vista de detalle del hotel (modal o página)
- Galería de fotos del hotel
- Descripción completa y servicios
- Ubicación en mapa
- Habitaciones disponibles con precios individuales
- Slider Puntos + Plata (ubicación y comportamiento)
- Opciones de ordenamiento (precio, estrellas, calificación)

**2. Checkout:**

- Resumen de reserva (hotel, fechas, habitaciones)
- Formulario de datos de huéspedes principales
- Datos de contacto (email, teléfono)
- Huéspedes adicionales (si aplica)
- Solicitudes especiales (cama extra, horario check-in, etc.)
- Métodos de pago (integración con gateway)
- Términos y condiciones del hotel

**3. Confirmación:**

- Confirmación exitosa (código de reserva, voucher PDF)
- Email de confirmación automático
- Información de contacto del hotel
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

- ⚠️ **CRÍTICO:** Confirmar reglas y ubicación del slider en Hoteles (disponibilidad, detalle o checkout)
- Porcentaje mínimo de puntos requerido
- Fórmula de cálculo Puntos ↔ Plata (por noche o estadía completa)
- Ubicación del slider (disponibilidad, detalle, checkout)

**Políticas de Producto:**

- Edades de niños permitidas (rangos)
- Máximo de habitaciones por reserva
- Máximo de huéspedes por habitación
- Políticas de cancelación por tipo de tarifa
- Prepago vs pago en hotel
- Impuestos incluidos o adicionales

**Proceso de Reserva:**

- Definir si emisión es automática o manual
- Tiempos de confirmación esperados
- Estados de reserva durante el proceso
- Disponibilidad de voucher
- Proceso de cancelación de reservas confirmadas

---

## 📚 REFERENCIAS

**Guías relacionadas:**

- [PROM_QA_Assistant.agent.md](../../../../agents/PROM_QA_Assistant.agent.md) - Valores globales PROM (URL, país, modelo de negocio)
- [PROM_VUELOS.md](PROM_VUELOS.md) - Referencia para estructura y componentes transversales

---

## 🔄 CONTROL DE CAMBIOS

### Versión 1.0 - 2026-01-25

**Cambios principales:**

- ✅ Aplicada jerarquía completa según estructura definida por el equipo: H1 (Producto) → H2 (Módulo) → H3 (Descripción/FUNCIONALIDADES) → H4 (Funcionalidad) → H5 (📖 Descripción, 🧩 Componentes, 💻 Comportamiento esperado)
- ✅ **MÓDULO HOME:** Widget de Búsqueda reorganizado completamente
  - Modal de Destinos, Calendario y Dropdown integrados en 💻 Comportamiento esperado (ya no como secciones H3 separadas)
  - Estructura correcta: H2 MÓDULO → H3 Descripción del Módulo + FUNCIONALIDADES → H4 Widget → H5 📖🧩💻🎨(Variaciones Móviles)
  - Componentes detallados: Campo Destino, Fechas, Habitaciones, Botón Buscar con comportamientos completos
- ✅ **MÓDULO DISPONIBILIDAD:** 3 funcionalidades reestructuradas con jerarquía correcta
  - H3 Descripción del Módulo + FUNCIONALIDADES → H4 (Widget Persistente, Filtros Laterales, Cards) → H5 📖🧩💻🎨
  - Filtros Laterales: 5 categorías (Precio, Estrellas, Tipo, Servicios, Cancelación) con comportamiento en tiempo real
  - Cards de Hoteles: 8 componentes por card (Imagen, Nombre, Estrellas, Servicios, Calificación, Precio, Política, Botón)
- ✅ Preservados todos los flujos E2E y contenido existente sin modificaciones (solo cambios estructurales)
- ✅ Modelo confirmado: Puntos + Plata (Slider)
- ✅ Proveedor: HotelBeds

### Versión 0.2 - 2026-01-20

**Cambios principales:**

- ✅ Identificado modelo de negocio B2B2C Transversal
- ✅ Agregados 7 países soportados (CR, PA, HN, DO, GT, SV, NI)

### Versión 0.1 - 2026-01-20

**Cambios principales:**

- ✅ Template inicial creado con estructura base
- ✅ Definidas secciones principales del documento

---

**Estado:** 🔄 Template - Completar con información específica de Promerica
