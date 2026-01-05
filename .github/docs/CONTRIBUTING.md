# 🤝 Guía de Contribución

> Cómo contribuir efectivamente al sistema de generación de test cases para PM y BGR.

---

## 📋 Tabla de Contenidos

- [Código de Conducta](#código-de-conducta)
- [Cómo Contribuir](#cómo-contribuir)
- [Agregar Nuevo Producto](#agregar-nuevo-producto)
- [Agregar Nuevo Portal](#agregar-nuevo-portal)
- [Actualizar Flujo Existente](#actualizar-flujo-existente)
- [Convenciones](#convenciones)
- [Proceso de Revisión](#proceso-de-revisión)

---

## 🔧 Operaciones con Azure DevOps

> **CRÍTICO:** Todas las operaciones de creación, actualización y gestión de test cases en Azure DevOps se realizan **exclusivamente mediante herramientas MCP** (Model Context Protocol).
>
> **Herramientas MCP disponibles:**
> - `mcp_microsoft_azu_testplan_create_test_case` → Crear test cases
> - `mcp_microsoft_azu_wit_update_work_item` → Actualizar campos HTML (Descriptions, Considerations)
> - `mcp_microsoft_azu_testplan_add_test_cases_to_suite` → Agregar casos a un suite
> - `mcp_microsoft_azu_wit_get_work_item` → Obtener información de HU/casos
>
> **No se requiere ni permite intervención manual** del usuario en la interfaz web de Azure DevOps para estas operaciones.

---

## 🤝 Código de Conducta

- ✅ Respetar las convenciones de nomenclatura establecidas
- ✅ Documentar todos los cambios en CHANGELOG.md
- ✅ Validar que no se rompen referencias entre archivos
- ✅ Mantener consistencia de formato en archivos Markdown
- ✅ Incluir metadata completa en nuevos archivos
- ✅ No duplicar información que ya existe en archivos compartidos

---

## 🚀 Cómo Contribuir

### 1. Identificar el tipo de contribución

| Tipo | Descripción | Template |
|------|-------------|----------|
| **Nuevo producto** | Agregar flujo E2E para producto nuevo en portal existente | `product-template.md` |
| **Nuevo portal** | Agregar portal completo (ej: PM Perú, BGR Colombia) | `portal-template.md` |
| **Actualización** | Modificar flujo E2E o reglas existentes | N/A |
| **Corrección** | Fix de bug o typo | N/A |
| **Documentación** | Mejorar docs sin cambiar funcionalidad | N/A |

### 2. Verificar que no exista

```powershell
# Buscar si ya existe
Get-ChildItem -Path ".github/products" -Filter "*PRODUCTO*" -Recurse
```

### 3. Usar template apropiado

Ver sección [Agregar Nuevo Producto](#agregar-nuevo-producto) o [Agregar Nuevo Portal](#agregar-nuevo-portal) según corresponda.

### 4. Documentar en CHANGELOG.md

```markdown
## [Unreleased]

### Added
- ✅ Nuevo flujo E2E para PM Seguros (30 pasos)
- ✅ Proveedor: AseguraTech
```

### 5. Validar cambios

```powershell
# Validar estructura (cuando esté disponible)
.\validation\validate-structure.ps1

# Verificar links rotos
.\validation\check-links.ps1
```

---

## ➕ Agregar Nuevo Producto

### Paso 1: Copiar template

```powershell
# Para PM
Copy-Item templates/product-template.md products/PM_NUEVO_PRODUCTO.md

# Para BGR
Copy-Item templates/product-template.md products/BGR_NUEVO_PRODUCTO.md
```

### Paso 2: Completar metadata YAML

```yaml
---
version: "1.0.0"
portal: "PM"  # o "BGR"
producto: "Nuevo Producto"
proveedor: "Nombre del proveedor"
tecnologia: "Angular"  # o "Meteor", "React"
ultima_actualizacion: "2026-01-05"
autor: "Tu Nombre"
estado: "activo"
---
```

### Paso 3: Documentar modelo de pago

**Para PM:**
```markdown
**Modelo de pago:** 100% Millas + Fee de procesamiento (si aplica tarjeta)
```

**Para BGR:**
```markdown
**Modelo de pago:** Millas (100%) o Millas + Plata (slider con mínimo 20%)
```

### Paso 4: Escribir pasos obligatorios

**Reglas:**
- ✅ Mínimo 15 pasos, idealmente 20-30
- ✅ Siempre iniciar desde login (paso 1)
- ✅ Formato: `N. Acción | Resultado esperado`
- ✅ Ser específico en acciones y validaciones
- ✅ Incluir validaciones de campos obligatorios
- ✅ Terminar en validación admin

**Estructura recomendada:**
1. Login (pasos 1-2)
2. Navegación (pasos 3-4)
3. Búsqueda (pasos 5-13)
4. Disponibilidad (pasos 14-16)
5. Checkout (pasos 17-23)
6. Confirmación (pasos 24-26)
7. Admin (pasos 27-30)

### Paso 5: Agregar validaciones críticas

```markdown
## ✅ VALIDACIONES CRÍTICAS

✅ **Integridad de datos:** [Descripción]
✅ **Campos obligatorios:** [Lista]
✅ **Cálculo de millas:** [Fórmula]
✅ **Proveedor:** [Validación específica]
✅ **[Validación específica del producto]**
```

### Paso 6: Definir variaciones

```markdown
## 🔄 VARIACIONES SEGÚN ESCENARIO

**[Característica 1]:**
- Opción A
- Opción B

**[Característica 2]:**
- Opción X
- Opción Y
```

### Paso 7: Formato de título

```markdown
## 📝 FORMATO DE TÍTULO

```
[PM/BGR] Nuevo Producto - [Escenario] - [Variante] - [Proveedor]
```

**Ejemplos:**
- `[PM] Nuevo Producto - Opción A - Característica X - ProveedorTech`
- `[BGR] Nuevo Producto - Opción B - Solo Millas automático`
```
```

### Paso 8: Actualizar agente

**En PM_QA_Assistant.agent.md o BGR_QA_Assistant.agent.md:**

```markdown
🎨 [PM_NUEVO_PRODUCTO.md](../products/PM_NUEVO_PRODUCTO.md) - Flujo E2E completo de Nuevo Producto
```

### Paso 9: Actualizar COMMON_RULES

**En PM_COMMON_RULES.md o BGR_COMMON_RULES.md:**

Agregar a la estructura de proveedores:

```markdown
├─ 🎨 NUEVO PRODUCTO [Angular]
│  └─ ProveedorTech
```

### Paso 10: Documentar en CHANGELOG

```markdown
## [Unreleased]

### Added
- ✅ Flujo E2E PM_NUEVO_PRODUCTO.md (30 pasos)
- ✅ Proveedor: ProveedorTech
- ✅ Tecnología: Angular
- ✅ Validaciones: [lista específicas]
```

---

## 🌍 Agregar Nuevo Portal

### Paso 1: Crear estructura base

```powershell
# Crear agente
Copy-Item templates/portal-template.md agents/NUEVO_PORTAL_QA_Assistant.agent.md

# Crear reglas comunes
New-Item -Path shared/NUEVO_PORTAL_COMMON_RULES.md -ItemType File

# Crear carpeta de productos (si se usa estructura jerárquica)
# New-Item -Path products/NUEVO_PORTAL/ -ItemType Directory
```

### Paso 2: Configurar agente

En `NUEVO_PORTAL_QA_Assistant.agent.md`:

```markdown
name: "qa-nuevo-portal-agent"
description: "Agente QA para Nuevo Portal [descripción]"

**ESTÁS EN MODO: NUEVO_PORTAL_QA_Assistant ([Nombre] - [País])**
**PREFIJO OBLIGATORIO: [NP]**

📍 **TU ALCANCE:**
- ✅ Portal: https://nuevoportal.ejemplo.com/
- ✅ País: [País]
- ✅ Productos: [Lista]
- ✅ Modelo: [Descripción]
- ✅ Prefijo: [NP]
```

### Paso 3: Documentar modelo de negocio

En `NUEVO_PORTAL_COMMON_RULES.md`:

```markdown
## 💰 MODELO DE NEGOCIO

### ECUACIÓN DE PAGO:
[Describir cómo funciona el pago]

### EMISIÓN:
[Describir proceso de emisión]

### ESTRUCTURA DE PROVEEDORES:
[Lista de proveedores por producto]
```

### Paso 4: Crear productos iniciales

Por cada producto esencial (mínimo Vuelos):

```powershell
Copy-Item templates/product-template.md products/NP_VUELOS.md
```

### Paso 5: Actualizar README principal

En `.github/README.md`:

```markdown
### **Nuevo Portal (NP)**
- **URL:** https://nuevoportal.ejemplo.com/
- **País:** [País]
- **Prefijo:** [NP]
- **Modelo:** [Descripción breve]
- **Emisión:** [Automática/Manual]
- **Agente:** `NUEVO_PORTAL_QA_Assistant.agent.md`
```

### Paso 6: Documentar en CHANGELOG

```markdown
## [2.0.0] - YYYY-MM-DD

### Added
- 🌍 Nuevo portal: Nuevo Portal ([País])
- ✅ Agente: NUEVO_PORTAL_QA_Assistant
- ✅ NUEVO_PORTAL_COMMON_RULES.md
- ✅ Flujo inicial: NP_VUELOS.md
- ✅ [Otros productos iniciales]
```

### Paso 7: Actualizar GLOSSARY

Agregar términos específicos del nuevo portal en `docs/GLOSSARY.md`.

### Paso 8: Documentar arquitectura

Agregar nueva ADR en `docs/ARCHITECTURE.md` explicando decisiones específicas del portal.

---

## 🔄 Actualizar Flujo Existente

### Paso 1: Identificar archivo

```powershell
# Buscar archivo
Get-ChildItem -Path ".github/products" -Filter "*PRODUCTO*"
```

### Paso 2: Editar archivo

Abrir `products/PM_PRODUCTO.md` o `BGR_PRODUCTO.md`

### Paso 3: Actualizar contenido

- ✅ Modificar pasos si cambió el flujo
- ✅ Agregar/quitar validaciones
- ✅ Actualizar variaciones

### Paso 4: Actualizar metadata

```yaml
---
version: "1.1.0"  # Incrementar versión
ultima_actualizacion: "2026-01-06"  # Fecha actual
---
```

### Paso 5: Documentar cambio

En `CHANGELOG.md`:

```markdown
## [1.1.0] - 2026-01-06

### Changed
- 🔧 PM_PRODUCTO: Actualizado paso 15 para incluir nueva validación X
- 🔧 PM_PRODUCTO: Agregada variación Y
```

### Paso 6: Validar impacto

Verificar si el cambio afecta:
- ¿COMMON_RULES del portal?
- ¿Otros productos similares?
- ¿Documentación relacionada?

---

## 📐 Convenciones

### Nomenclatura de archivos

| Tipo | Patrón | Ejemplo |
|------|--------|---------|
| Agente | `{PORTAL}_QA_Assistant.agent.md` | `PM_QA_Assistant.agent.md` |
| Common Rules | `{PORTAL}_COMMON_RULES.md` | `BGR_COMMON_RULES.md` |
| Producto | `{PORTAL}_{PRODUCTO}.md` | `PM_VUELOS.md` |
| Imagen | `{pantalla}-{producto}-{PORTAL}.png` | `Checkout-vuelos-PM.png` |

### Prefijos de título

| Portal | Prefijo | Ejemplo |
|--------|---------|---------|
| Pichincha Miles | [PM] | `[PM] Vuelos - Ida y vuelta` |
| BGR Miles | [BGR] | `[BGR] Hoteles - 3 noches` |
| Nuevo Portal | [NP] | `[NP] Producto - Escenario` |

### Formato de pasos

```markdown
N. [Verbo] en [elemento] | [Estado/resultado esperado]
```

**Ejemplos:**
- ✅ `1. Ingresar a la URL https://portal.com/ | Portal cargado correctamente`
- ✅ `5. Click en el botón Buscar | Se muestra disponibilidad`
- ❌ `1. Portal` (incompleto)
- ❌ `5. Buscar vuelos` (sin resultado esperado)

### Versionado

Seguir [Semantic Versioning](https://semver.org/):

- **MAJOR** (X.0.0): Cambios incompatibles, reestructuración completa
- **MINOR** (1.X.0): Nueva funcionalidad compatible (nuevo producto/portal)
- **PATCH** (1.0.X): Correcciones y mejoras menores

---

## 🔍 Proceso de Revisión

### Checklist antes de contribuir

- [ ] Metadata completa en archivo nuevo
- [ ] Formato de pasos correcto
- [ ] Inicio desde login
- [ ] Validaciones críticas documentadas
- [ ] Variaciones incluidas
- [ ] Formato de título definido
- [ ] Agente actualizado con referencia
- [ ] COMMON_RULES actualizado (si aplica)
- [ ] CHANGELOG.md documentado
- [ ] Links entre archivos verificados
- [ ] Sin duplicación innecesaria

### Validación automatizada (futuro)

```powershell
# Ejecutar todas las validaciones
.\validation\validate-all.ps1

# Validaciones específicas
.\validation\check-metadata.ps1     # Verifica metadata YAML
.\validation\check-links.ps1        # Verifica links rotos
.\validation\check-format.ps1       # Verifica formato de pasos
.\validation\check-duplicates.ps1   # Detecta duplicación
```

---

## 💡 Tips y Mejores Prácticas

### ✅ DO (Hacer)

- ✅ Ser específico en pasos y validaciones
- ✅ Incluir todas las validaciones críticas
- ✅ Usar emojis para categorizar secciones
- ✅ Mantener consistencia con archivos existentes
- ✅ Documentar decisiones importantes en ARCHITECTURE.md
- ✅ Actualizar GLOSSARY si introduces términos nuevos
- ✅ Validar antes de commit

### ❌ DON'T (Evitar)

- ❌ Iniciar flujos desde otra pantalla que no sea login
- ❌ Duplicar información que ya está en COMMON_RULES
- ❌ Usar formato inconsistente de pasos
- ❌ Omitir validaciones críticas
- ❌ Olvidar actualizar CHANGELOG
- ❌ Romper links entre archivos
- ❌ Crear archivos sin metadata

---

## 📞 Contacto

**Dudas o sugerencias:**
- QA Team Ultragroup
- Documentación: `.github/docs/`
- Changelog: `.github/CHANGELOG.md`

---

**Última actualización:** 2026-01-05  
**Versión:** 1.0.0  
**Mantenido por:** QA Team Ultragroup
