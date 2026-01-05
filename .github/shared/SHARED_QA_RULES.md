# 📚 REGLAS COMPARTIDAS QA - PM & BGR

> **Archivo de referencia para PM_QA_Assistant y BGR_QA_Assistant**  
> Contiene reglas comunes aplicables a ambos agentes

---

## 🎯 FUNDAMENTOS ISTQB

### Principios Obligatorios

1. **Todo caso de prueba DEBE incluir:**
   - Título descriptivo y específico
   - Descripción del objetivo (HTML)
   - Criterios de aceptación (HTML)
   - Pasos completos desde login
   - Resultado esperado por cada paso
   - Prioridad (1-4)

2. **Inicio desde Login (SIEMPRE):**
   - No se permite iniciar en "home", "checkout", "disponibilidad"
   - Si el usuario pide un caso que no empiece en login → corregir automáticamente
   - Razón: Garantizar reproducibilidad completa

3. **Trazabilidad:**
   - Todo caso debe poder vincularse a una HU (testsWorkItemId opcional)
   - Coherencia entre Descriptions, Considerations y Steps

---

## 🔧 INTEGRACIÓN AZURE DEVOPS VÍA MCP

> **CRÍTICO:** Todas las operaciones de Azure DevOps se realizan **exclusivamente mediante herramientas MCP** (Model Context Protocol).
> No se permite ni requiere intervención manual. El agente ejecuta automáticamente:
> - `mcp_microsoft_azu_testplan_create_test_case` (crear casos)
> - `mcp_microsoft_azu_wit_update_work_item` (actualizar campos HTML)
> - `mcp_microsoft_azu_testplan_add_test_cases_to_suite` (agregar a suite)
> - `mcp_microsoft_azu_wit_get_work_item` (obtener HU)

### Campos Obligatorios

```yaml
Título: [PREFIJO] [Producto] - [Escenario] - [Variante]
Descriptions: HTML (sin <div> ni <span>)
Considerations: HTML (campo Custom.Conciderations - typo del sistema)
Steps: Formato "Acción | Resultado esperado"
Priority: 1-4 (1=Crítico, 4=Nice-to-have)
Area Path: ultragroupla\Kepler
Iteration Path: ultragroupla\2025_Q4\SP20-2025
testsWorkItemId: [Opcional]
```

### Formato HTML Estándar

**Descriptions:**
```html
<strong>🗒️ Descripción del Test Case:</strong><br>
[Descripción completa del objetivo del caso]<br>
```

**Considerations (Custom.Conciderations):**
```html
<strong>✅ Criterios de Aceptación:</strong><br>
• [Criterio 1]<br>
• [Criterio 2]<br>
```

---

## ⚡ PROCESO DE CREACIÓN

### Flujo Obligatorio

1. **Solicitar planId y suiteId** (ambos obligatorios)
   - Ejemplo URL: `https://dev.azure.com/ultragrouplaorg/ultragroupla/_testPlans/define?planId=121536&suiteId=121850`
   - Si no se proporcionan → DETENER y solicitar

2. **Generar casos de prueba completos:**
   - Analizar HU/criterios
   - Aplicar técnicas ISTQB (partición equivalencia, valores límite)
   - Identificar flujo normal + errores + casos límite

3. **Presentar tabla para validación:**
   - Mostrar todos los casos en formato tabla
   - Esperar confirmación del usuario

4. **Preguntar antes de crear:**
   ```
   ¿Procedo a crear los {N} casos en Azure DevOps en planId={PLAN} suiteId={SUITE}? (sí/no/ajusta)
   ```

5. **Crear UNO POR UNO (CRÍTICO):**
   ```
   Para cada caso:
   a. Crear test case → obtener ID
   b. Actualizar campos HTML (Descriptions + Considerations)
   c. Agregar a suite
   d. Validar agregado
   e. Continuar con siguiente (NO en paralelo)
   ```

6. **Validación post-creación:**
   - Confirmar todos los IDs creados
   - Validar presencia en el suite
   - Mostrar resumen final

---

## 🚫 RECHAZO AUTOMÁTICO

Rechazar y pedir corrección si:

- ❌ Falta Descriptions
- ❌ Falta Considerations
- ❌ Pasos no empiezan en login
- ❌ Pasos no tienen resultado esperado
- ❌ No se dio suiteId
- ❌ Texto contiene el carácter "|" dentro de las acciones (reservado para separador)
- ❌ Usuario pide algo que va contra ISTQB

---

## 📊 PRIORIZACIÓN

### Escala de Prioridad

| Nivel | Criterio | Ejemplos |
|-------|----------|----------|
| **1** | Crítico para negocio | Flujo completo de compra, pago, emisión |
| **2** | Importante funcional | Validaciones de campos, filtros, búsqueda |
| **3** | Nice-to-have | Tooltips, mensajes informativos |
| **4** | Cosmético/UX | Colores, alineación, estilos |

---

## 🎨 NOMENCLATURA DE CASOS

### Formato Obligatorio

```
[PREFIJO] [Producto] - [Escenario] - [Variante] - [Proveedor si aplica]
```

### Ejemplos Correctos

```
✅ [PM] Vuelos - Ida y vuelta - Sabre - Fee con lightbox
✅ [PM] Hoteles - 2 noches - HotelBeds - Cancelación gratuita
✅ [PM] Autos - Dropoff diferente - Hertz - 5 días

✅ [BGR] Vuelos - Solo ida - Agregador - Millas + Plata manual
✅ [BGR] Hoteles - 3 noches - HotelBeds - Solo Millas automático
✅ [BGR] Actividades - Tour - HotelBeds - Cancelación con devolución
```

### Ejemplos Incorrectos

```
❌ Vuelos ida y vuelta (falta prefijo [PM] o [BGR])
❌ E2E Checkout (no específico, sin prefijo)
❌ Validar disponibilidad (no empieza en login implícito)
```

---

## 🔍 TÉCNICAS ISTQB APLICABLES

### 1. Partición de Equivalencia

Dividir inputs en clases válidas e inválidas:
- **Válidas:** Dentro de rango esperado
- **Inválidas:** Fuera de rango o formato incorrecto

**Ejemplo (Pasajeros):**
- Válida: 1-9 pasajeros
- Inválida: 0 pasajeros, 10+ pasajeros, letras

### 2. Valores Límite

Probar en los bordes de las particiones:
- Mínimo válido
- Máximo válido
- Justo debajo del mínimo
- Justo encima del máximo

**Ejemplo (Fechas):**
- Hoy (mínimo válido)
- Hoy - 1 día (inválido)
- 1 año adelante (máximo válido)
- 1 año + 1 día (inválido)

### 3. Tabla de Decisión

Para lógica compleja con múltiples condiciones:

| Millas suficientes | Slider > Mínimo | Resultado |
|--------------------|-----------------|-----------|
| Sí | Sí | Permitir compra |
| Sí | No | Bloquear (slider mínimo) |
| No | - | Mostrar error saldo |

---

## ✅ VALIDACIONES UNIVERSALES

### Integridad de Datos

En TODOS los productos validar:

1. **Consistencia entre pantallas:**
   - Búsqueda → Disponibilidad → Resumen → Checkout → Confirmación → Admin
   - Valores deben coincidir exactamente

2. **Campos obligatorios:**
   - No permitir avanzar sin completar
   - Botones deshabilitados hasta completar

3. **Enlaces funcionales:**
   - Términos y condiciones abre correctamente
   - Tratamiento de datos abre correctamente

4. **Estados de reserva:**
   - Confirmación: Código de reserva visible
   - Admin: Reserva localizable por código
   - Pagos coinciden en todos los sistemas

---

## 🔐 SEGURIDAD Y PRIVACIDAD

### No incluir en casos de prueba:

- ❌ Datos personales reales (nombres, emails, documentos)
- ❌ Números de tarjeta reales
- ❌ Contraseñas o tokens
- ❌ Información de cuentas de usuario reales

### Usar datos de prueba:

- ✅ Usuario: usuario.prueba@test.com
- ✅ Nombres: Juan Pérez, María González
- ✅ Documentos: 1234567890 (genéricos)
- ✅ Tarjetas: Usar números de prueba del gateway

---

## 📝 BUENAS PRÁCTICAS

1. **Atomicidad:** Un caso = Una funcionalidad específica
2. **Independencia:** Casos no deben depender de ejecución previa
3. **Repetibilidad:** Mismo input = Mismo output
4. **Claridad:** Pasos entendibles sin conocimiento previo
5. **Mantenibilidad:** Fácil actualizar cuando cambie funcionalidad

---

## 🎓 GLOSARIO COMPARTIDO

| Término | Definición |
|---------|------------|
| **HU** | Historia de Usuario |
| **E2E** | End-to-End (flujo completo) |
| **Admin** | Módulo de administración (PM o BGR) |
| **Emisión** | Proceso de confirmar reserva en sistema |
| **Dispersión** | Distribución de fondos (fee vs valor producto) |
| **Proveedor** | Sistema externo (Sabre, HotelBeds, etc.) |
| **Suite** | Conjunto de casos de prueba en Azure DevOps |
| **Test Plan** | Plan de pruebas en Azure DevOps |

---

**Última actualización:** Diciembre 16, 2025  
**Aplica a:** PM_QA_Assistant.agent.md, BGR_QA_Assistant.agent.md
