# 📚 Glosario de Términos

> Definiciones de términos técnicos y de negocio utilizados en el sistema de generación de test cases para PM y BGR.

---

## A

### Admin
Panel de administración de PM o BGR donde se gestionan las reservas. Permite buscar, visualizar, emitir y cancelar reservas.

### AGGREGATOR - NETACTICA
Proveedor de vuelos que consolida disponibilidad de múltiples aerolíneas. **No** incluye dispersión de fondos.

### AGGREGATOR - SABRE
Proveedor de vuelos basado en la plataforma Sabre que consolida disponibilidad. **No** incluye dispersión de fondos.

### Area Path
Campo obligatorio de Azure DevOps que define el área organizacional del caso de prueba.  
**Valor estándar:** `ultragroupla\Kepler`

### Azure DevOps
Plataforma de Microsoft para gestión de proyectos ágiles, control de versiones y pruebas. Utilizada para crear y gestionar test cases.

---

## B

### BGR
**BGR Miles** - Portal de redención de millas con modelo mixto (Millas + Plata) operado en Ecuador.  
**URL:** https://bgrmiles-ec.preprodppm.com/

### Botón Canjear
Botón principal en checkout que ejecuta la transacción de redención. Solo se habilita cuando todos los campos obligatorios están completos.

---

## C

### Canje
Acción de redimir millas por productos o servicios (vuelos, hoteles, autos, actividades, Disney).

### Checkout
Pantalla final del flujo de compra donde se ingresan datos del usuario, se validan términos y se ejecuta la transacción.

### Considerations (Custom.Conciderations)
Campo personalizado de Azure DevOps que contiene los criterios de aceptación del test case en formato HTML.  
**Nota:** El nombre del campo tiene un typo intencional del sistema (`Conciderations` en lugar de `Considerations`).

### Criterios de Aceptación
Condiciones que deben cumplirse para que un test case sea considerado exitoso. Se documentan en el campo Considerations.

---

## D

### Debitar millas
Acción administrativa de descontar millas de la cuenta del usuario. En BGR, este proceso es manual para transacciones Millas + Plata.

### Descriptions (Custom.Descriptions)
Campo personalizado de Azure DevOps que contiene la descripción completa del test case y referencias visuales en formato HTML.

### DerbySoft
Proveedor tecnológico para tickets de Disney en PM (Pichincha Miles).

### Dispersión de fondos
Proceso automático de SABRE EDIFACT que distribuye pagos entre aerolíneas involucradas en un vuelo. **Solo aplica en PM**, no en BGR.

### Dollar
Empresa de renta de autos disponible a través del proveedor Sabre.

### Drop-off fee
Cargo adicional aplicado cuando se devuelve un auto de alquiler en una ciudad diferente a la de recogida. Solo aplica en Autos.

---

## E

### E2E (End-to-End)
Flujo completo de prueba desde login hasta validación en admin. Incluye todas las pantallas y pasos del proceso.

### Emisión
Proceso de confirmar y activar una reserva. Puede ser:
- **Automática:** Sistema emite inmediatamente (100% millas)
- **Manual/Semiautomática:** Requiere intervención del admin (Millas + Plata en BGR)

### Estado EMITIDA
Estado final de una reserva que ha sido confirmada y activada correctamente.

### Estado PENDIENTE
Estado temporal de una reserva que requiere procesamiento manual antes de ser emitida. Aplica en BGR para transacciones Millas + Plata.

### Estado CANCELADO
Estado de una reserva que fue cancelada exitosamente con devolución de millas.

---

## F

### Fee de procesamiento
Cargo adicional en tarjeta de crédito para vuelos en PM. **Solo aplica en PM Vuelos**, no en otros productos ni en BGR.

---

## H

### Hertz
Empresa de renta de autos disponible a través del proveedor Sabre.

### HotelBeds
Proveedor global de hoteles y actividades utilizado tanto en PM como en BGR.

### HU (Historia de Usuario / User Story)
Requisito funcional en formato ágil del cual se derivan los casos de prueba. Se vincula mediante `testsWorkItemId`.

---

## I

### ISTQB
**International Software Testing Qualifications Board** - Estándar internacional para certificación en testing. Los test cases siguen sus principios y mejores prácticas.

### Iteration Path
Campo obligatorio de Azure DevOps que define el sprint o iteración del caso de prueba.  
**Valor estándar:** `ultragroupla\2025_Q4\SP20-2025`

---

## L

### Lightbox
Modal o ventana emergente para ingresar datos de tarjeta de crédito en el pago del fee. **Solo aplica en PM Vuelos**.

### Login
Pantalla de autenticación. **Todos los flujos E2E DEBEN iniciar desde login** sin excepción.

---

## M

### MCP (Model Context Protocol)

**Model Context Protocol** - Protocolo de integración con Azure DevOps utilizado por los agentes para **todas las operaciones automáticas**:
- Crear test cases (`mcp_microsoft_azu_testplan_create_test_case`)
- Actualizar campos HTML (`mcp_microsoft_azu_wit_update_work_item`)
- Agregar casos a suites (`mcp_microsoft_azu_testplan_add_test_cases_to_suite`)
- Obtener información de work items (`mcp_microsoft_azu_wit_get_work_item`)

**Todas las operaciones de Azure DevOps se ejecutan exclusivamente mediante MCP**, sin intervención manual del usuario.

### Millas
Puntos de fidelización canjeables por productos o servicios. Unidad de pago principal en ambos portales.

### Millas + Plata
Modelo de pago mixto exclusivo de BGR donde el usuario paga parte en millas y parte en dinero usando el slider.

---

## O

### OffLine
Proveedor de tickets Disney en BGR (diferente a DerbySoft en PM).

---

## P

### planId
Identificador numérico del Test Plan en Azure DevOps. **Obligatorio** para crear test cases.  
Ejemplo: `121536`

### Plata
Dinero en efectivo (moneda local). En BGR, se paga con tarjeta de crédito en el checkout cuando se selecciona el modelo Millas + Plata.

### PM
**Pichincha Miles** - Portal de redención 100% millas operado en Ecuador.  
**URL:** https://pichinchamiles-ec.preprodppm.com/

### PPM
**Programa Partners Miles** - Plataforma tecnológica base que soporta tanto PM como BGR.

### Prefijo
Etiqueta obligatoria al inicio del título de cada test case:
- `[PM]` para Pichincha Miles
- `[BGR]` para BGR Miles

### Priority
Campo obligatorio que indica la criticidad del test case:
- **1:** Crítico (blocker)
- **2:** Alto (major)
- **3:** Medio (normal)
- **4:** Bajo (nice-to-have)

### Proveedor
Sistema externo que proporciona disponibilidad y procesamiento de reservas:
- Vuelos: AGGREGATOR NETACTICA, AGGREGATOR SABRE, SABRE EDIFACT
- Hoteles/Actividades: HotelBeds
- Autos: Sabre
- Disney: DerbySoft (PM) / OffLine (BGR)

---

## R

### Reserva
Transacción completada que queda registrada en el sistema con un código único.

---

## S

### SABRE
Plataforma global de distribución (GDS) para vuelos y autos.

### SABRE EDIFACT
Proveedor de vuelos con capacidad de dispersión automática de fondos. **Solo en PM**.

### Slider
Control deslizante visual en BGR que permite al usuario seleccionar qué porcentaje pagar en millas vs plata.  
**Mínimos:**
- Vuelos: 2875 millas
- Otros productos: 20% del total en millas

### Solo Millas
Modelo de pago 100% en millas. En BGR, emite automáticamente sin intervención manual.

### Steps
Pasos del test case en formato: `Acción | Resultado esperado`  
**Regla crítica:** SIEMPRE deben iniciar desde login.

### suiteId
Identificador numérico del Test Suite en Azure DevOps. **Obligatorio** para crear test cases.  
Ejemplo: `121850`

---

## T

### Test Case
Caso de prueba completo que incluye: título, descripción, criterios, pasos, prioridad y campos de Azure DevOps.

### Test Plan
Contenedor organizacional en Azure DevOps que agrupa múltiples test suites.

### Test Suite
Agrupación lógica de test cases dentro de un test plan.

### testsWorkItemId
Campo opcional que vincula el test case con una HU específica en Azure DevOps para trazabilidad.

### Thrifty
Empresa de renta de autos disponible a través del proveedor Sabre.

### Trazabilidad
Capacidad de vincular un test case con su HU origen y seguir su ejecución.

---

## U

### Upsell
Popup o modal que presenta opciones de tarifas con diferentes beneficios (Basic, Plus, Premium). Permite al usuario seleccionar nivel de servicio.

---

## V

### Validación
Verificación que se realiza en cada paso del test case para confirmar el comportamiento esperado del sistema.

---

## Términos por Portal

### Solo PM
- Fee de procesamiento
- Lightbox
- Dispersión de fondos (SABRE EDIFACT)
- DerbySoft
- Emisión siempre automática

### Solo BGR
- Slider
- Millas + Plata
- Emisión manual/semiautomática
- Estado PENDIENTE → EMITIDA (proceso manual)
- OffLine (Disney)
- Mínimo slider: 2875 millas (vuelos), 20% (otros)

---

## Acrónimos Comunes

| Acrónimo | Significado |
|----------|-------------|
| E2E | End-to-End (Extremo a Extremo) |
| HU | Historia de Usuario (User Story) |
| PM | Pichincha Miles |
| BGR | BGR Miles |
| PPM | Programa Partners Miles |
| ADO | Azure DevOps |
| GDS | Global Distribution System |
| QA | Quality Assurance |
| ISTQB | International Software Testing Qualifications Board |
| MCP | Model Context Protocol |

---

**Última actualización:** 2026-01-05  
**Versión:** 1.0.0  
**Mantenido por:** QA Team Ultragroup
