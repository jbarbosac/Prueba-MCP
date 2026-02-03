# 🎡 PRODUCTO: DISNEY - PROMERICA REWARDS

> **📖 Información Global:** Ver [PROM_QA_Assistant.agent.md](../../../../agents/PROM_QA_Assistant.agent.md) para URL del portal, país activo, modelo de negocio y versión del marketplace.
>
> **📌 Versión:** v1.1 (03-02-2026)  
> **📝 Última Actualización:** Actualización completa según Knowledge_Base_Promerica.md - Disney V2

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

Página principal del marketplace donde el usuario accede al widget de búsqueda de paquetes Disney y navega entre productos disponibles. La interfaz es personalizable según el país configurado (Costa Rica en Test). Este módulo proporciona búsqueda simplificada con selección de fechas y cantidad de visitantes.

### 🎨 FUNCIONALIDADES

#### 🔹 Funcionalidad: Widget de Búsqueda de Disney

##### 📖 Descripción Funcional

Formulario simplificado para búsqueda de paquetes y entradas a parques Disney con selección de fechas y cantidad de visitantes. A diferencia de otros productos, Disney no requiere selección inicial de parques o tipo de ticket en el buscador inicial.

**Ubicación:** Centro de la página de inicio, debajo del header y tabs de productos  
**Tipo de componente:** Formulario interactivo simplificado  
**Acceso:** Disponible para todos los usuarios autenticados

##### 🧩 Componentes

| Componente                        | Descripción                          | Tipo               | Funcionalidad/Editable                                                                                                                                                                              |
| --------------------------------- | ------------------------------------ | ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Campo "Selecciona tus fechas"** | Selector de fechas de visita         | Date picker        | - Label: "Selecciona tus fechas"<br>- Placeholder: "Selecciona tus fechas"<br>- Ícono calendario verde a la derecha<br>- Formato después selección: "Vie, 31 Oct - Vie, 7 Nov"<br>- Editable        |
| **Dropdown "Pasajeros"**          | Configuración de visitantes por edad | Dropdown + Modal   | - Label: "Pasajeros"<br>- Valor por defecto: "1 adulto"<br>- Ícono chevron-down<br>- Abre modal con contadores Adultos/Niños<br>- Editable                                                          |
| **Texto informativo**             | Política entrada gratuita menores    | Text informativo   | - Mensaje: "Entrada gratuita para menores de 3 años (al momento de entrar al parque)."<br>- No editable                                                                                             |
| **Botón "Buscar"**                | Ejecuta búsqueda de paquetes         | Button (CTA verde) | - Color: Verde institucional (#00563F)<br>- Texto: "Buscar" blanco centrado<br>- Ancho completo (full-width)<br>- Bordes redondeados<br>- Efecto hover opacidad<br>- Deshabilitado si faltan campos |

##### 💻 Comportamiento Esperado

**Interacción con campo "Selecciona tus fechas" (Datepicker):**

- Clic en campo abre calendario interactivo Disney
- **Componentes del calendario:**
  - **Navegación mensual:** Flechas simples < > con visualización mes/año (ej: "ENE 2024")
  - **Navegación rápida:** Flechas dobles << >> para saltar múltiples meses
  - **Vista desktop:** Calendario dual (dos meses lado a lado)
  - **Formato grid:** Días de semana L, M, M, J, V, S, D, días del mes clickeables
  - **Indicadores visuales:**
    - Fechas seleccionadas (inicio y fin) resaltadas en verde (#00563F)
    - Rango entre fechas con conexión gráfica verde claro
    - Fechas pasadas deshabilitadas (no clickeables)
  - **Botones del modal:**
    - "Cancelar": Cierra sin guardar cambios
    - "Aceptar": Confirma selección y cierra datepicker
- **Validaciones:**
  - No permite seleccionar fechas pasadas
  - Fecha de inicio debe ser anterior a fecha de fin
- Después de selección, campo muestra formato: "Vie, 31 Oct - Vie, 7 Nov"

**Interacción con dropdown "Pasajeros" (Modal de configuración):**

- Clic en campo abre modal con fondo blanco
- Muestra selector dropdown superior: "1 adulto" para vista rápida
- **Controles de pasajeros:**
  - **Sección Adultos:**
    - Label: "Adultos"
    - Contador numérico con botones - / +
    - Valor editable en el centro
    - Texto informativo: "Mayores de 10 años"
    - Validación: Mínimo 1 adulto
  - **Sección Niños:**
    - Label: "Niños"
    - Contador numérico con botones - / +
    - Valor editable en el centro
    - Texto informativo: "De 3 a 9 años"
    - Rango: 0 a múltiples niños
  - **Botones de acción del modal:**
    - "Cancelar": Descarta cambios y cierra modal sin aplicar
    - "Aceptar": Guarda configuración, actualiza texto del dropdown y cierra modal
  - **Actualización dinámica:** Texto del dropdown cambia según configuración (ej: "2 adultos", "1 adulto y 1 niño")

**Validaciones del sistema:**

- Fechas son obligatorias (inicio y fin)
- Fecha de inicio debe ser anterior a fecha de fin
- Mínimo 1 adulto requerido
- Botón "Buscar" se habilita solo cuando todos los campos requeridos estén completos
- Al presionar "Buscar" se redirige al módulo de Disponibilidad con parámetros de búsqueda
- Entrada gratuita para menores de 3 años (no se cuentan en pasajeros)

**Variaciones Móviles:**

- **Layout vertical:** Los campos se apilan verticalmente para optimizar espacio en pantalla móvil
- **Campo "Fechas":** Al hacer clic abre datepicker de pantalla completa con calendario único (no dual). Teclado numérico virtual disponible en la parte inferior
- **Selector de pasajeros:** Abre modal de pantalla completa con contadores +/- más grandes para facilitar interacción táctil
- **Botones del modal:** "Aceptar" y "Cancelar" ocupan mayor tamaño y están espaciados para facilitar toque en móvil
- **Botón "Buscar":** Permanece fijo (sticky) en la parte inferior de la pantalla móvil, siempre visible al hacer scroll

##### ✅ VALIDACIONES DE QA

Estas validaciones deben incluirse en todos los casos de prueba que involucren el Widget de Búsqueda:

- [ ] **VAL-DIS-HOME-001:** Fechas son obligatorias
  - **Verificar:** Botón "Buscar" deshabilitado si no se seleccionan fechas
- [ ] **VAL-DIS-HOME-002:** Mínimo 1 adulto requerido
  - **Verificar:** Dropdown "Pasajeros" valida mínimo 1 adulto
- [ ] **VAL-DIS-HOME-003:** Datepicker no permite fechas pasadas
  - **Verificar:** Fechas anteriores a hoy están deshabilitadas y no seleccionables
- [ ] **VAL-DIS-HOME-004:** Rango de fechas lógico
  - **Verificar:** Fecha fin debe ser posterior a fecha inicio, rango visual verde claro entre fechas
- [ ] **VAL-DIS-HOME-005:** Navegación del datepicker funcional
  - **Verificar:** Flechas simples < > cambian mes, flechas dobles << >> saltan múltiples meses
- [ ] **VAL-DIS-HOME-006:** Modal de pasajeros funciona correctamente
  - **Verificar:** Botones +/- ajustan cantidades, "Cancelar" descarta cambios, "Aceptar" guarda y cierra
- [ ] **VAL-DIS-HOME-007:** Actualización dinámica de pasajeros
  - **Verificar:** Campo muestra "2 adultos", "1 adulto y 1 niño" según configuración
- [ ] **VAL-DIS-HOME-008:** Texto informativo visible
  - **Verificar:** Mensaje "Entrada gratuita para menores de 3 años" visible debajo de campos
- [ ] **VAL-DIS-HOME-009:** Botón "Buscar" redirige correctamente
  - **Verificar:** Clic en "Buscar" redirige a módulo Disponibilidad con parámetros de búsqueda
- [ ] **VAL-DIS-HOME-010:** Variaciones móviles
  - **Verificar:** Layout vertical, datepicker pantalla completa calendario único, modal pasajeros fullscreen, botón "Buscar" sticky

##### 🧪 Escenarios de Prueba

**Escenario 1: Búsqueda exitosa de paquetes Disney - 1 adulto**

- **Precondición:** Usuario autenticado en home Disney
- **Pasos:**
  1. Clic en campo "Selecciona tus fechas"
  2. Seleccionar rango: Vie, 31 Oct - Vie, 7 Nov
  3. Clic en "Aceptar"
  4. Verificar campo muestra "Vie, 31 Oct - Vie, 7 Nov"
  5. Dejar dropdown "Pasajeros" en valor por defecto "1 adulto"
  6. Clic en "Buscar"
- **Resultado esperado:** Redirige a Disponibilidad con paquetes para rango de fechas seleccionado, 1 adulto

**Escenario 2: Búsqueda con múltiples pasajeros - 2 adultos 2 niños**

- **Precondición:** Usuario autenticado en home Disney
- **Pasos:**
  1. Seleccionar rango de fechas en datepicker
  2. Clic en dropdown "Pasajeros"
  3. Ajustar Adultos a 2 con botón +
  4. Ajustar Niños a 2 con botón +
  5. Verificar texto informativo "Mayores de 10 años" y "De 3 a 9 años"
  6. Clic en "Aceptar"
  7. Verificar campo muestra "2 adultos y 2 niños"
  8. Clic en "Buscar"
- **Resultado esperado:** Redirige a Disponibilidad con paquetes para 2 adultos y 2 niños

**Escenario 3: Validación de fechas pasadas**

- **Precondición:** Usuario en home Disney
- **Pasos:**
  1. Abrir datepicker
  2. Intentar seleccionar fecha anterior a hoy
- **Resultado esperado:** Fechas pasadas no seleccionables, botón deshabilitado

**Escenario 4: Cancelar selección en modal de pasajeros**

- **Precondición:** Usuario en home Disney con "1 adulto" seleccionado
- **Pasos:**
  1. Clic en dropdown "Pasajeros"
  2. Cambiar a 3 adultos + 1 niño
  3. Clic en "Cancelar"
- **Resultado esperado:** Modal se cierra, campo mantiene "1 adulto" (cambios descartados)

**Escenario 5: Navegación rápida en datepicker**

- **Precondición:** Usuario en home Disney
- **Pasos:**
  1. Abrir datepicker (muestra mes actual)
  2. Clic en flechas dobles >> varias veces
  3. Verificar salto de múltiples meses
  4. Usar flechas simples < > para ajustar mes específico
  5. Seleccionar rango de fechas
  6. Clic en "Aceptar"
- **Resultado esperado:** Navegación rápida funcional, rango seleccionado correctamente

---

## 📋 MÓDULO: DISPONIBILIDAD

### 📋 Descripción del Módulo

Módulo que muestra los resultados de búsqueda de paquetes Disney disponibles según los criterios del usuario (fechas y pasajeros). Presenta opciones de paquetes de 1 a 10 días con información detallada de precios, fechas de validez y permite seleccionar tipo de entrada específico según parques deseados.

> 🔗 **Referencia HU:** [#116797](https://dev.azure.com/ultragrouplaorg/_workitems/edit/116797) - Ajustar componentes de disponibilidad de disney de acuerdo a Look & Feel Promerica - Web  
> 🎨 **Diseño Figma:** [050-004-PRO-WEB-CLUB-PRO](https://www.figma.com/design/wpVJRncGYMTrt2hCysWOkf/050-004-PRO-WEB-CLUB-PRO?node-id=4189-17191&p=f&t=qJ170CFMcYKSFOeX-0)  
> 📅 **Versión:** V2 - Look & Feel Promerica (Febrero 2026)

---

> ⚠️ **IMPORTANTE - PRECIOS DINÁMICOS:**  
> Todos los precios mostrados en este documento son **EJEMPLOS ILUSTRATIVOS** y no representan tarifas fijas.  
> Los precios reales son calculados dinámicamente y varían según:
>
> - **Configuración de agencia:** Cada agencia define sus tarifas base
> - **Número de pasajeros:** Precio base × cantidad de adultos y niños
> - **Cantidad de días:** Más días = **menor costo por día** (economía de escala)
>   - Ejemplo: 1 día = $200/día → 10 días = $500 total ($50/día)
> - **Tipo de entrada/parque:** Animal Kingdom, EPCOT, Hollywood, Magic Kingdom, Park Hopper
> - **Temporada y disponibilidad:** Precios pueden variar según demanda e inventario en tiempo real
> - **Códigos promocionales:** Descuentos aplicables según configuración
>
> **Formato de precios en documentación:** USD $XXX (valor de referencia, no definitivo)

---

### 🎯 Flujo de Interacción General

**Estado inicial del módulo:**

- **Buscador:** Aparece **cerrado** (colapsado) mostrando resumen compacto de búsqueda
- **Listado de paquetes:** Visible con opciones de 1 a 10 días disponibles
- **Avatares de pasajeros:** Representación visual de pasajeros seleccionados
- **Texto informativo:** Banner recordatorio sobre entrada gratuita menores de 3 años

**Secuencia típica de navegación del usuario:**

1. Usuario llega de HOME con búsqueda ejecutada
2. Revisa listado de paquetes (1-10 días) con precios "Desde" (Animal Kingdom base)
3. Si desea modificar búsqueda: Clic en "Modificar búsqueda" → Widget se expande
4. Selecciona paquete deseado (ej: "3 Días") → Clic en "Seleccionar"
5. Se abre modal "Mejora tu tipo de entrada" con 5 opciones de parques
6. Selecciona tipo de entrada (Animal Kingdom, EPCOT, Hollywood, Magic Kingdom, Park Hopper)
7. Clic en "Seleccionar" de la opción elegida
8. Modal se cierra y redirige a módulo Checkout

---

### 🎨 FUNCIONALIDADES

#### 🔹 Funcionalidad: Widget de Búsqueda V2 (Cerrado/Desplegable)

##### 📖 Descripción Funcional

Componente de búsqueda mejorado que permite modificar los criterios de búsqueda con dos estados visuales: cerrado (compacto) y desplegable (expandido). Requiere configuración específica de agencia para activar la Versión 2 de componentes Disney.

**Ubicación:** Parte superior del módulo Disponibilidad, debajo del header  
**Tipo:** Widget colapsable/expandible con dos estados  
**Acceso:** Visible en todo momento durante navegación de paquetes

**🔧 Configuración:**

- **Requisito:** Agencia debe tener activa la **Versión 2 de componentes** de Disney
- **Estado por defecto:** Buscador aparece **cerrado** (colapsado)
- **Activación:** Se despliega al hacer clic en el botón "Modificar búsqueda"

##### 🧩 Componentes

**Componentes - Estado Cerrado:**

| Componente                     | Descripción                                | Tipo           | Funcionalidad/Editable                                                                                                                                   |
| ------------------------------ | ------------------------------------------ | -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Resumen de Búsqueda**        | Muestra parámetros seleccionados compactos | Text display   | - Formato: "1 adulto \| Jue, 23 oct 2025"<br>- Separadores visuales (pipe \|)<br>- No editable directamente                                              |
| **Botón "Modificar búsqueda"** | Despliega el widget completo               | Button (verde) | - Texto: "Modificar búsqueda"<br>- Color: Verde institucional (#00563F)<br>- Posicionamiento: Alineado a la derecha<br>- Ícono: Lápiz/edición (opcional) |

**Componentes - Estado Desplegable:**

| Componente                        | Descripción                       | Tipo               | Funcionalidad/Editable                                                                                                                                                                |
| --------------------------------- | --------------------------------- | ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Campo "Selecciona tus fechas"** | Selector de fechas de visita      | Date picker        | - Label: "Selecciona tus fechas"<br>- Placeholder: "Selecciona tus fechas"<br>- Ícono: Calendario verde a la derecha<br>- Formato después selección: "Jue, 23 oct 2025"<br>- Editable |
| **Dropdown "Pasajeros"**          | Configuración de adultos y niños  | Dropdown + Modal   | - Label: "Pasajeros"<br>- Valor por defecto: "1 adulto"<br>- Ícono: Chevron-down<br>- Abre modal con contadores +/-<br>- Editable                                                     |
| **Campo "Código promocional"**    | Código de descuento opcional      | Text input         | - Label: "Código promocional"<br>- Placeholder: "Ingresa tu código promocional"<br>- Campo texto libre<br>- Ícono: Tag/etiqueta (opcional)<br>- Editable                              |
| **Botón "Buscar"**                | Ejecuta nueva búsqueda            | Button (CTA verde) | - Texto: "Buscar"<br>- Color: Verde institucional (#00563F)<br>- Texto blanco centrado<br>- Ancho completo (full-width)<br>- Bordes redondeados                                       |
| **Texto informativo**             | Política entrada gratuita menores | Text informativo   | - Mensaje: "Entrada gratuita para menores de 3 años (al momento de entrar al parque)."<br>- Estilo: Texto pequeño, color gris<br>- Posicionamiento: Debajo de controles               |

##### 💻 Comportamiento Esperado

**Estado inicial:**

- Buscador cerrado muestra resumen compacto de búsqueda ejecutada desde HOME
- Botón "Modificar búsqueda" visible alineado a la derecha
- Listado de paquetes visible debajo del buscador cerrado

**Clic en "Modificar búsqueda":**

- Widget se expande con animación suave
- Muestra todos los campos editables (fechas, pasajeros, código promocional)
- Datepicker con comportamiento idéntico al HOME:
  - Navegación mensual con flechas < >
  - Visualización: Mes/Año (ej: "OCT 2025")
  - Grid semanal: L, M, M, J, V, S, D
  - Fecha seleccionada resaltada en verde (#00563F)
  - Restricción: No permite fechas pasadas
  - Botones "Cancelar" y "Aceptar"
- Modal de pasajeros con comportamiento idéntico al HOME:
  - Sección Adultos: "Mayores de 10 años" con contador +/-
  - Sección Niños: "De 3 a 9 años" con contador +/-
  - Validación: Mínimo 1 adulto
  - Actualización dinámica del texto (ej: "2 adultos", "1 adulto y 1 niño")
  - Botones "Cancelar" y "Aceptar"

**Edición de campos:**

- Usuario modifica fecha, pasajeros o ingresa código promocional
- Validación: Mínimo 1 adulto y fecha obligatoria
- Botón "Buscar" se habilita solo con criterios válidos

**Clic en "Buscar":**

- Actualiza resultados sin recargar página completa
- Muestra spinner/skeleton durante carga
- Actualiza listado de paquetes con nuevos criterios
- Widget puede volver a estado cerrado automáticamente (opcional según diseño)

**Clic en "Cancelar" (si existe):**

- Colapsa el widget sin aplicar cambios
- Mantiene criterios de búsqueda originales

**Diseño Visual:**

- Fondo blanco con bordes sutiles
- Separadores entre secciones
- Paleta de colores verde Promerica
- Tipografía corporativa consistente
- Espaciado uniforme entre elementos

**Variaciones Móviles:**

- **Botón "Regresar al home":** Aparece en la parte superior izquierda para navegación rápida (específico de mobile)
- **Buscador colapsado:** Ocupa menos altura, muestra resumen compacto en una línea
- **Botón "Modificar búsqueda":** Centrado horizontalmente, tamaño mayor para facilitar toque táctil
- **Estado expandido:** Ocupa pantalla completa con overlay oscuro
- **Botón "Ocultar búsqueda":** Aparece cuando el widget está expandido, permite colapsar sin aplicar cambios
- **Campos de entrada:** Se apilan verticalmente con mayor espaciado entre elementos
- **Datepicker:** Modal de pantalla completa con calendario de un solo mes (no dual)
- **Modal de pasajeros:** Pantalla completa con contadores +/- de mayor tamaño
- **Botón "Buscar":** Sticky en parte inferior, siempre visible, ocupa ancho completo
- **Campo "Código promocional":** Ancho completo con teclado optimizado para códigos alfanuméricos
- **Texto informativo:** Se mantiene visible debajo del formulario con tipografía reducida

##### ✅ VALIDACIONES DE QA

- [ ] **VAL-DIS-DISP-001:** Widget V2 requiere configuración de agencia
  - **Verificar:** Versión 2 de componentes Disney debe estar activa en configuración
- [ ] **VAL-DIS-DISP-002:** Estado inicial cerrado (colapsado)
  - **Verificar:** Buscador aparece cerrado mostrando resumen compacto con separadores pipe |
- [ ] **VAL-DIS-DISP-003:** Botón "Modificar búsqueda" funcional
  - **Verificar:** Clic despliega widget completo con animación suave
- [ ] **VAL-DIS-DISP-004:** Datepicker funciona correctamente en estado desplegable
  - **Verificar:** Navegación mensual, grid semanal, restricción fechas pasadas, botones Cancelar/Aceptar
- [ ] **VAL-DIS-DISP-005:** Modal de pasajeros funciona correctamente
  - **Verificar:** Contadores +/- Adultos/Niños, validación mínimo 1 adulto, actualización dinámica texto
- [ ] **VAL-DIS-DISP-006:** Campo código promocional opcional
  - **Verificar:** Campo texto libre, placeholder visible, no obligatorio para búsqueda
- [ ] **VAL-DIS-DISP-007:** Botón "Buscar" actualiza resultados
  - **Verificar:** Clic ejecuta nueva búsqueda, muestra spinner, actualiza listado de paquetes sin recargar página
- [ ] **VAL-DIS-DISP-008:** Texto informativo visible
  - **Verificar:** Mensaje "Entrada gratuita para menores de 3 años" visible debajo de controles
- [ ] **VAL-DIS-DISP-009:** Variaciones móviles - Botón "Regresar al home"
  - **Verificar:** Botón específico mobile en parte superior izquierda, navegación rápida funcional
- [ ] **VAL-DIS-DISP-010:** Variaciones móviles - Estado expandido pantalla completa
  - **Verificar:** Widget expandido ocupa pantalla completa con overlay oscuro, botón "Ocultar búsqueda" visible
- [ ] **VAL-DIS-DISP-011:** Variaciones móviles - Botón "Buscar" sticky
  - **Verificar:** Botón sticky en parte inferior móvil, siempre visible, ancho completo

##### 🧪 Escenarios de Prueba

**Escenario 1: Expandir widget cerrado y modificar fechas**

- **Precondición:** Usuario en Disponibilidad, widget V2 en estado cerrado mostrando "1 adulto | Jue, 23 oct 2025"
- **Pasos:**
  1. Clic en botón "Modificar búsqueda"
  2. Verificar widget se expande con animación suave
  3. Clic en campo "Selecciona tus fechas"
  4. Seleccionar nuevo rango: Vie, 30 oct - Lun, 2 nov
  5. Clic en "Aceptar"
  6. Verificar campo actualizado
  7. Clic en botón "Buscar"
- **Resultado esperado:** Nueva búsqueda ejecutada, spinner visible, listado de paquetes actualizado con nuevas fechas

**Escenario 2: Modificar pasajeros y agregar código promocional**

- **Precondición:** Usuario en Disponibilidad, widget V2 expandido
- **Pasos:**
  1. Clic en dropdown "Pasajeros"
  2. Ajustar a 2 adultos + 1 niño
  3. Clic en "Aceptar"
  4. Verificar campo muestra "2 adultos y 1 niño"
  5. Clic en campo "Código promocional"
  6. Ingresar código "DISNEY2026"
  7. Clic en "Buscar"
- **Resultado esperado:** Búsqueda con 2 adultos + 1 niño + código promocional, paquetes actualizados con descuento si aplica

**Escenario 3: Cancelar modificación en estado expandido**

- **Precondición:** Usuario en Disponibilidad, widget V2 expandido
- **Pasos:**
  1. Modificar fechas a nuevo rango
  2. Modificar pasajeros a 3 adultos
  3. Clic en botón "Cancelar" o "Ocultar búsqueda" (móvil)
- **Resultado esperado:** Widget colapsa sin aplicar cambios, resumen mantiene valores originales

**Escenario 4: Variaciones móviles - Botón "Regresar al home"**

- **Precondición:** Usuario en Disponibilidad en dispositivo móvil
- **Pasos:**
  1. Verificar botón "Regresar al home" visible en parte superior izquierda
  2. Clic en botón
- **Resultado esperado:** Navegación rápida a HOME sin perder contexto

**Escenario 5: Variaciones móviles - Estado expandido pantalla completa**

- **Precondición:** Usuario en Disponibilidad en dispositivo móvil, widget cerrado
- **Pasos:**
  1. Clic en "Modificar búsqueda"
  2. Verificar widget ocupa pantalla completa con overlay oscuro
  3. Verificar datepicker modal pantalla completa (calendario único)
  4. Verificar modal pasajeros pantalla completa (contadores +/- grandes)
  5. Verificar botón "Buscar" sticky en parte inferior
  6. Clic en "Ocultar búsqueda"
- **Resultado esperado:** Widget colapsa, overlay desaparece, resumen compacto visible

---

#### 🔹 Funcionalidad: Card de Paquetes Disney

##### 📖 Descripción Funcional

Tarjeta visual que presenta información detallada de cada paquete de entrada a Disney con diseño adaptado al Look & Feel de Promerica. Cada card representa un paquete específico con duración, fechas de validez, precios por pasajero y precio total "Desde" el parque más económico.

**Ubicación:** Área principal del módulo Disponibilidad, debajo del widget V2  
**Tipo:** Card individual dentro de grid responsivo  
**Acceso:** Visible tras ejecutar búsqueda desde HOME o modificar criterios en widget

**🔧 Configuración:**

- **Requisito:** Agencia debe tener activa la **V2 de card de Disney**
- **Visualización:** Grid de cards responsivo (columnas automáticas según viewport)

##### 🧩 Componentes de la Card

**1. Encabezado de Paquete:**

| Componente             | Descripción      | Tipo         | Funcionalidad                                                                                                                                                     |
| ---------------------- | ---------------- | ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Título del paquete** | Cantidad de días | Text/Heading | - Formato: "X Día" / "X Días"<br>- Ejemplos: "1 Día", "2 Días", "3 Días"<br>- Tipografía: Bold, tamaño grande<br>- Color: Verde oscuro Promerica<br>- No editable |

**2. Información de Fechas:**

| Componente               | Descripción                      | Tipo        | Funcionalidad                                                                                                                                                                                        |
| ------------------------ | -------------------------------- | ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Fecha de ingreso**     | Primera fecha válida del paquete | Date + Icon | - Ícono: Calendario verde<br>- Label: "Fecha de ingreso:"<br>- Valor: "día, dd de mes de aaaa"<br>- Ejemplo: "mié, 23 oct 2025"<br>- Estilo: Texto con ícono alineado izquierda<br>- No editable     |
| **Entrada válida hasta** | Última fecha válida del paquete  | Date + Icon | - Ícono: Calendario verde<br>- Label: "Entrada válida hasta:"<br>- Valor: "día, dd de mes de aaaa"<br>- Ejemplo: "dom, 26 oct 2025"<br>- Estilo: Texto con ícono alineado izquierda<br>- No editable |

**3. Sección de Precios:**

> ⚠️ **Nota:** Los precios mostrados son ejemplos. Los valores reales son calculados dinámicamente según configuración de agencia.

| Componente                  | Descripción                        | Tipo             | Funcionalidad                                                                                                                                                                                                                                                                                                                      |
| --------------------------- | ---------------------------------- | ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Label "Precio por pax:"** | Identificador de precio individual | Text label       | - Texto descriptivo<br>- Permite identificar precio individual<br>- No editable                                                                                                                                                                                                                                                    |
| **Precio Adulto**           | Tarifa por adulto                  | Price text       | - Formato: "USD $XXX / Adulto"<br>- Ejemplo: "USD $189 / Adulto"<br>- Tamaño: Texto mediano<br>- Color: Negro o gris oscuro<br>- Cálculo: Tarifa base agencia<br>- No editable                                                                                                                                                     |
| **Precio Niño**             | Tarifa por niño                    | Price text       | - Formato: "USD $XXX / Niño"<br>- Ejemplo: "USD $189 / Niño"<br>- Tamaño: Texto mediano<br>- Color: Negro o gris oscuro<br>- Cálculo: Tarifa base (puede tener descuento vs adulto)<br>- No editable                                                                                                                               |
| **Precio Total (Desde)**    | Precio base parque más económico   | Price highlight  | - Label: "Desde"<br>- Formato: "USD $XXX"<br>- Ejemplo: "USD $200" (Animal Kingdom base)<br>- Tamaño: Texto grande, bold<br>- Color: Verde institucional (#00563F)<br>- Posicionamiento: Destacado visualmente<br>- Cálculo: Precio base Animal Kingdom × pasajeros<br>- Nota: Varía según tipo entrada posterior<br>- No editable |
| **Texto precio por día**    | Información adicional              | Text informativo | - Mensaje: "Precio por persona por día"<br>- Estilo: Texto pequeño, color gris<br>- Posicionamiento: Debajo del precio total<br>- No editable                                                                                                                                                                                      |

**4. Botón de Acción:**

| Componente              | Descripción                | Tipo               | Funcionalidad                                                                                                                                                                                                                                                                                                                                                     |
| ----------------------- | -------------------------- | ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Botón "Seleccionar"** | Acción para elegir paquete | Button (CTA verde) | - Texto: "Seleccionar"<br>- Color de fondo: Verde institucional (#00563F)<br>- Texto: Blanco, centrado, bold<br>- Ancho: Full-width dentro de la card<br>- Bordes: Redondeados<br>- Efecto hover: Oscurecimiento o cambio opacidad<br>- Estado deshabilitado: Gris con cursor not-allowed si sin disponibilidad<br>- Clic: Abre modal "Mejora tu tipo de entrada" |
| ------------            | -------------              | ------             | ------------------------                                                                                                                                                                                                                                                                                                                                          |

##### 💻 Comportamiento Esperado

**Diseño Visual:**

- **Fondo:** Blanco
- **Borde:** Sutil, gris claro (1px)
- **Sombra:** Box-shadow suave para efecto de elevación
- **Espaciado interno:** Padding uniforme (16-24px)
- **Separadores:** Líneas horizontales sutiles entre secciones (opcional)
- **Altura:** Uniforme entre todas las cards del grid
- **Hover effect:** Sombra más pronunciada o borde verde al pasar el cursor

**Comportamiento esperado:**

- **Renderizado:** Cards se organizan en grid responsivo
- **Desktop:** 2-4 columnas según ancho de pantalla
- **Tablet:** 2 columnas
- **Móvil:** 1 columna (stack vertical)
- **Clic en "Seleccionar":** Abre modal "Mejora tu tipo de entrada" con opciones de parques disponibles
- **Cálculo de precio total:** Se actualiza según número de adultos y niños seleccionados en búsqueda
- **Disponibilidad:** Cards sin disponibilidad pueden mostrarse con opacidad reducida y botón deshabilitado
- **Flujo completo:** Selección de paquete → Modal de parques → Selección de parque → Checkout

**Precio "Desde" - Lógica:**

- **Precio base:** Muestra el precio del parque más económico (Animal Kingdom)
- **El precio varía según el tipo de entrada/parque seleccionado posteriormente:**
  - Animal Kingdom: Base (ejemplo: $200)
  - EPCOT: Base + incremento (ejemplo: $240)
  - Hollywood Studios: Base + incremento (ejemplo: $289)
  - Magic Kingdom: Base + incremento (ejemplo: $320)
  - Park Hopper: Precio premium (ejemplo: $400)

**Lógica de economía de escala:**

- **Más días = Menor costo por día**
- Ejemplo ilustrativo:
  - 1 día: $200 total → $200/día
  - 5 días: $320 total → $64/día (economía del 68%)
  - 10 días: $500 total → $50/día (economía del 75%)

**Datos dinámicos:**

- Fechas ajustadas según selección del usuario
- Precios calculados según configuración de agencia
- Disponibilidad en tiempo real (puede variar según inventario)

**Variaciones Móviles:**

- **Layout:** Cards apiladas verticalmente (single column), scroll vertical fluido
- **Ancho:** Cards ocupan 100% del ancho de pantalla con padding lateral uniforme
- **Información condensada:** Fechas y precios con tipografía ligeramente reducida pero legible
- **Botón "Seleccionar":** Área táctil ampliada (min 44x44px), ancho completo dentro de la card
- **Espaciado:** Mayor gap entre cards (16-20px) para facilitar scroll
- **Precios:** Sección de precios reorganizada en layout compacto vertical
- **Íconos:** Tamaño optimizado para visualización en pantallas pequeñas

##### ✅ VALIDACIONES DE QA

- [ ] **VAL-DIS-CARD-001:** V2 de card requiere configuración
  - **Verificar:** Agencia tiene activa V2 de card de Disney en configuración
- [ ] **VAL-DIS-CARD-002:** Encabezado muestra cantidad de días correctamente
  - **Verificar:** Título con formato "1 Día" / "X Días", tipografía bold, color verde oscuro
- [ ] **VAL-DIS-CARD-003:** Fechas con íconos y formato correcto
  - **Verificar:** "Fecha de ingreso" y "Entrada válida hasta" con ícono calendario verde, formato "día, dd de mes de aaaa"
- [ ] **VAL-DIS-CARD-004:** Precios por pasajero visibles
  - **Verificar:** "USD $XXX / Adulto" y "USD $XXX / Niño" visibles con formato correcto
- [ ] **VAL-DIS-CARD-005:** Precio "Desde" destacado correctamente
  - **Verificar:** Label "Desde", precio en verde institucional (#00563F), bold, tamaño grande
- [ ] **VAL-DIS-CARD-006:** Texto informativo precio por día visible
  - **Verificar:** "Precio por persona por día" visible debajo del precio total, texto pequeño gris
- [ ] **VAL-DIS-CARD-007:** Botón "Seleccionar" funcional
  - **Verificar:** Color verde, texto blanco centrado, ancho completo dentro de card, clic abre modal "Mejora tu tipo de entrada"
- [ ] **VAL-DIS-CARD-008:** Grid responsivo funciona correctamente
  - **Verificar:** Desktop 2-4 columnas, Tablet 2 columnas, Móvil 1 columna (stack vertical)
- [ ] **VAL-DIS-CARD-009:** Hover effect en desktop
  - **Verificar:** Sombra más pronunciada o borde verde al pasar cursor sobre card
- [ ] **VAL-DIS-CARD-010:** Estado deshabilitado si sin disponibilidad
  - **Verificar:** Card con opacidad reducida, botón gris con cursor not-allowed
- [ ] **VAL-DIS-CARD-011:** Variaciones móviles - Layout vertical
  - **Verificar:** Cards apiladas verticalmente, ancho 100% con padding lateral, scroll fluido
- [ ] **VAL-DIS-CARD-012:** Variaciones móviles - Botón táctil
  - **Verificar:** Botón "Seleccionar" área táctil mínima 44x44px, ancho completo, tap feedback visible

##### 🧪 Escenarios de Prueba

**Escenario 1: Selección de paquete 1 día**

- **Precondición:** Usuario en Disponibilidad, listado de paquetes visible (1-10 días)
- **Pasos:**
  1. Localizar card "1 Día"
  2. Verificar "Fecha de ingreso: mié, 23 oct 2025" con ícono calendario verde
  3. Verificar "Entrada válida hasta: mié, 23 oct 2025"
  4. Verificar "Precio por pax: USD $189 / Adulto | USD $189 / Niño"
  5. Verificar "Desde USD $200" en verde bold
  6. Verificar texto "Precio por persona por día" debajo
  7. Clic en botón "Seleccionar"
- **Resultado esperado:** Abre modal "Mejora tu tipo de entrada" con 5 opciones de parques (Animal Kingdom pre-seleccionado)

**Escenario 2: Selección de paquete 5 días - Economía de escala**

- **Precondición:** Usuario en Disponibilidad con búsqueda para 1 adulto
- **Pasos:**
  1. Localizar card "5 Días"
  2. Verificar fechas: "Fecha de ingreso: mié, 22 oct 2025" y "Entrada válida hasta: dom, 26 oct 2025"
  3. Verificar precio "Desde USD $320" (ejemplo)
  4. Calcular costo por día: $320 ÷ 5 = $64/día
  5. Comparar con paquete 1 día: $200/día
  6. Verificar economía: 68% menos costo por día
  7. Clic en "Seleccionar"
- **Resultado esperado:** Modal se abre mostrando que precio final variará según tipo de entrada seleccionado

**Escenario 3: Hover effect en desktop**

- **Precondición:** Usuario en Disponibilidad en desktop
- **Pasos:**
  1. Posicionar cursor sobre card "3 Días"
  2. Observar efecto visual
- **Resultado esperado:** Card muestra sombra más pronunciada o borde verde, indicando interactividad

**Escenario 4: Grid responsivo - Cambio de viewport**

- **Precondición:** Usuario en Disponibilidad, pantalla desktop (>1200px)
- **Pasos:**
  1. Verificar grid muestra 3-4 columnas de cards
  2. Reducir viewport a tablet (768-1199px)
  3. Verificar grid reorganiza a 2 columnas
  4. Reducir viewport a móvil (<768px)
  5. Verificar cards apiladas verticalmente (1 columna)
- **Resultado esperado:** Grid responsivo ajusta correctamente sin pérdida de información

**Escenario 5: Variaciones móviles - Scroll y tap feedback**

- **Precondición:** Usuario en Disponibilidad en móvil
- **Pasos:**
  1. Verificar cards ocupan 100% ancho con padding lateral
  2. Hacer scroll vertical entre cards
  3. Verificar 1.5-2 cards visibles en viewport inicial
  4. Hacer tap en botón "Seleccionar" de card "2 Días"
  5. Observar tap feedback visual
- **Resultado esperado:** Scroll fluido, botón con área táctil >44px, tap feedback visible, modal se abre correctamente

---

#### 🔹 Funcionalidad: Listado de Opciones de Entrada (1-10 Días)

> **Documentación completa disponible en:** [Knowledge_Base_Promerica.md - Listado de Opciones de Entrada](../../../../../knowledge-bases/Knowledge_Base_Promerica.md)

Esta funcionalidad muestra el grid completo de paquetes Disney desde 1 hasta 10 días con lógica de economía de escala (más días = menor costo por día). Cada paquete se representa mediante una Card de Paquetes Disney documentada en la funcionalidad anterior.

**Componentes principales:**

- Grid de 10 cards (1-10 días)
- Indicador de resultados: "Mostrando 10 paquetes disponibles"
- Avatares de pasajeros (visual)
- Texto informativo: "Entrada gratuita para menores de 3 años"

**Referencia:** Ver [Knowledge_Base_Promerica.md](../../../../../knowledge-bases/Knowledge_Base_Promerica.md) para ejemplos de precios, rangos de fechas y lógica completa de economía de escala.

---

#### 🔹 Funcionalidad: Modal de Selección de Tipo de Entrada (Mejora tu tipo de entrada)

> **Documentación completa disponible en:** [Knowledge_Base_Promerica.md - Modal de Selección de Tipo de Entrada](../../../../../knowledge-bases/Knowledge_Base_Promerica.md)

Modal interactivo que se despliega después de seleccionar un paquete de días, permitiendo al usuario elegir el tipo de entrada específico según los parques que desea visitar.

**Estructura del modal:**

1. Encabezado: "Entrada de [X] día(s)" + fechas válidas + descripción
2. Sección: "Mejora tu tipo de entrada"
3. Grid de 5 opciones:
   - Animal Kingdom (seleccionada por defecto)
   - EPCOT
   - Hollywood Studios
   - Magic Kingdom
   - Park Hopper (premium)

**Referencia:** Ver [Knowledge_Base_Promerica.md](../../../../../knowledge-bases/Knowledge_Base_Promerica.md) para detalles completos de cada opción, parques incluidos, precios y comportamiento del modal.

---

### 💡 Referencia a Slider Puntos + Plata

> 📋 **Documentación completa:** Ver sección **"Slider Puntos + Plata"** en [Knowledge_Base_Promerica.md](../../../../../knowledge-bases/Knowledge_Base_Promerica.md)

El slider es un componente transversal aplicable a todos los productos (Vuelos, Autos, Hoteles, Disney, Actividades) que permite al usuario ajustar dinámicamente la proporción de pago entre Puntos y Plata (dinero).

**Para detalles completos consultar el Knowledge Base:**

- Comportamiento esperado del slider
- Validaciones de saldo de puntos
- Cálculo dinámico de conversión
- Variaciones móviles
- Estados del componente

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

### Versión 1.1 - 2026-02-03

**Cambios principales:**

- ✅ **Actualización completa según Knowledge_Base_Promerica.md (Disney V2)**
- ✅ **Módulo HOME/LOGIN actualizado:**
  - Widget de Búsqueda de Disney V2: Simplificado sin selección inicial de parques/tipo entrada
  - Datepicker dual mejorado con navegación rápida
  - Modal de pasajeros con rangos Adultos/Niños
  - 10 validaciones actualizadas (VAL-DIS-HOME-001 a 010)
  - 5 escenarios de prueba actualizados
- ✅ **Módulo DISPONIBILIDAD actualizado con 4 funcionalidades V2:**
  - **Widget de Búsqueda V2 (Cerrado/Desplegable):**
    - Estados cerrado/expandido con transición smooth
    - Campo "Código de promoción (opcional)" agregado
    - 11 validaciones (VAL-DIS-WIDGET-001 a 011)
    - 5 escenarios de prueba
  - **Card de Paquetes Disney (1-10 días):**
    - Descripción funcional con economía de escala
    - 4 componentes en tablas: Encabezado, Fechas, Precios, Botón
    - Comportamiento esperado: diseño visual, precio "Desde", lógica economía de escala
    - 12 validaciones (VAL-DIS-CARD-001 a 012)
    - 5 escenarios de prueba
  - **Listado de Opciones de Entrada (1-10 Días):** Referencia a Knowledge Base
  - **Modal de Selección de Tipo de Entrada:** Referencia a Knowledge Base (5 opciones: Animal Kingdom default, EPCOT, Hollywood, Magic Kingdom, Park Hopper)
- ✅ **Añadida sección de referencia a Slider Puntos + Plata**
- ✅ **Añadido disclaimer de precios dinámicos en DISPONIBILIDAD**
- ✅ **Flujo de interacción general (8 pasos) agregado**
- ✅ **Variaciones móviles específicas por funcionalidad**
- ✅ **Control de Cambios actualizado a v1.1**

**Diferencias clave v1.1 vs v1.0:**

- v1.0: Widget HOME con selección upfront de parques/tipo ticket
- v1.1: Widget HOME simplificado → Solo fechas + pasajeros → Paquetes por días → Modal para selección final de parque
- v1.0: Cards genéricas de tickets
- v1.1: Cards específicas de paquetes (1-10 días) con economía de escala
- v1.0: Sin código promocional
- v1.1: Campo código promocional en widget desplegable

**Referencia completa:** [Knowledge_Base_Promerica.md - Sección Disney](../../../../../knowledge-bases/Knowledge_Base_Promerica.md)

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
