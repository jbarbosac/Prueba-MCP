# 🏨 FLUJO E2E OBLIGATORIO PARA HOTELES - PROMERICA REWARDS

> **📖 Información Global:** Ver [PROM_QA_Assistant.agent.md](../../../../agents/PROM_QA_Assistant.agent.md) para URL del portal, país activo, modelo de negocio y versión del marketplace.

---

## 📦 PROVEEDORES DISPONIBLES

**Proveedor confirmado:**

- **HotelBeds** (proveedor principal para hoteles)

⚠️ **Pendiente validar:** Si existen proveedores adicionales o alternativas

---

## 🔧 COMPONENTES TRANSVERSALES

> **Nota:** Estos componentes son compartidos por todos los productos del marketplace (Vuelos, Autos, **Hoteles**, Disney, Actividades). Ver detalle completo en [PROM_VUELOS.md](PROM_VUELOS.md#-componentes-transversales).

### Header Global

Barra superior con navegación principal, branding personalizado de Promerica y acceso de usuario.

### Tabs de Productos

Pestañas horizontales para navegación entre productos (Vuelos, Autos, **Hoteles**, Disney, Actividades).

### Footer Global

Sección inferior con información institucional y canales de contacto personalizados por país.

---

## 📋 PASOS OBLIGATORIOS DEL FLUJO E2E

**Siempre incluir estos pasos desde login para el flujo completo de Hoteles:**

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
11. **Confirmar configuración** → Clic en "Listo" o fuera del dropdown | Dropdown se cierra y campo muestra resumen (ej: "1 habitación, 2 adultos")
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

**Descripción:** Página principal del marketplace donde el usuario accede al buscador de hoteles y navega entre productos disponibles. La interfaz es personalizable según el país configurado (Costa Rica en Test).

---

### Widget de Búsqueda de Hoteles

**Descripción:** Formulario principal para búsqueda de hoteles con selectores de destino, fechas y configuración de habitaciones/huéspedes.

**Componentes:**

1. **Selector "Destino":**
   - Campo con ícono de ubicación
   - Placeholder: "Ingresa tu destino"
   - Clic abre modal de búsqueda de destinos

2. **Selector "Check-in":**
   - Campo con ícono de calendario
   - Placeholder: "Fecha de entrada"
   - Clic abre calendario mensual

3. **Selector "Check-out":**
   - Campo con ícono de calendario
   - Placeholder: "Fecha de salida"
   - Clic abre calendario mensual
   - Validación: Debe ser posterior al check-in

4. **Selector "Habitaciones y huéspedes":**
   - Campo con ícono de personas
   - Placeholder: "1 habitación, 2 adultos"
   - Clic abre dropdown con controles numéricos

5. **Botón Buscar:**
   - Botón verde para ejecutar la búsqueda
   - Deshabilitado si faltan campos obligatorios

**Comportamiento esperado:**

- **Destino:** Clic abre modal con buscador de ciudades/países/hoteles
- **Check-in/Check-out:** Clic abre calendario mensual con navegación
- **Fechas:** Validación automática (check-out después de check-in, no fechas pasadas)
- **Habitaciones/Huéspedes:** Dropdown con controles + / - para ajustar cantidades
- **Validación:** Destino y fechas son obligatorios antes de buscar
- Al hacer clic en "Buscar" → Redirige a módulo de Disponibilidad con resultados filtrados

**Variaciones Móviles:**

- **Campos apilados verticalmente:** Cada campo ocupa ancho completo
- **Modal de destino:** Pantalla completa con buscador
- **Calendario:** Vista en pantalla completa con navegación táctil
- **Dropdown habitaciones:** Expansión fullscreen con controles grandes
- **Botón "Buscar":** Sticky en la parte inferior de la pantalla
- **Touch targets:** Áreas de toque optimizadas

---

### Modal de Búsqueda de Destinos

**Descripción:** Modal emergente que permite buscar y seleccionar destinos mediante campo de búsqueda y lista de resultados.

**Componentes:**

- **Título del Modal:** "¿A dónde quieres ir?"
- **Botón Cerrar (X):** Esquina superior derecha
- **Campo de Búsqueda:**
  - Barra de texto con ícono de lupa
  - Placeholder: "Ciudad, hotel, punto de interés"
- **Lista de Resultados:**
  - Panel scrollable con formato: Nombre | Tipo (Ciudad/Hotel) | País
  - Ejemplo: "San José | Ciudad | Costa Rica"
- **Sugerencias Populares (opcional):**
  - Lista de destinos frecuentes o destacados
  - Aparece cuando el campo está vacío
- **Mensaje de Estado Vacío:**
  - "No se encontraron resultados para tu búsqueda"
  - "Intenta con otro destino"

**Comportamiento esperado:**

- **Apertura:** Clic en campo "Destino" del widget principal
- **Búsqueda:** Usuario escribe destino → Sistema filtra en tiempo real
- **Resultados encontrados:** Muestra lista de destinos coincidentes
- **Selección:** Clic en destino → Cierra modal y actualiza campo "Destino"
- **Sin resultados:** Muestra mensaje de estado vacío
- **Cerrar:** Botón X o clic fuera → Cierra sin cambios

---

### Calendario de Fechas

**Descripción:** Componente de calendario para seleccionar check-in y check-out.

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
  - Check-in seleccionado (verde)
  - Rango seleccionado (verde claro)
  - Check-out seleccionado (verde)
- **Botones de Acción:**
  - "Cancelar" (cierra sin cambios)
  - "Aceptar" (confirma selección) - botón verde

**Comportamiento esperado:**

- **Primer clic:** Establece check-in
- **Segundo clic:** Establece check-out (debe ser posterior al check-in)
- **Validación:** No permite seleccionar fechas pasadas
- **Rango visual:** Muestra días entre check-in y check-out resaltados
- **Cancelar:** Cierra calendario sin aplicar cambios
- **Aceptar:** Actualiza campos y cierra calendario

---

### Dropdown Habitaciones y Huéspedes

**Descripción:** Control desplegable para configurar cantidad de habitaciones, adultos y niños.

**Componentes:**

1. **Habitaciones:**
   - Label: "Habitaciones"
   - Controles: Botón "-" | Número | Botón "+"
   - Rango: Mínimo 1, máximo ⚠️ por definir

2. **Adultos:**
   - Label: "Adultos"
   - Controles: Botón "-" | Número | Botón "+"
   - Rango: Mínimo 1, máximo ⚠️ por definir

3. **Niños:**
   - Label: "Niños"
   - Controles: Botón "-" | Número | Botón "+"
   - Rango: Mínimo 0, máximo ⚠️ por definir
   - ⚠️ **Pendiente:** Validar si pide edades de niños

4. **Botón "Listo":**
   - Botón verde para confirmar configuración

**Comportamiento esperado:**

- **Incremento/Decremento:** Botones +/- ajustan cantidades
- **Límites:** Botones se deshabilitan al alcanzar mínimo/máximo
- **Validación:** Mínimo 1 habitación y 1 adulto siempre
- **Niños:** ⚠️ Pendiente definir si solicita edades y rangos permitidos
- **Resumen:** Al cerrar, campo principal muestra "X habitación(es), Y adulto(s), Z niño(s)"

**Variaciones Móviles:**

- **Pantalla completa:** Dropdown ocupa toda la pantalla
- **Controles más grandes:** Botones +/- con áreas táctiles amplias
- **Botón "Listo":** Sticky en parte inferior

---

## 📋 MÓDULO: DISPONIBILIDAD

**Descripción:** Módulo que muestra los resultados de búsqueda de hoteles disponibles según los criterios del usuario. Incluye widget persistente, filtros laterales y cards de hoteles.

---

### Widget de Búsqueda Persistente

**Descripción:** Resumen compacto de criterios de búsqueda que permanece visible en la parte superior del módulo de disponibilidad.

**Componentes:**

1. **Campo "Destino":**
   - Muestra destino seleccionado (ej: "San José, Costa Rica")
   - Ícono de ubicación
   - Clic abre modal de destinos

2. **Campos de Fechas:**
   - Check-in: Muestra fecha con formato corto (ej: "22 Oct")
   - Check-out: Muestra fecha con formato corto (ej: "25 Oct")
   - Ícono de calendario
   - Clic abre calendario

3. **Campo "Habitaciones y huéspedes":**
   - Muestra resumen (ej: "1 habitación, 2 adultos")
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

**Descripción:** Panel lateral de filtros para refinar búsqueda de hoteles según múltiples criterios.

**Componentes:**

1. **Título de Sección:** "Filtros" (texto destacado)

2. **Filtro: Precio**
   - Rango de precio con slider doble
   - Valores mínimo y máximo mostrados
   - Formato: Puntos o Plata según configuración

3. **Filtro: Estrellas del hotel**
   - Checkboxes: ★ 1, ★★ 2, ★★★ 3, ★★★★ 4, ★★★★★ 5
   - Selección múltiple permitida

4. **Filtro: Tipo de alojamiento**
   - Checkboxes: Hotel, Resort, Apartamento, Hostal, etc.
   - ⚠️ Pendiente confirmar tipos disponibles

5. **Filtro: Servicios/Amenidades**
   - Checkboxes: Wi-Fi, Piscina, Estacionamiento, Desayuno incluido, Gimnasio, etc.
   - ⚠️ Pendiente confirmar servicios disponibles

6. **Filtro: Políticas de cancelación**
   - Checkboxes: Cancelación gratuita, No reembolsable, Prepago
   - ⚠️ Pendiente confirmar opciones disponibles

7. **Botón "Limpiar filtros":**
   - Link o botón para resetear todos los filtros

**Diseño Visual:**

- Panel fijo en lado izquierdo de la pantalla
- Fondo blanco con bordes suaves
- Espaciado vertical entre secciones de filtro
- Checkboxes y sliders con estilo Promerica (verde)

**Comportamiento esperado:**

- **Clic en checkbox:** Activa/desactiva filtro
- **Slider de precio:** Ajuste dinámico de rango
- **Selección múltiple:** Se aplican de forma acumulativa (filtro AND dentro de categoría, OR entre categorías)
- **Actualización en tiempo real:** Resultados se actualizan al aplicar filtros
- **Limpiar filtros:** Vuelve al estado inicial (todos desactivados)
- **Persistencia:** Los filtros se mantienen al navegar detalles de hoteles

**Variaciones Móviles:**

- **Botón flotante "Filtros":** Ícono flotante (🔽) en esquina inferior
- **Panel modal:** Filtros como modal/sheet desde el fondo
- **Filtros apilados verticalmente:** Expansibles por sección
- **Contador de filtros activos:** Badge numérico en botón flotante
- **Botones de acción:** "Limpiar filtros" y "Aplicar" (verde) en parte inferior
- **Cerrar modal:** Swipe hacia abajo o tap en overlay

---

### Cards de Hoteles (Vista Lista)

**Descripción:** Tarjetas individuales que muestran información detallada de cada hotel disponible.

**Componentes (por cada card):**

1. **Imagen del hotel:**
   - Foto principal del hotel en alta resolución
   - Posibilidad de galería (indicador "1/10" si hay múltiples fotos)

2. **Nombre del hotel:**
   - Título destacado (negrita)
   - Ubicación: Ciudad, País (gris, texto más pequeño)

3. **Estrellas:**
   - Visualización de estrellas: ★★★★ (dorado/amarillo)
   - Número de estrellas según categoría del hotel

4. **Servicios destacados (íconos):**
   - 📶 Wi-Fi
   - 🏊 Piscina
   - 🅿️ Estacionamiento
   - 🍳 Desayuno
   - ⚠️ Máximo 4-5 íconos visibles

5. **Calificación de huéspedes:**
   - Puntaje: 8.5/10 (ejemplo)
   - Label: "Muy bueno" | "Excelente" | etc.
   - Número de reseñas: "(124 opiniones)"
   - ⚠️ Pendiente confirmar si está disponible

6. **Precio:**
   - Label: "Desde" (pequeño)
   - Precio por noche en Puntos o Plata
   - Ejemplo: "12,000 puntos/noche" o "USD $150/noche"
   - Precio total de estadía (opcional)

7. **Política de cancelación:**
   - Badge verde: "Cancelación gratuita"
   - Badge rojo: "No reembolsable"
   - Texto pequeño con detalles

8. **Botón de acción:**
   - Botón "Ver más" o "Ver habitaciones" (verde)
   - Clic redirige a detalle del hotel

**Diseño Visual:**

- Card con borde gris claro y sombra suave
- Layout: Imagen izquierda | Información derecha | Precio esquina superior derecha
- Espaciado uniforme entre elementos
- Íconos en color gris/verde con estilo minimalista

**Comportamiento esperado:**

- **Hover en card:** Sombra más pronunciada o borde destacado
- **Clic en imagen:** ⚠️ Pendiente definir: ¿Abre galería de fotos?
- **Clic en card completo:** ⚠️ Pendiente definir: ¿Abre modal de detalle o redirige a página?
- **Clic en botón "Ver más":** Navega a vista de detalle con habitaciones disponibles
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
[PROM] Hoteles - [Noches] - [Proveedor] - [Habitaciones] - [Huéspedes] - [Modelo de pago]
```

**Ejemplos actualizados:**

- `[PROM] Hoteles - 2 noches - HotelBeds - 1 habitación - 2 adultos - Puntos + Plata`
- `[PROM] Hoteles - 3 noches - HotelBeds - 2 habitaciones - 4 adultos 2 niños - Solo Puntos`
- `[PROM] Hoteles - 5 noches - HotelBeds - 1 habitación - 1 adulto - Puntos + Plata (50%)`

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

- ⚠️ **CRÍTICO:** Confirmar si aplica slider en hoteles como en otros productos
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
- ✅ Documentado Módulo Home/Login completo (Widget búsqueda + Modal destinos + Calendario + Dropdown habitaciones)
- ✅ Documentado Módulo Disponibilidad (Widget persistente, Filtros laterales, Cards de hoteles)
- ✅ Agregados Pasos Obligatorios del Flujo E2E (25 pasos)
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
- `[PROM] Hoteles - 3 noches - HotelBeds - 2 habitaciones - 4 adultos - Cancelación gratuita`

---

**Estado:** 🔄 Template - Completar con información específica de Promerica
