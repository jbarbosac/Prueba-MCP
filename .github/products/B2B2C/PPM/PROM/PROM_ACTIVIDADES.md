# 🎢 FLUJO E2E OBLIGATORIO PARA ACTIVIDADES - PROMERICA REWARDS

> **📖 Información Global:** Ver [PROM_QA_Assistant.agent.md](../../../../agents/PROM_QA_Assistant.agent.md) para URL del portal, país activo, modelo de negocio y versión del marketplace.

---

## 📦 PROVEEDORES DISPONIBLES

**Proveedor confirmado:**

- **HotelBeds** (proveedor principal para actividades)

⚠️ **Pendiente validar:** Si existen proveedores adicionales o alternativas

---

## 🔧 COMPONENTES TRANSVERSALES

> **Nota:** Estos componentes son compartidos por todos los productos del marketplace (Vuelos, Autos, Hoteles, Disney, **Actividades**). Ver detalle completo en [PROM_VUELOS.md](PROM_VUELOS.md#-componentes-transversales).

### Header Global

Barra superior con navegación principal, branding personalizado de Promerica y acceso de usuario.

### Tabs de Productos

Pestañas horizontales para navegación entre productos (Vuelos, Autos, Hoteles, Disney, **Actividades**).

### Footer Global

Sección inferior con información institucional y canales de contacto personalizados por país.

---

## 📋 PASOS OBLIGATORIOS DEL FLUJO E2E

**Siempre incluir estos pasos desde login para el flujo completo de Actividades:**

1. **Acceder al portal** → https://traveltest-club-promerica.preprodppm.com/es-cr | El portal carga correctamente y muestra la pantalla de inicio
2. **Realizar login** → Ingresar usuario y contraseña válidos | Login exitoso y acceso al home con tabs de productos visibles
3. **Navegar a Actividades** → Clic en tab "Actividades" | Widget de búsqueda de actividades se muestra correctamente
4. **Seleccionar destino** → Clic en campo "Destino" o "¿A dónde quieres ir?" | Modal de búsqueda de destinos se abre
5. **Buscar y seleccionar ciudad** → Escribir ciudad/país en buscador | Sistema filtra resultados y muestra lista de destinos
6. **Confirmar destino** → Clic en ciudad deseada de la lista | Modal se cierra y campo "Destino" se actualiza con selección
7. **Seleccionar fecha** → Clic en campo "Fecha" o calendario | Calendario mensual se abre
8. **Confirmar fecha de actividad** → Seleccionar fecha específica | Calendario se cierra y campo muestra fecha seleccionada
9. **Configurar participantes** → Clic en campo "Participantes" o "Viajeros" | Dropdown de participantes se abre
10. **Ajustar cantidades por edad** → Seleccionar adultos, niños, infantes según rangos de edad | Campos se actualizan con cantidades
11. **Confirmar participantes** → Clic en "Listo" o fuera del dropdown | Dropdown se cierra y campo muestra resumen (ej: "2 adultos, 1 niño")
12. **Ejecutar búsqueda** → Clic en botón "Buscar" verde | Sistema redirige a módulo de Disponibilidad con resultados
13. **Revisar widget de búsqueda persistente** → Verificar resumen de criterios en parte superior | Widget compacto muestra destino, fecha, participantes
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

**Descripción:** Página principal del marketplace donde el usuario accede al buscador de actividades y navega entre productos disponibles. La interfaz es personalizable según el país configurado (Costa Rica en Test).

---

### Widget de Búsqueda de Actividades

**Descripción:** Formulario principal para búsqueda de actividades con selectores de destino, fecha y participantes.

**Componentes:**

1. **Selector "Destino":**
   - Campo con ícono de ubicación
   - Placeholder: "¿A dónde quieres ir?"
   - Clic abre modal de búsqueda de destinos

2. **Selector "Fecha":**
   - Campo con ícono de calendario
   - Placeholder: "Selecciona tu fecha"
   - Clic abre calendario mensual
   - Nota: Actividades típicamente requieren solo UNA fecha (día de la actividad)

3. **Selector "Participantes" o "Viajeros":**
   - Campo con ícono de personas
   - Placeholder: "Participantes"
   - Clic abre dropdown con controles por rango de edad

4. **Botón Buscar:**
   - Botón verde para ejecutar la búsqueda
   - Deshabilitado si faltan campos obligatorios

**Comportamiento esperado:**

- **Destino:** Clic abre modal con buscador de ciudades/países
- **Fecha:** Clic abre calendario mensual con navegación, validación de fechas pasadas
- **Participantes:** Dropdown con controles + / - por rango de edad (adultos, niños, infantes)
- **Validación:** Destino, fecha y participantes son obligatorios antes de buscar
- Al hacer clic en "Buscar" → Redirige a módulo de Disponibilidad con resultados filtrados

**Variaciones Móviles:**

- **Campos apilados verticalmente:** Cada campo ocupa ancho completo
- **Modal de destino:** Pantalla completa con buscador
- **Calendario:** Vista en pantalla completa con navegación táctil
- **Dropdown participantes:** Expansión fullscreen con controles grandes
- **Botón "Buscar":** Sticky en la parte inferior de la pantalla

---

### Modal de Búsqueda de Destinos

**Descripción:** Modal emergente que permite buscar y seleccionar destinos para actividades.

**Componentes:**

- **Título del Modal:** "¿A dónde quieres ir?" o "Buscar destino"
- **Botón Cerrar (X):** Esquina superior derecha
- **Campo de Búsqueda:**
  - Barra de texto con ícono de lupa
  - Placeholder: "Ciudad o país"
- **Lista de Resultados:**
  - Panel scrollable con formato: Nombre Ciudad | País
  - Ejemplo: "San José | Costa Rica"
- **Sugerencias Populares (opcional):**
  - Lista de destinos frecuentes o destacados
  - Aparece cuando el campo está vacío
- **Mensaje de Estado Vacío:**
  - "No se encontraron resultados"
  - "Intenta con otro destino"

**Comportamiento esperado:**

- **Apertura:** Clic en campo "Destino" del widget principal
- **Búsqueda:** Usuario escribe destino → Sistema filtra en tiempo real
- **Resultados encontrados:** Muestra lista de ciudades coincidentes
- **Selección:** Clic en destino → Cierra modal y actualiza campo "Destino"
- **Sin resultados:** Muestra mensaje de estado vacío
- **Cerrar:** Botón X o clic fuera → Cierra sin cambios

---

### Calendario de Fecha

**Descripción:** Componente de calendario para seleccionar fecha de la actividad.

**Componentes:**

- **Navegación de Mes/Año:**
  - Flechas izquierda/derecha para cambiar mes
  - Selector de mes y año en encabezado
- **Grilla de Días:**
  - Días de la semana (Lun-Dom)
  - Días del mes con estado visual
- **Indicadores Visuales:**
  - Día actual destacado
  - Fechas pasadas deshabilitadas
  - Fecha seleccionada (verde)
- **Botones de Acción:**
  - "Cancelar" (cierra sin cambios)
  - "Aceptar" (confirma selección) - botón verde

**Comportamiento esperado:**

- **Selección:** Clic en día disponible establece fecha de actividad
- **Validación:** No permite seleccionar fechas pasadas
- **Visual feedback:** Fecha seleccionada se destaca en verde
- **Cancelar:** Cierra calendario sin aplicar cambios
- **Aceptar:** Actualiza campo y cierra calendario

---

### Dropdown Participantes

**Descripción:** Control desplegable para configurar cantidad de participantes por rango de edad.

**Componentes:**

1. **Adultos:**
   - Label: "Adultos" (edad: ⚠️ Pendiente definir rango, típicamente 12+ o 18+)
   - Controles: Botón "-" | Número | Botón "+"
   - Rango: Mínimo 1, máximo ⚠️ por definir

2. **Niños:**
   - Label: "Niños" (edad: ⚠️ Pendiente definir rango, típicamente 3-11)
   - Controles: Botón "-" | Número | Botón "+"
   - Rango: Mínimo 0, máximo ⚠️ por definir
   - ⚠️ **Pendiente:** Validar si requiere edad específica de cada niño

3. **Infantes (opcional):**
   - Label: "Infantes" (edad: ⚠️ Pendiente definir rango, típicamente 0-2)
   - Controles: Botón "-" | Número | Botón "+"
   - Rango: Mínimo 0, máximo ⚠️ por definir

4. **Botón "Listo":**
   - Botón verde para confirmar configuración

**Comportamiento esperado:**

- **Incremento/Decremento:** Botones +/- ajustan cantidades
- **Límites:** Botones se deshabilitan al alcanzar mínimo/máximo
- **Validación:** Mínimo 1 participante (típicamente al menos 1 adulto)
- **Edades específicas:** ⚠️ Pendiente definir si solicita edad exacta de niños/infantes
- **Resumen:** Al cerrar, campo principal muestra "X adulto(s), Y niño(s), Z infante(s)"

**Variaciones Móviles:**

- **Pantalla completa:** Dropdown ocupa toda la pantalla
- **Controles más grandes:** Botones +/- con áreas táctiles amplias
- **Botón "Listo":** Sticky en parte inferior

---

## 📋 MÓDULO: DISPONIBILIDAD

**Descripción:** Módulo que muestra los resultados de búsqueda de actividades disponibles según los criterios del usuario. Incluye widget persistente, filtros laterales y cards de actividades.

---

### Widget de Búsqueda Persistente

**Descripción:** Resumen compacto de criterios de búsqueda que permanece visible en la parte superior del módulo de disponibilidad.

**Componentes:**

1. **Campo "Destino":**
   - Muestra destino seleccionado (ej: "San José, Costa Rica")
   - Ícono de ubicación
   - Clic abre modal de destinos

2. **Campo "Fecha":**
   - Muestra fecha con formato corto (ej: "22 Oct 2026")
   - Ícono de calendario
   - Clic abre calendario

3. **Campo "Participantes":**
   - Muestra resumen (ej: "2 adultos, 1 niño")
   - Ícono de personas
   - Clic abre dropdown de configuración

4. **Botón "Buscar":** Botón verde para ejecutar nueva búsqueda

5. **Link "Ocultar búsqueda":** Texto pequeño para colapsar widget

**Comportamiento esperado:**

- **Widget persistente:** Permanece visible mientras el usuario navega los resultados
- **Edición de criterios:** Clic en cualquier campo permite modificar búsqueda
- **Botón "Buscar":** Actualiza resultados con nuevos criterios sin recargar página
- **Ocultar/Mostrar:** Colapsa widget para dar más espacio a resultados

**Variaciones Móviles:**

- **Widget colapsado por defecto:** Barra compacta con resumen
- **Expansión:** Tap expande en pantalla completa
- **Campos:** Abren modales/calendarios fullscreen
- **Botón "Buscar":** Sticky en la parte inferior

---

### Filtros Laterales

**Descripción:** Panel lateral de filtros para refinar búsqueda de actividades según múltiples criterios.

**Componentes:**

1. **Título de Sección:** "Filtros" (texto destacado)

2. **Filtro: Categoría de Actividad**
   - Checkboxes: Tours, Experiencias, Parques, Museos, Deportes, Acuáticas, Aventura, Cultural, etc.
   - ⚠️ Pendiente confirmar categorías disponibles en HotelBeds
   - Selección múltiple permitida

3. **Filtro: Precio**
   - Rango de precio con slider doble
   - Valores mínimo y máximo mostrados
   - Formato: Puntos o Plata según configuración

4. **Filtro: Duración**
   - Checkboxes: Menos de 4 horas, 4-8 horas (medio día), Más de 8 horas (día completo), Varios días
   - ⚠️ Pendiente confirmar opciones disponibles
   - Selección múltiple permitida

5. **Filtro: Horario/Momento del día (opcional)**
   - Checkboxes: Mañana, Tarde, Noche
   - ⚠️ Pendiente confirmar si está disponible

6. **Filtro: Incluye**
   - Checkboxes: Transporte, Comida, Guía, Entradas, Equipo, etc.
   - ⚠️ Pendiente confirmar servicios disponibles
   - Selección múltiple permitida

7. **Filtro: Cancelación**
   - Checkboxes: Cancelación gratuita, Reembolsable parcialmente, No reembolsable
   - ⚠️ Pendiente confirmar opciones disponibles

8. **Botón "Limpiar filtros":**
   - Link o botón para resetear todos los filtros

**Diseño Visual:**

- Panel fijo en lado izquierdo de la pantalla
- Fondo blanco con bordes suaves
- Espaciado vertical entre secciones de filtro
- Checkboxes y sliders con estilo Promerica (verde)

**Comportamiento esperado:**

- **Clic en checkbox:** Activa/desactiva filtro
- **Slider de precio:** Ajuste dinámico de rango
- **Selección múltiple:** Se aplican de forma acumulativa (AND dentro de categoría, OR entre categorías)
- **Actualización en tiempo real:** Resultados se actualizan al aplicar filtros
- **Limpiar filtros:** Vuelve al estado inicial (todos desactivados)
- **Persistencia:** Los filtros se mantienen al navegar detalles de actividades

**Variaciones Móviles:**

- **Botón flotante "Filtros":** Ícono flotante (🔽) en esquina inferior
- **Panel modal:** Filtros como modal/sheet desde el fondo
- **Filtros apilados verticalmente:** Expansibles por sección
- **Contador de filtros activos:** Badge numérico en botón flotante
- **Botones de acción:** "Limpiar filtros" y "Aplicar" (verde) en parte inferior
- **Cerrar modal:** Swipe hacia abajo o tap en overlay

---

### Cards de Actividades (Vista Lista)

**Descripción:** Tarjetas individuales que muestran información detallada de cada actividad disponible.

**Componentes (por cada card):**

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
[PROM] Actividades - [Ciudad] - [Tipo] - [Participantes] - [Modelo de pago]
```

**Ejemplos actualizados:**

- `[PROM] Actividades - San José - City Tour - 2 adultos - Puntos + Plata`
- `[PROM] Actividades - Cancún - Snorkel - 4 personas (2A 2N) - Solo Puntos`
- `[PROM] Actividades - Quito - Aventura - 3 adultos 1 niño - Puntos + Plata (70%)`

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

- ⚠️ **CRÍTICO:** Confirmar si aplica slider en actividades como en otros productos
- Porcentaje mínimo de puntos requerido
- Fórmula de cálculo Puntos ↔ Plata (por persona o total)
- Ubicación del slider (disponibilidad, detalle, checkout)

**Políticas de Producto:**

- Rangos de edad por categoría (adultos, niños, infantes)
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

- [SHARED_QA_RULES.md](../../../../shared/SHARED_QA_RULES.md) - Fundamentos ISTQB y Azure DevOps
- [PROM_COMMON_RULES.md](../../../../shared/Reglas Marketplace/PROM_COMMON_RULES.md) - Reglas comunes Promerica
- [PROM_VUELOS.md](PROM_VUELOS.md) - Referencia para estructura y componentes transversales

---

## 🔄 CONTROL DE CAMBIOS

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
