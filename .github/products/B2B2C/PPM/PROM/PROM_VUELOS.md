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

#### 🔹 Funcionalidad: Resumen de Búsqueda

##### 📖 Descripción Funcional

Barra compacta informativa que muestra los criterios de búsqueda actualmente aplicados, permitiendo al usuario tener contexto constante de su búsqueda y la posibilidad de modificarla sin perder su posición en los resultados.

**Ubicación:** Parte superior del módulo Disponibilidad, encima de los resultados  
**Tipo de componente:** Barra informativa con acción de edición  
**Persistencia:** Visible durante toda la navegación en Disponibilidad

##### 🧩 Componentes

| Componente | Descripción | Tipo | Editable |
|------------|-------------|------|----------|
| **Ruta** | Origen - Destino (ejemplo: "SJO - MIA") | Text | ❌ |
| **Fechas de viaje** | Ida y regreso (o solo ida) | Text | ❌ |
| **Número de pasajeros** | Total de pasajeros y tipos | Text | ❌ |
| **Clase de cabina** | Económica, Ejecutiva, etc. | Text | ❌ |
| **Botón modificar** | "Modificar búsqueda" o ícono editar | Button | ✅ |

##### 💻 Comportamiento Esperado

**Visualización:**
- Resumen muestra información condensada pero completa de la búsqueda
- Formato claro y legible (ejemplo: "SJO - MIA • 15-25 Feb • 2 adultos • Económica")

**Interacción:**
- Clic en "Modificar búsqueda" → Abre widget de búsqueda con datos precargados
- Usuario puede editar cualquier campo sin perder el contexto
- Al buscar nuevamente, resultados se actualizan

**Persistencia:**
- Resumen permanece visible al hacer scroll en resultados
- Se mantiene durante navegación entre páginas de resultados

##### ✅ VALIDACIONES DE QA

- [ ] **VAL-VUE-DISP-RESUM-001:** Resumen coincide con búsqueda original
  - **Verificar:** Datos en resumen = Datos configurados en Widget de Búsqueda
  
- [ ] **VAL-VUE-DISP-RESUM-002:** Botón "Modificar búsqueda" funciona
  - **Verificar:** Abre widget con datos precargados correctamente
  
- [ ] **VAL-VUE-DISP-RESUM-003:** Resumen visible durante navegación
  - **Verificar:** Permanece visible al hacer scroll o cambiar páginas

##### 🧪 Escenarios de Prueba

**Escenario 1: Verificación de resumen de búsqueda - MGA a MIA**
- **Prioridad:** 1 (Crítico)
- **Precondición:** Búsqueda ejecutada desde Home (MGA-MIA, 1 adulto)
- **Pasos:**
  1-10. [Pasos de búsqueda desde Home según Escenario 1 de HOME]
  11. En Disponibilidad, localizar barra de Resumen de Búsqueda
  12. **Validar:** Ruta muestra "MGA - MIA"
  13. **Validar:** Fechas coinciden con las seleccionadas
  14. **Validar:** Muestra "1 adulto"
  15. **Validar:** Clase mostrada correctamente
- **Resultado esperado:** Resumen preciso y completo para ruta MGA-MIA
- **Título ADO:** `[PROM] Vuelos - Disponibilidad - Resumen correcto - MGA a MIA - 1 adulto`

---

#### 🔹 Funcionalidad: Filtros Dinámicos

##### 📖 Descripción Funcional

Panel lateral de filtrado que permite refinar los resultados de búsqueda aplicando múltiples criterios simultáneamente. Los filtros se aplican de forma acumulativa y actualizan los resultados en tiempo real sin recargar la página.

**Ubicación:** Panel lateral izquierdo en desktop, drawer expandible en móvil  
**Tipo de componente:** Panel de filtros con controles múltiples  
**Actualización:** Dinámica (sin recarga de página)

##### 🧩 Componentes

| Componente | Descripción | Tipo | Funcionalidad |
|------------|-------------|------|---------------|
| **Filtro aerolínea** | Checkboxes con logos y nombres de aerolíneas | Multi-checkbox | Filtrar por 1+ aerolíneas |
| **Filtro precio** | Rango deslizante min-max | Range Slider | Definir rango de precios |
| **Filtro horario salida** | Rangos horarios (mañana, tarde, noche) | Checkbox/Time Range | Filtrar por franja horaria |
| **Filtro horario llegada** | Rangos horarios (mañana, tarde, noche) | Checkbox/Time Range | Filtrar por franja horaria |
| **Filtro escalas** | Opciones: Sin escalas, 1 escala, 2+ escalas | Checkbox | Filtrar por cantidad escalas |
| **Filtro duración** | Rango de horas (ej: 2-12 horas) | Range Slider | Filtrar por duración total |
| **Filtro aeropuertos** | Aeropuertos específicos para escalas | Multi-checkbox | Incluir/excluir aeropuertos |
| **Botón limpiar** | "Limpiar filtros" o ícono reset | Button | Remover todos los filtros |

##### 💻 Comportamiento Esperado

**Aplicación de filtros:**
- Filtros se aplican de forma acumulativa (AND lógico)
- Actualización de resultados en tiempo real (< 1 segundo)
- Contador muestra cantidad de resultados filtrados (ej: "24 vuelos encontrados")

**Interacción:**
- Clic en checkbox →Filtro se aplica inmediatamente
- Movimiento de slider → Actualiza al soltar (onMouseUp) o con delay (300ms)
- Filtros múltiples del mismo tipo actúan como OR (ej: Aerolínea A o B)

**Persistencia:**
- Filtros se mantienen durante la sesión
- Al modificar búsqueda, filtros se resetean
- Estado de filtros visible (checkboxes marcados, sliders en posición)

**Botón limpiar:**
- Remueve todos los filtros aplicados
- Restaura vista a resultados completos sin filtros
- Resetea todos los controles a su estado inicial

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
  1-11. [Pasos de búsqueda completa hasta ver resultados]
  12. Localizar panel de Filtros (izquierda en desktop)
  13. En "Filtro por aerolínea", seleccionar checkbox de "Copa Airlines"
  14. **Validar:** Resultados se actualizan automáticamente (< 1 seg)
  15. **Validar:** TODOS los resultados mostrados son de Copa Airlines
  16. **Validar:** Contador muestra "X vuelos encontrados" (reducido)
  17. Scroll por todos los resultados visible
  18. **Validar:** Ningún vuelo de otra aerolínea aparece
- **Resultado esperado:** Solo vuelos de Copa Airlines visibles
- **Título ADO:** `[PROM] Vuelos - Disponibilidad - Filtro aerolínea funciona correctamente`

**Escenario 2: Filtros acumulativos - MGA a MIA - 2 adultos - P+P**
- **Prioridad:** 1 (Crítico)
- **Modelo de pago:** Puntos + Plata (70%)
- **Precondición:** Búsqueda MGA-MIA con 2 adultos ejecutada
- **Pasos:**
  1. Login y buscar: MGA → MIA, ida y vuelta, 2 adultos
  2-11. [Completar búsqueda hasta ver resultados]
  12. Aplicar filtro: Seleccionar "Avianca"
  13. **Validar:** Solo vuelos Avianca visibles
  14. Aplicar filtro adicional: Seleccionar "Sin escalas"
  15. **Validar:** Resultados se reducen nuevamente
  16. **Validar:** TODOS los vuelos son Avianca Y sin escalas
  17. **Validar:** Precio mostrado para 2 adultos con modelo P+P
  18. Hacer scroll completo por resultados
  19. **Validar:** Ningún vuelo con escalas o de otra aerolínea
- **Resultado esperado:** Filtros acumulativos correctos para 2 adultos
- **Título ADO:** `[PROM] Vuelos - Disponibilidad - Filtros acumulativos - MGA a MIA - 2 adultos - P+P`

---

#### 🔹 Funcionalidad: Cards de Resultados

##### 📖 Descripción Funcional

Tarjetas individuales que presentan información resumida de cada vuelo disponible. Cada card muestra detalles clave del itinerario, precio en el modelo Puntos + Plata, y permite acceder al detalle expandido para más información.

**Ubicación:** Área central de resultados, listado vertical  
**Tipo de componente:** Card interactiva con información resumida  
**Carga:** Lazy loading (carga progresiva al hacer scroll)

##### 🧩 Componentes

| Componente | Descripción | Visualización |
|------------|-------------|---------------|
| **Logo aerolínea** | Imagen corporativa de la aerolínea | Image (40x40px aprox) |
| **Horario salida** | Hora de despegue formato 24h o 12h | Text (grande, bold) |
| **Horario llegada** | Hora de aterrizaje formato 24h o 12h | Text (grande, bold) |
| **Duración total** | Tiempo total de viaje (ej: "5h 30m") | Text (mediano) |
| **Número de escalas** | "Sin escalas", "1 escala", "2 escalas" | Badge/Chip |
| **Aeropuertos escalas** | Códigos IATA si aplica (ej: "PTY") | Text (pequeño, gris) |
| **Precio Puntos + Plata** | Visualización del modelo slider | Display dual |
| **Info equipaje** | Equipaje de mano/bodega incluido | Icon + Text |
| **Botón acción** | "Seleccionar" o "Ver detalles" | Button (principal) |

##### 💻 Comportamiento Esperado

**Visualización:**
- Cards se muestran en lista vertical ordenada
- Información clara y escaneable rápidamente
- Modelo Puntos + Plata visible en cada card

**Interacción:**
- Hover en card → Borde destacado (color verde o similar)
- Clic en card (área completa) → Abre detalle expandido
- Clic en botón "Seleccionar" → Abre detalle expandido (mismo comportamiento)

**Carga de resultados:**
- Primeros 10-20 cards se cargan inmediatamente
- Al hacer scroll cerca del final → Cargan siguientes 10-20 (lazy loading)
- Indicador de carga (spinner) mientras cargan más resultados

**Información de precio:**
- Precio mostrado según slider default o última configuración
- Formato claro: "12,500 pts + $250 USD" o similar

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

**Escenario 1: Visualización correcta de cards**
- **Prioridad:** 1 (Crítico)
- **Precondición:** Búsqueda con resultados disponibles
- **Pasos:**
  1-11. [Búsqueda completa hasta resultados]
  12. Localizar primera card de resultado
  13. **Validar:** Logo de aerolínea visible
  14. **Validar:** Horarios de salida y llegada visibles
  15. **Validar:** Duración total mostrada (formato "Xh Ym")
  16. **Validar:** Badge de escalas visible
  17. **Validar:** Precio en formato "X pts + $Y USD"
  18. **Validar:** Info de equipaje visible
  19. **Validar:** Botón "Seleccionar" o "Ver detalles" presente
- **Resultado esperado:** Card con información completa y legible
- **Título ADO:** `[PROM] Vuelos - Disponibilidad - Card muestra información completa`

---

#### 🔹 Funcionalidad: Ordenamiento de Resultados

##### 📖 Descripción Funcional

Control que permite al usuario reordenar la lista de vuelos según diferentes criterios (precio, duración, horario, etc.). El ordenamiento se aplica instantáneamente sobre los resultados visibles, respetando los filtros activos.

**Ubicación:** Encima de los resultados, generalmente a la derecha  
**Tipo de componente:** Dropdown o botones de ordenamiento  
**Actualización:** Inmediata (sin recarga)

##### 🧩 Componentes

| Opción de Ordenamiento | Descripción | Orden |
|------------------------|-------------|-------|
| **Precio (menor a mayor)** | Ordena por precio total ascendente | ASC |
| **Duración (menor a mayor)** | Ordena por tiempo total de viaje ascendente | ASC |
| **Horario de salida** | Ordena por hora de despegue (más temprano primero) | ASC |
| **Aerolínea** | Ordena alfabéticamente por nombre de aerolínea | ASC |
| **Puntos (si aplica)** | Ordena por cantidad de puntos requeridos | ASC |

##### 💻 Comportamiento Esperado

**Interacción:**
- Selección de criterio → Reordenamiento inmediato de cards (< 500ms)
- Indicador visual del criterio activo (checkmark, highlight, etc.)
- Ordenamiento default al cargar resultados (usualmente por Precio)

**Aplicación:**
- Se aplica sobre resultados filtrados (no resetea filtros)
- Nuevo ordenamiento reemplaza el anterior
- Ordenamiento se mantiene al cargar más resultados (lazy loading)

**Feedback visual:**
- Durante reordenamiento: transición suave de cards
- Criterio activo claramente identificable

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

**Escenario 1: Ordenamiento por precio**
- **Prioridad:** 2 (Importante)
- **Precondición:** Resultados con diferentes precios visibles
- **Pasos:**
  1-11. [Búsqueda completa]
  12. Localizar control de ordenamiento
  13. Seleccionar "Precio (menor a mayor)"
  14. **Validar:** Resultados se reordenan inmediatamente
  15. Revisar primeras 3 cards
  16. **Validar:** Precios en orden ascendente (más barato primero)
  17. Scroll hasta el final
  18. **Validar:** Último resultado tiene precio más alto
- **Resultado esperado:** Ordenamiento correcto por precio
- **Título ADO:** `[PROM] Vuelos - Disponibilidad - Ordenamiento por precio funciona`

---

#### 🔹 Funcionalidad: Detalle Expandido de Vuelo

##### 📖 Descripción Funcional

Vista ampliada que muestra información completa y detallada del vuelo seleccionado, incluyendo itinerario completo por tramo, políticas de equipaje y cambios, y el Slider de Puntos + Plata para ajustar el modelo de pago antes de continuar al Checkout.

**Ubicación:** Modal central o sección expandible en la página  
**Tipo de componente:** Modal/Drawer con información detallada + Slider interactivo  
**Acceso:** Clic en card de resultado

##### 🧩 Componentes

| Componente | Descripción | Interactivo |
|------------|-------------|-------------|
| **Itinerario completo** | Desglose de todos los tramos del viaje | ❌ |
| **Detalles por tramo** | Aeropuerto, terminal, puerta, duración por segmento | ❌ |
| **Info equipaje** | Equipaje de mano y bodega permitido | ❌ |
| **Políticas cambio/cancelación** | Reglas de la tarifa seleccionada | ❌ |
| **Slider Puntos + Plata** | Control para ajustar proporción de pago | ✅ |
| **Botón continuar** | "Continuar con este vuelo" | ✅ |
| **Botón cerrar** | Cerrar detalle y volver a resultados | ✅ |

##### 💻 Comportamiento Esperado

**Apertura:**
- Clic en card o botón "Ver detalles" → Abre modal/drawer
- Animación suave de apertura
- Fondo oscurecido (overlay) si es modal

**Información mostrada:**
- Itinerario completo con todos los tramos (ida y regreso)
- Para cada tramo: aeropuerto origen/destino, terminal, horarios, duración
- Escalas claramente identificadas con tiempos de espera
- Información de equipaje: peso y piezas permitidas
- Políticas de cambio y cancelación de la tarifa

**Slider Puntos + Plata:**
- Permite ajustar proporción antes de continuar
- Actualización en tiempo real de valores
- Validación de saldo disponible

**Navegación:**
- Botón "Continuar con este vuelo" → Redirige a Checkout
- Botón cerrar (X) o clic fuera del modal → Vuelve a resultados
- Vuelo seleccionado no se pierde

##### ✅ VALIDACIONES DE QA

- [ ] **VAL-VUE-DISP-DETALLE-001:** Modal se abre correctamente
  - **Verificar:** Abre al hacer clic en card, información visible
  
- [ ] **VAL-VUE-DISP-DETALLE-002:** Itinerario completo mostrado
  - **Verificar:** Todos los tramos con aeropuertos, horarios, terminales
  
- [ ] **VAL-VUE-DISP-DETALLE-003:** Información de equipaje visible
  - **Verificar:** Peso y piezas permitidas claras
  
- [ ] **VAL-VUE-DISP-DETALLE-004:** Slider funciona en detalle
  - **Verificar:** Ajusta proporción, valida saldo, actualiza en tiempo real
  
- [ ] **VAL-VUE-DISP-DETALLE-005:** Botón continuar redirige a Checkout
  - **Verificar:** URL cambia a módulo Checkout con vuelo seleccionado
  
- [ ] **VAL-VUE-DISP-DETALLE-006:** Botón cerrar vuelve a resultados
  - **Verificar:** Modal se cierra, resultados siguen visibles

##### 🧪 Escenarios de Prueba

**Escenario 1: Abrir y revisar detalle expandido**
- **Prioridad:** 1 (Crítico)
- **Precondición:** Resultados de búsqueda visibles
- **Pasos:**
  1-11. [Búsqueda completa]
  12. Hacer clic en primera card de resultado
  13. **Validar:** Modal/drawer se abre con animación
  14. **Validar:** Itinerario completo visible (todos los tramos)
  15. **Validar:** Información de equipaje presente
  16. **Validar:** Políticas de cambio/cancelación visibles
  17. **Validar:** Slider Puntos + Plata presente y funcional
  18. **Validar:** Botones "Continuar" y "Cerrar" visibles
- **Resultado esperado:** Detalle completo y navegación correcta
- **Título ADO:** `[PROM] Vuelos - Disponibilidad - Detalle expandido muestra información completa`

---

#### 🔹 Funcionalidad: Slider Puntos + Plata

> **Nota:** Esta funcionalidad es transversal y crítica del modelo de negocio Promerica. Se documenta aquí en detalle para referencia en casos de prueba.

##### 📖 Descripción Funcional

Control interactivo que permite al usuario ajustar dinámicamente la proporción de puntos y efectivo (plata) para el pago del vuelo seleccionado. El slider calcula en tiempo real la cantidad exacta de puntos a utilizar y el monto en efectivo a pagar, validando el saldo disponible del usuario.

**Ubicación:** Presente en cards de resultados (versión simplificada) y detalle expandido (versión completa)  
**Tipo de control:** Range slider con valores dinámicos  
**Rango:** TBD (mínimo configurable) - 100% en puntos (según reglas de negocio)  
**Validación:** Verifica saldo disponible en tiempo real

##### 🧩 Componentes

| Componente | Descripción | Actualización |
|------------|-------------|---------------|
| **Slider visual** | Barra horizontal con handle arrastrable | Manual (usuario) |
| **Label % Puntos** | Porcentaje actual en puntos | Tiempo real |
| **Label % Plata** | Porcentaje actual en efectivo | Tiempo real |
| **Display puntos** | Cantidad exacta de puntos (ej: "12,500 pts") | Tiempo real |
| **Display plata** | Monto exacto en efectivo (ej: "$450 USD") | Tiempo real |
| **Saldo disponible** | "Tienes X puntos disponibles" | Estático |
| **Mensaje error** | "Saldo insuficiente" (condicional) | Condicional |

##### 💻 Comportamiento Esperado

**Interacción principal:**
1. Usuario arrastra handle del slider → Aumenta/disminuye % puntos
2. Sistema recalcula en tiempo real (< 500ms):
   - Cantidad de puntos a usar
   - Monto en efectivo a pagar
   - Actualiza ambos displays simultáneamente

**Validaciones automáticas:**
- Verifica saldo disponible en cada movimiento
- Bloquea slider si usuario no tiene puntos suficientes
- Mantiene porcentaje mínimo (según configuración)
- Valida que total (puntos convertidos + plata) = precio del vuelo

**Estados:**
- **Normal:** Slider activo, cálculos correctos, saldo suficiente
- **Error saldo:** Slider bloqueado, mensaje "Saldo insuficiente de puntos"
- **Loading:** Spinner durante cálculo si API tarda (>500ms)

**Ejemplo de cálculo:**
```
Precio total vuelo: $1,000 USD
Tasa de conversión: 100 puntos = $1 USD

Slider al 50%:
- Puntos a usar: 50,000 pts
- Plata a pagar: $500 USD

Slider al 100%:
- Puntos a usar: 100,000 pts
- Plata a pagar: $0 USD

Slider al mínimo configurado (ejemplo: 20%):
- Puntos a usar: 20,000 pts
- Plata a pagar: $800 USD
```

##### ✅ VALIDACIONES DE QA

- [ ] **VAL-VUE-DISP-SLIDER-001:** Cálculo en tiempo real (< 500ms)
  - **Verificar:** Valores se actualizan inmediatamente al mover slider
  
- [ ] **VAL-VUE-DISP-SLIDER-002:** Validación de saldo de puntos
  - **Verificar:** Si saldo < requerido, slider bloqueado + mensaje error
  
- [ ] **VAL-VUE-DISP-SLIDER-003:** Porcentaje mínimo respetado (según configuración)
  - **Verificar:** Slider no permite ir debajo del mínimo configurado
  
- [ ] **VAL-VUE-DISP-SLIDER-004:** Copago en plata correcto
  - **Verificar:** Valor en $ = (Precio total - Puntos convertidos)
  
- [ ] **VAL-VUE-DISP-SLIDER-005:** Formato de números correcto
  - **Verificar:** Puntos con separadores de miles, plata con 2 decimales
  
- [ ] **VAL-VUE-DISP-SLIDER-006:** Mensaje error claro
  - **Verificar:** "Saldo insuficiente" visible y comprensible
  
- [ ] **VAL-VUE-DISP-SLIDER-007:** Persistencia al navegar
  - **Verificar:** Última posición del slider se mantiene

##### 🧪 Escenarios de Prueba

**Escenario 1: Ajuste exitoso Slider - MGA a MIA - 1 adulto**
- **Prioridad:** 1 (Crítico)
- **Ruta:** MGA → MIA (ida y vuelta)
- **Pasajeros:** 1 adulto
- **Precondición:** Usuario con 150,000 puntos disponibles, vuelo de $800
- **Pasos:**
  1-11. [Búsqueda MGA-MIA con 1 adulto y selección de vuelo]
  12. En detalle expandido, localizar Slider Puntos + Plata
  13. **Validar:** Saldo disponible mostrado correctamente (150,000 pts)
  14. Mover slider a 50% (Puntos + Plata equilibrado)
  15. **Validar:** Display muestra "40,000 pts + $400 USD" (o según tasa)
  16. Mover slider a 100% (Solo puntos)
  17. **Validar:** Display muestra "80,000 pts + $0 USD"
  18. Mover slider al mínimo permitido (según configuración)
  19. **Validar:** Display refleja el mínimo configurado (puntos/plata) y mantiene consistencia con la fórmula
  20. **Validar:** Slider no permite ir debajo del mínimo configurado
  21. **Validar:** Cálculos en tiempo real (< 500ms)
- **Resultado esperado:** Slider funcional con cálculos precisos P+P
- **Título ADO:** `[PROM] Vuelos - Disponibilidad - Slider P+P - MGA a MIA - 1 adulto`

**Escenario 2: Bloqueo por saldo insuficiente - MGA a MEX**
- **Prioridad:** 1 (Crítico)
- **Ruta:** MGA → MEX (Ciudad de México, ida y vuelta)
- **Pasajeros:** 1 adulto
- **Precondición:** Usuario con saldo de puntos inferior al mínimo requerido por configuración (TBD) y vuelo de $800
- **Pasos:**
  1. Login con usuario de saldo bajo (5,000 pts)
  2-11. [Búsqueda MGA-MEX, 1 adulto, selección de vuelo $800]
  12. En detalle expandido, localizar Slider Puntos + Plata
  13. **Validar:** Slider aparece bloqueado/deshabilitado
  14. **Validar:** Mensaje "Saldo insuficiente de puntos" visible
  15. **Validar:** Muestra saldo actual: "Tienes 5,000 puntos"
  16. **Validar:** Se muestra opción alternativa "Pagar 100% en efectivo: $800"
  17. Intentar mover slider
  18. **Validar:** Slider no responde, permanece bloqueado
- **Resultado esperado:** Usuario informado claramente, opción de pago alternativa visible
- **Título ADO:** `[PROM] Vuelos - Disponibilidad - Slider bloqueado - Saldo insuficiente - MGA a MEX`

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
- Evitar fijar valores ⚠️ *Pendiente/TBD* (ej. proveedor) dentro del título.

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

### Versión 1.0 - 2026-01-25

**Cambios principales:**

- ✅ Aplicada arquitectura híbrida (propósito dual: humanos + agente QA)
- ✅ Reorganizada jerarquía según estructura estándar de productos
- ✅ Módulo Home/Login con estructura completa:
  - 📖 Descripción Funcional
  - 🧩 Componentes (tabla estructurada)
  - 💻 Comportamiento Esperado
  - ✅ Validaciones de QA (8 validaciones)
  - 🧪 Escenarios de Prueba (3 escenarios detallados)
- ✅ Módulo Disponibilidad con 6 funcionalidades documentadas:
  - Resumen de Búsqueda
  - Filtros Dinámicos
  - Cards de Resultados
  - Ordenamiento de Resultados
  - Detalle Expandido de Vuelo
  - Slider Puntos + Plata (documentación extendida)
- ✅ Cada funcionalidad incluye validaciones QA y escenarios de prueba
- ✅ Formato optimizado para generación de casos por agente
- ✅ Información completa para consulta humana

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
