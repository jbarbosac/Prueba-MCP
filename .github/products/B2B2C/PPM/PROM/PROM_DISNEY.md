# 🎡 FLUJO E2E OBLIGATORIO PARA DISNEY - PROMERICA REWARDS

> **📖 Información Global:** Ver [PROM_QA_Assistant.agent.md](../../../../agents/PROM_QA_Assistant.agent.md) para URL del portal, país activo, modelo de negocio y versión del marketplace.

---

## 📦 PROVEEDORES DISPONIBLES

⚠️ **PENDIENTE CONFIRMAR PARA PROMERICA**

**Proveedores conocidos en otros modelos:**

- **DerbySoft** (usado en Pichincha Miles)
- **OffLine** (usado en BGR Miles)

⚠️ **Acción requerida:** Validar cuál proveedor utiliza Promerica Rewards

---

## 🔧 COMPONENTES TRANSVERSALES

> **Nota:** Estos componentes son compartidos por todos los productos del marketplace (Vuelos, Autos, Hoteles, **Disney**, Actividades). Ver detalle completo en [PROM_VUELOS.md](PROM_VUELOS.md#-componentes-transversales).

### Header Global

Barra superior con navegación principal, branding personalizado de Promerica y acceso de usuario.

### Tabs de Productos

Pestañas horizontales para navegación entre productos (Vuelos, Autos, Hoteles, **Disney**, Actividades).

### Footer Global

Sección inferior con información institucional y canales de contacto personalizados por país.

---

## 📋 PASOS OBLIGATORIOS DEL FLUJO E2E

**Siempre incluir estos pasos desde login para el flujo completo de Disney:**

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

**Descripción:** Página principal del marketplace donde el usuario accede al selector/buscador de tickets Disney y navega entre productos disponibles. La interfaz es personalizable según el país configurado (Costa Rica en Test).

---

### Widget de Búsqueda/Selección de Disney

**Descripción:** Formulario principal para configurar tickets de Disney con selectores de parques, fechas, tipo de ticket y visitantes.

⚠️ **IMPORTANTE:** La interfaz exacta de Disney puede variar significativamente según el proveedor (DerbySoft vs OffLine). Documentamos estructura genérica hasta confirmar proveedor específico.

**Componentes esperados:**

1. **Selector de Parques:**
   - Formato: ⚠️ Pendiente confirmar (Dropdown, Checkboxes, Cards)
   - Opciones: Magic Kingdom, Epcot, Hollywood Studios, Animal Kingdom
   - Selección: Única o múltiple según tipo de ticket

2. **Selector de Fechas:**
   - Campo con ícono de calendario
   - Placeholder: "Selecciona tus fechas"
   - Comportamiento: Fecha única (1 día) o rango (múltiples días)
   - Clic abre calendario mensual

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
   - Clic abre dropdown con controles por edad

5. **Botón Buscar/Ver Opciones:**
   - Botón verde para ejecutar la búsqueda
   - Deshabilitado si faltan campos obligatorios

**Comportamiento esperado:**

- **Parques:** Selección condicional según tipo de ticket (Base = 1 parque, Hopper = múltiples)
- **Fechas:** Validación de fechas pasadas deshabilitadas, rango lógico
- **Tipo de ticket:** Afecta precio y opciones de parques
- **Visitantes:** Dropdown con controles + / - por rango de edad Disney
- **Validación:** Todos los campos obligatorios antes de buscar
- Al hacer clic en "Buscar" → Redirige a módulo de Disponibilidad/Opciones

**Variaciones Móviles:**

- **Campos apilados verticalmente:** Cada campo ocupa ancho completo
- **Selector de parques:** Vista optimizada según formato
- **Calendario:** Pantalla completa con navegación táctil
- **Dropdown visitantes:** Expansión fullscreen
- **Botón "Buscar":** Sticky en la parte inferior

---

### Calendario de Fechas Disney

**Descripción:** Componente de calendario para seleccionar fechas de visita a los parques Disney.

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
  - Fecha inicio seleccionada (verde)
  - Rango seleccionado (verde claro) si son múltiples días
  - Fecha fin seleccionada (verde)
- **Botones de Acción:**
  - "Cancelar" (cierra sin cambios)
  - "Aceptar" (confirma selección) - botón verde

**Comportamiento esperado:**

- **1 día:** Un solo clic selecciona fecha única
- **Múltiples días:** Primer clic = inicio, segundo clic = fin, rango visual entre fechas
- **Validación:** No permite fechas pasadas
- **Disponibilidad:** ⚠️ Pendiente confirmar si muestra disponibilidad/precios por fecha
- **Cancelar:** Cierra calendario sin cambios
- **Aceptar:** Actualiza campo y cierra calendario

---

### Dropdown Visitantes Disney

**Descripción:** Control desplegable para configurar cantidad de visitantes por rango de edad Disney.

**Componentes:**

1. **Adultos:**
   - Label: "Adultos" (edad: ⚠️ Pendiente confirmar rango, típicamente 10+ o 12+)
   - Controles: Botón "-" | Número | Botón "+"
   - Rango: Mínimo 1, máximo ⚠️ por definir

2. **Niños:**
   - Label: "Niños" (edad: ⚠️ Pendiente confirmar rango, típicamente 3-9)
   - Controles: Botón "-" | Número | Botón "+"
   - Rango: Mínimo 0, máximo ⚠️ por definir
   - ⚠️ **Pendiente:** Validar si requiere edad específica de cada niño

3. **Infantes (si aplica):**
   - Label: "Infantes" (edad: ⚠️ Pendiente confirmar, típicamente 0-2, gratis)
   - Controles: Botón "-" | Número | Botón "+"
   - Rango: Mínimo 0, máximo ⚠️ por definir

4. **Botón "Listo":**
   - Botón verde para confirmar configuración

**Comportamiento esperado:**

- **Incremento/Decremento:** Botones +/- ajustan cantidades
- **Límites:** Botones se deshabilitan al alcanzar mínimo/máximo
- **Validación:** Mínimo 1 visitante (típicamente al menos 1 adulto)
- **Edades específicas:** ⚠️ Pendiente definir si solicita edad exacta de niños para validación Disney
- **Resumen:** Al cerrar, campo principal muestra "X adulto(s), Y niño(s)"

**Variaciones Móviles:**

- **Pantalla completa:** Dropdown ocupa toda la pantalla
- **Controles más grandes:** Botones +/- con áreas táctiles amplias
- **Botón "Listo":** Sticky en parte inferior

---

## 📋 MÓDULO: DISPONIBILIDAD/OPCIONES

**Descripción:** Módulo que muestra las opciones de tickets Disney disponibles según los criterios del usuario. La estructura exacta depende del proveedor (DerbySoft vs OffLine).

⚠️ **PENDIENTE DOCUMENTAR:** Este módulo requiere validación del proveedor específico de Promerica para documentar correctamente:

- Layout de opciones de tickets
- Presentación de precios por día/total
- Información de cada tipo de ticket
- Slider Puntos + Plata (ubicación)
- Filtros disponibles (si aplica)

**Componentes esperados:**

### Widget de Búsqueda Persistente (esperado)

**Descripción:** Resumen compacto de criterios que permite modificar la búsqueda.

**Componentes:**

1. **Parques seleccionados**
2. **Fechas de visita**
3. **Tipo de ticket**
4. **Visitantes**
5. **Botón "Buscar"**

### Cards/Lista de Opciones de Tickets (esperado)

**Descripción:** Visualización de diferentes opciones de tickets disponibles.

**Componentes esperados por cada opción:**

1. **Nombre del ticket:**
   - Ejemplo: "Magic Kingdom - 1 Día - Base"
   - Ejemplo: "Multi Parque - 3 Días - Hopper"

2. **Parques incluidos:**
   - Íconos o lista de parques según tipo

3. **Duración:**
   - Número de días válido
   - Fecha inicio y fin

4. **Tipo:**
   - Badge: Base | Hopper | Hopper Plus

5. **Precio:**
   - Precio por persona o total
   - Formato: Puntos o Plata
   - ⚠️ Pendiente confirmar: ¿Por persona o total grupo?

6. **Información adicional:**
   - Qué incluye
   - Restricciones
   - Validez del ticket

7. **Botón de acción:**
   - "Seleccionar" o "Ver más" (verde)

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
[PROM] Disney - [Parques] - [Días] - [Tipo ticket] - [Visitantes] - [Modelo de pago]
```

**Ejemplos actualizados:**

- `[PROM] Disney - Magic Kingdom - 1 día - Base - 2 adultos - Puntos + Plata`
- `[PROM] Disney - Multi parque - 3 días - Hopper - 2 adultos 2 niños - Solo Puntos`
- `[PROM] Disney - 4 parques - 5 días - Hopper Plus - 4 adultos - Puntos + Plata (60%)`

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

- ⚠️ **CRÍTICO:** Confirmar si aplica slider en Disney como en otros productos
- Porcentaje mínimo de puntos requerido
- Fórmula de cálculo Puntos ↔ Plata (por persona o total grupo)
- Ubicación del slider (disponibilidad, detalle, checkout)

**Políticas de Disney:**

- Rangos de edad por categoría (adultos, niños, infantes)
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

- [SHARED_QA_RULES.md](../../../../shared/SHARED_QA_RULES.md) - Fundamentos ISTQB y Azure DevOps
- [PROM_COMMON_RULES.md](../../../../shared/Reglas Marketplace/PROM_COMMON_RULES.md) - Reglas comunes Promerica
- [PROM_VUELOS.md](PROM_VUELOS.md) - Referencia para estructura y componentes transversales

---

## 🔄 CONTROL DE CAMBIOS

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
