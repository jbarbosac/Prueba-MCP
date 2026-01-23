# 🚗 FLUJO E2E OBLIGATORIO PARA AUTOS - PROMERICA REWARDS

> **📖 Información Global:** Ver [PROM_QA_Assistant.agent.md](../../../../agents/PROM_QA_Assistant.agent.md) para URL del portal, país activo, modelo de negocio y versión del marketplace.

---

## 📦 PROVEEDORES DISPONIBLES

⚠️ **PENDIENTE DE DEFINIR**

**Proveedores potenciales:**

- Sabre → Hertz, Dollar, Thrifty
- [Otros por confirmar]

---

## 🔧 COMPONENTES TRANSVERSALES

> **Nota:** Estos componentes son compartidos por todos los productos del marketplace (Vuelos, Autos, Hoteles, Disney, Actividades). Ver detalle completo en [PROM_VUELOS.md](PROM_VUELOS.md#-componentes-transversales).

### Header Global

Barra superior con navegación principal, branding personalizado de Promerica y acceso de usuario.

### Tabs de Productos

Pestañas horizontales para navegación entre productos (Vuelos, **Autos**, Hoteles, Disney, Actividades).

### Footer Global

Sección inferior con información institucional y canales de contacto personalizados por país.

---

## 📋 PASOS OBLIGATORIOS DEL FLUJO E2E

**Siempre incluir estos pasos desde login para el flujo completo de Autos:**

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
17. **Seleccionar vehículo** → Clic en card o botón dentro de card | ⚠️ Pendiente documentar: ¿Abre detalle expandido o redirige directo a checkout?
18. **Revisar protecciones y seguros** → ⚠️ Pendiente documentar modal específico | ⚠️ Pendiente documentar opciones y comportamiento
19. **Ajustar slider Puntos + Plata** → ⚠️ Pendiente documentar ubicación y comportamiento | ⚠️ Pendiente documentar validación de saldo
20. **Continuar a Checkout** → Clic en botón de confirmación | ⚠️ Pendiente documentar validaciones de checkout

**⚠️ ADVERTENCIA: Los siguientes pasos (21-25) deben ejecutarse SOLO con búsquedas de 1 día para evitar costos reales:**

21. **Completar datos del conductor** → Llenar formulario con información requerida y licencia | ⚠️ Pendiente documentar campos específicos | 🚨 **Usar solo 1 día desde este punto**
22. **Seleccionar método de pago** → Ingresar datos de tarjeta si hay copago en plata | ⚠️ Pendiente documentar proceso de pago
23. **Confirmar reserva** → Clic en botón de confirmación final | ⚠️ Pendiente documentar proceso de emisión
24. **Validar confirmación** → Verificar código de reserva, voucher | ⚠️ Pendiente documentar datos mostrados
25. **Verificar en Admin** → Buscar reserva en aplicativo Admin | ⚠️ Pendiente documentar validaciones de backend

**Nota:** Los pasos 17-25 están pendientes de documentación completa según información de módulos Detalle, Checkout, Confirmación y Admin.

---

## 🏠 MÓDULO: HOME/LOGIN

**Descripción:** Página principal del marketplace donde el usuario accede al buscador de autos y navega entre productos disponibles. La interfaz es personalizable según el país configurado (Costa Rica en Test).

---

### Widget de Búsqueda de Autos

**Descripción:** Formulario principal para búsqueda de autos con selectores de ubicación, fechas y opciones de descuento.

**Componentes:**

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

**Comportamiento esperado:**

- **Recogida:** Clic abre modal de búsqueda por localidades (búsqueda avanzada con mapa)
- **Devolución:** Clic despliega dropdown categorizado (acceso rápido) o link para modal completo
- Toggle permite alternar entre configurar recogida o devolución
- **Calendario:** Permite seleccionar rango de fechas + horas/minutos específicas
- **Descuentos Hertz:** Expansible, código opcional, se agrega con botón verde
- **Descuentos Promocionales:** Dropdown predefinido o campo manual si activa checkbox
- **Validación:** Recogida, devolución y fechas son obligatorias antes de buscar
- Al hacer clic en "Buscar" → Redirige a módulo de Disponibilidad con resultados filtrados

**Variaciones Móviles:**

- **Toggle "Pago en línea":** Aparece en la parte superior del widget (no visible en desktop)
- **Modal de Recogida/Devolución:** Vista simplificada en pantalla completa con lista de aeropuertos y ciudades
- **Mapa:** Accesible mediante interacción adicional
- **Calendario:** Ocupa pantalla completa con navegación táctil
- **Selectores de hora/minutos:** Aparecen como ruedas nativas (picker wheels) debajo del calendario
- **Secciones de descuentos:** Se expanden en pantalla completa cuando el usuario interactúa
- **Botón "Buscar":** Permanece fijo (sticky) en la parte inferior de la pantalla

---

### Modal de Búsqueda por Localidades

**Descripción:** Modal emergente que permite buscar y seleccionar ubicaciones mediante campo de búsqueda, filtros de ciudades, lista de resultados y mapa interactivo sincronizado.

**Componentes:**

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

**Comportamiento esperado:**

- **Apertura:** Clic en "Recogida" o "Devolución" del widget principal
- **Búsqueda:** Usuario escribe ciudad/localidad → Sistema filtra en tiempo real
- **Resultados encontrados:** Aparecen tabs de ciudades, contador y lista de ubicaciones
- **Sincronización:** Hover en lista resalta marcador en mapa | Clic en marcador resalta item en lista
- **Filtros:** Clic en tab de ciudad actualiza lista y mapa con ubicaciones de esa ciudad
- **Selección:** Clic en botón "Seleccionar" → Cierra modal y actualiza campo correspondiente
- **Sin resultados:** Muestra mensaje de estado vacío (sin tabs ni lista)
- **Cerrar:** Botón X o clic fuera → Cierra sin cambios

---

## 📋 MÓDULO: DISPONIBILIDAD

**Descripción:** Módulo que muestra los resultados de búsqueda de autos disponibles según los criterios del usuario. Incluye widget persistente, categorías, filtros y dos vistas (lista/matriz).

---

### Widget de Búsqueda Persistente

**Descripción:** Resumen compacto de criterios de búsqueda que permanece visible en la parte superior del módulo de disponibilidad.

**Componentes:**

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

**Comportamiento esperado:**

- **Widget persistente:** Permanece visible mientras el usuario navega los resultados
- **Edición de criterios:** Clic en cualquier campo permite modificar búsqueda
- **Botón "Buscar":** Actualiza resultados con nuevos criterios sin recargar página
- **Ocultar/Mostrar:** Colapsa widget para dar más espacio a resultados

**Variaciones Móviles:**

- **Widget colapsado por defecto:** Aparece como barra compacta con resumen
- **Expansión del widget:** Tap en barra compacta expande en pantalla completa
- **Campos de ubicación:** Abren pantalla completa con lista scrollable
- **Selector de fechas:** Calendario en pantalla completa con ruedas nativas
- **Botón "Buscar":** Sticky en la parte inferior
- **Botón "Cerrar/Colapsar":** Icono X permite volver a vista compacta

---

### Categorías de Vehículos

**Descripción:** Navegación por pestañas para filtrar rápidamente por categoría de auto.

**Componentes:**

1. **Pestañas horizontales con íconos:**
   - 🚗 **Standard** (activo - borde verde)
   - 🚙 **Intermediate**
   - 🚐 **SUV**
   - 🛻 **Truck/Van**
   - 🏎️ **Premium**
   - 🌿 **Green**

2. **Indicadores visuales:**
   - Pestaña activa: Fondo blanco con borde verde en parte inferior
   - Pestañas inactivas: Fondo gris claro
   - Ícono de vehículo representativo en cada pestaña

3. **Controles de vista (esquina superior derecha):**
   - 📋 **Botón Lista** (3 líneas horizontales)
   - 📊 **Botón Matriz** (cuadrícula 3x3)
   - Botón activo en verde

**Comportamiento esperado:**

- **Clic en pestaña:** Filtra resultados por categoría seleccionada
- **Visual feedback:** Pestaña activa se destaca con borde verde
- **Cambio de vista:** Botones Lista/Matriz alternan visualización de resultados
- **Estado persistente:** Categoría seleccionada se mantiene al cambiar vista

**Variaciones Móviles:**

- **Scroll horizontal:** Pestañas se desplazan horizontalmente con swipe táctil
- **Indicador de scroll:** Puntos o barra indica que hay más pestañas fuera de vista
- **Botones de vista reducidos:** Iconos más pequeños pero mantienen funcionalidad
- **Pestañas compactas:** Reducción de padding sin sacrificar legibilidad
- **Touch feedback:** Animación rápida al tocar pestaña

---

### Filtros

**Descripción:** Panel lateral de filtros para refinar búsqueda de autos según tipo, rentadora y transmisión.

**Componentes:**

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

**Comportamiento esperado:**

- **Clic en dropdown:** Despliega lista de opciones disponibles
- **Selección:** Al elegir opción → Actualiza resultados en tiempo real
- **Múltiples filtros:** Se aplican de forma acumulativa (filtro AND)
- **Resetear:** Seleccionar "Todas" vuelve al estado inicial del filtro
- **Persistencia:** Los filtros se mantienen al cambiar entre vista lista/matriz

**Variaciones Móviles:**

- **Botón flotante "Filtros":** Ícono flotante (🔽) en esquina inferior derecha
- **Panel modal:** Filtros como modal/sheet desde el fondo (70-80% altura)
- **Filtros apilados verticalmente:** Cada filtro ocupa ancho completo
- **Dropdowns nativos:** Utilizan selectores nativos del sistema operativo
- **Contador de filtros activos:** Badge numérico en botón flotante
- **Botones de acción:** "Limpiar filtros" y "Aplicar" (verde) en parte inferior
- **Cerrar modal:** Swipe hacia abajo o tap en overlay oscuro

---

### Cards de Resultados (Vista Lista)

**Descripción:** Tarjetas individuales que muestran información detallada de cada vehículo disponible.

**Componentes (por cada card):**

1. **Ícono de información (i):** Esquina superior izquierda del card

2. **Imagen del vehículo:** Foto lateral del auto en alta resolución

3. **Categoría y Modelo:**
   - Título: "Economic" | "Compact" | "Intermediate" (negrita)
   - Subtítulo: "Ford Focus o Similar" (gris)

4. **Especificaciones con íconos:**
   - 👤 **Pasajeros:** Número (ej: 4)
   - 🧳 **Maletas grandes:** Número (ej: 2)
   - 💼 **Maletas pequeñas:** Número (ej: 2)
   - ⚙️ **Transmisión:** Ícono de automático (A)

5. **Precio:**
   - Label: "Desde" (pequeño, parte superior derecha)
   - Precio: "USD $300" (grande, negrita)
   - ⚠️ **Pendiente:** ¿Se muestra en Puntos + Plata también?

6. **Logos de Rentadoras:**
   - Badges rectangulares con logos: Thrifty, Dollar, Hertz
   - Alineados horizontalmente en la parte inferior

**Diseño Visual:**

- Card con borde gris claro y sombra suave
- Espaciado uniforme entre elementos
- Íconos en color gris/negro con estilo minimalista
- Logos de rentadoras con bordes redondeados

**Comportamiento esperado:**

- **Hover en card:** Sombra más pronunciada o borde destacado
- **Clic en ícono (i):** Muestra tooltip con información adicional del vehículo
- **Clic en card completo:** ⚠️ Pendiente definir: ¿Abre modal de detalle o redirige a checkout?
- **Clic en logo rentadora:** ⚠️ Pendiente definir: ¿Filtra por esa compañía?
- **Scroll:** Carga lazy de cards adicionales conforme usuario navega

**Variaciones Móviles:**

- **Cards apiladas verticalmente:** Ocupan ancho completo con scroll vertical
- **Imagen más pequeña:** Proporción reducida para optimizar espacio
- **Layout reorganizado:** Información en dos columnas (specs izquierda, precio derecha)
- **Logos de rentadoras:** Lista horizontal scrollable si son muchos
- **Precio más prominente:** Tamaño aumentado para mejor visibilidad
- **Touch targets:** Áreas de toque más grandes para botones

---

### Vista Matriz de Comparación

**Descripción:** Tabla comparativa que permite ver múltiples vehículos lado a lado.

⚠️ **PENDIENTE:** El Knowledge Base menciona esta funcionalidad pero no detalla los componentes específicos.

**Componentes esperados:**

- Tabla con columnas por vehículo
- Filas comparativas de características
- Encabezado con imagen y modelo
- Precios alineados
- Botones de selección por columna

**Comportamiento esperado:**

- Scroll horizontal en vista de tabla
- Comparación visual rápida de características
- Selección directa desde la tabla

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
✅ Vista Matriz: Comparación lado a lado (pendiente documentar)  
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
[PROM] Autos - [Días] - [Rentadora] - [Dropoff] - [Tipo de vehículo] - [Modelo de pago]
```

**Ejemplos actualizados:**

- `[PROM] Autos - 5 días - Hertz - Dropoff diferente - SUV - Puntos + Plata`
- `[PROM] Autos - 3 días - Dollar - Mismo lugar - Económico - Solo Puntos`
- `[PROM] Autos - 7 días - Thrifty - Mismo lugar - Standard - Puntos + Plata (60%)`

---

## 🚀 PRÓXIMOS PASOS PARA COMPLETAR ESTE ARCHIVO

### Módulos Documentados:

✅ **Componentes Transversales** - Referencia a vuelos (Header, Tabs, Footer)  
✅ **Pasos Obligatorios del Flujo E2E** - 25 pasos documentados (pasos 1-16 completos, 17-25 pendientes)  
✅ **Módulo Home/Login** - Widget de búsqueda con 7 componentes + Modal de localidades  
✅ **Módulo Disponibilidad** - 5 funcionalidades: Widget persistente, Categorías, Filtros, Cards Lista, Vista Matriz (parcial)

### Módulos Pendientes:

**1. Disponibilidad - Completar:**

- Vista Matriz de Comparación (detalles de componentes)
- Modal de Protecciones y Seguros
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
