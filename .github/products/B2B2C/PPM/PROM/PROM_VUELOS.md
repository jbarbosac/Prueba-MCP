# 🛫 FLUJO E2E OBLIGATORIO PARA VUELOS - PROMERICA REWARDS

> **📖 Información Global:** Ver [PROM_QA_Assistant.agent.md](../../../../agents/PROM_QA_Assistant.agent.md) para URL del portal, país activo, modelo de negocio y versión del marketplace.

---

## 📦 PROVEEDORES DISPONIBLES

⚠️ **PENDIENTE DE DEFINIR**

**Proveedores potenciales:**

- AGGREGATOR - NETACTICA
- AGGREGATOR - SABRE
- SABRE EDIFACT
- [Otros por confirmar]

---

## 🔧 COMPONENTES TRANSVERSALES

> **Nota:** Estos componentes son compartidos por todos los productos del marketplace (Vuelos, Autos, Hoteles, Disney, Actividades).

### Header Global

**Descripción:** Barra superior con navegación principal, branding personalizado de Promerica y acceso de usuario.

**Componentes:**

- Logo de Promerica (branding personalizable según país)
- Menú desplegable "Beneficios" (con ícono dropdown)
- Menú desplegable "Viajes" (con ícono dropdown)
- Menú desplegable "Más" (con ícono dropdown)
- Link "Contáctenos"
- Indicador de país de operación (esquina superior derecha)
- Perfil de usuario con iniciales, nombre completo y dropdown

### Tabs de Productos

**Descripción:** Pestañas horizontales para navegación entre productos.

**Componentes:**

- Tab "Vuelos" (activo con subrayado verde)
- Tab "Autos"
- Tab "Hoteles"
- Tab "Disney"
- Tab "Actividades"

### Footer Global

**Descripción:** Sección inferior con información institucional y canales de contacto personalizados por país.

**Componentes:**

- Logo y texto descriptivo de Promerica
- Sección "Enlaces" (Información del programa, Términos, Política de privacidad)
- Sección "Canales de atención" (Email, Teléfono)
- Redes sociales (Facebook, Instagram, X/Twitter)
- Copyright con año y país

---

## 📋 PASOS OBLIGATORIOS DEL FLUJO E2E

**Siempre incluir estos pasos desde login para el flujo completo de Vuelos:**

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

**Descripción:** Página principal del marketplace donde el usuario accede al buscador de vuelos y navega entre productos disponibles. La interfaz es personalizable según el país configurado (Costa Rica en Test).

---

### Widget de Búsqueda de Vuelos

**Descripción:** Formulario principal para búsqueda de vuelos con múltiples opciones de configuración.

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

**Comportamiento esperado:**

- Radio "Ida y vuelta" muestra selector de fecha de regreso
- Radio "Solo ida" oculta fecha de regreso
- Toggle "Vuelos directos" filtra solo vuelos sin escalas
- Campos origen/destino muestran autocompletado con íconos de aeropuertos
- Campo fechas previene selección de fechas pasadas
- **Validación:** Origen y destino son obligatorios
- **Validación:** Fechas son obligatorias
- Botón "Buscar" deshabilitado si faltan campos requeridos
- Al buscar, redirige a módulo de Disponibilidad

**Variaciones Móviles:**

- **Selector de pasajeros:** Usa contadores +/- verticales en lugar de dropdown expandible
- **Teclado nativo:** Al seleccionar campos de origen/destino, aparece teclado móvil con barra de búsqueda
- **Sticky bar:** El botón "Buscar" permanece fijo en la parte inferior de la pantalla al hacer scroll

---

## 📋 MÓDULO: DISPONIBILIDAD

**Descripción:** Módulo que muestra los resultados de búsqueda de vuelos disponibles según los criterios del usuario. Incluye filtros, ordenamiento y visualización detallada de opciones.

---

### Resumen de Búsqueda

**Descripción:** Barra compacta que muestra los criterios de búsqueda aplicados.

**Componentes:**

- Ruta seleccionada (origen - destino)
- Fechas de viaje
- Número de pasajeros
- Clase de cabina
- Botón: Modificar búsqueda

**Comportamiento esperado:**

- Botón "Modificar búsqueda" permite editar criterios sin perder contexto
- Resumen visible durante navegación de resultados

---

### Filtros

**Descripción:** Panel lateral para refinar búsqueda de vuelos.

**Componentes:**

- Filtro por aerolínea (checkboxes o dropdown)
- Filtro por precio (rango deslizante)
- Filtro por horario de salida
- Filtro por horario de llegada
- Filtro por número de escalas
- Filtro por duración del vuelo
- Filtro por aeropuertos
- Botón: Limpiar filtros

**Comportamiento esperado:**

- Actualización dinámica de resultados al aplicar filtros
- Contador de resultados filtrados
- Persistencia de filtros durante la sesión
- Filtros se aplican de forma acumulativa

---

### Cards de Resultados

**Descripción:** Tarjetas individuales que muestran información de cada vuelo disponible.

**Componentes (por cada card):**

- Logo de aerolínea
- Horario de salida
- Horario de llegada
- Duración total del vuelo
- Número de escalas
- Aeropuertos de escala (si aplica)
- **Precio en Puntos + Plata** (modelo slider)
- Información de equipaje
- Botón: Seleccionar / Ver detalles

**Comportamiento esperado:**

- Hover en card muestra borde destacado
- Clic en card abre detalle expandido
- Visualización clara del modelo Puntos + Plata
- Carga lazy de cards adicionales al hacer scroll

---

### Ordenamiento de Resultados

**Descripción:** Opciones para ordenar la lista de vuelos.

**Componentes:**

- Ordenar por: Precio (menor a mayor)
- Ordenar por: Duración (menor a mayor)
- Ordenar por: Horario de salida
- Ordenar por: Aerolínea
- Ordenar por: Puntos (si aplica modelo slider)

**Comportamiento esperado:**

- Reordenamiento inmediato de resultados
- Indicador visual del criterio activo

---

### Detalle Expandido de Vuelo

**Descripción:** Vista ampliada con información completa del vuelo seleccionado.

**Componentes:**

- Itinerario completo (origen, escalas, destino)
- Detalles de cada tramo (aeropuerto, terminal, duración)
- Información de equipaje permitido
- Políticas de cambio y cancelación
- **Slider Puntos + Plata** (modelo híbrido)
- Botón: Continuar con este vuelo

**Comportamiento esperado:**

- Modal o sección expandible con toda la información
- Slider permite ajustar combinación Puntos/Plata
- Validación de saldo suficiente
- Botón "Continuar" redirige a Checkout

---

## 💳 MÓDULO: CHECKOUT

> ⚠️ **Documentación en proceso**  
> Este módulo está siendo estandarizado según el Knowledge Base de Promerica.  
> Se está trabajando en la documentación de: Formulario de pasajeros, Datos de contacto, Servicios adicionales, Métodos de pago, Resumen de reserva.  
> **Estado:** 🔄 Pendiente de completar

---

## ✅ MÓDULO: CONFIRMACIÓN

> ⚠️ **Documentación en proceso**  
> Este módulo está siendo estandarizado según el Knowledge Base de Promerica.  
> Se está trabajando en la documentación de: Confirmación exitosa, Número de reserva (PNR), Voucher descargable, Error en procesamiento.  
> **Estado:** 🔄 Pendiente de completar

---

## ✅ VALIDACIONES CRÍTICAS

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

## 📝 FORMATO DE TÍTULO

```
[PROM] Vuelos - [Tipo de vuelo] - [Proveedor] - [Clase] - [Pasajeros] - [Modelo de pago]
```

**Ejemplos actualizados:**

- `[PROM] Vuelos - Ida y vuelta - SABRE - Económica - 1 adulto - Puntos + Plata`
- `[PROM] Vuelos - Solo ida - AGGREGATOR NETACTICA - Económica - 2 adultos 1 niño - Solo Puntos`
- `[PROM] Vuelos - Ida y vuelta - AGGREGATOR SABRE - Ejecutiva - 3 adultos - Puntos + Plata (50%)`

---

## 🚀 PRÓXIMOS PASOS PARA COMPLETAR ESTE ARCHIVO

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
