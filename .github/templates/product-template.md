# 📄 Template - Nuevo Producto

> Plantilla base para agregar un nuevo flujo E2E de producto en PM o BGR

---

## ⚠️ INSTRUCCIONES DE USO

**ANTES DE EDITAR:**

1. **Copiar este archivo:**
   ```powershell
   # Para PM
   Copy-Item templates/product-template.md products/PM_NUEVO_PRODUCTO.md
   
   # Para BGR
   Copy-Item templates/product-template.md products/BGR_NUEVO_PRODUCTO.md
   ```

2. **Reemplazar placeholders:**
   - `{PORTAL}` → `PM` o `BGR`
   - `{PRODUCTO}` → Nombre del producto (Vuelos, Hoteles, etc.)
   - `{PROVEEDOR}` → Nombre del proveedor principal
   - `{TECNOLOGIA}` → Angular, Meteor o React
   - `{URL_PORTAL}` → URL del portal correspondiente
   - `{MODELO_PAGO}` → Descripción del modelo de pago

3. **Completar metadata YAML**

4. **Escribir flujo E2E completo** (mínimo 15-30 pasos)

5. **Validar checklist final**

---

## 📋 METADATA (Completar antes de editar)

```yaml
---
version: "1.0.0"
portal: "{PORTAL}"           # PM o BGR
producto: "{PRODUCTO}"       # Nombre del producto
proveedor: "{PROVEEDOR}"     # Proveedor principal
tecnologia: "{TECNOLOGIA}"   # Angular, Meteor o React
ultima_actualizacion: "YYYY-MM-DD"
autor: "Tu Nombre"
estado: "activo"            # activo, deprecado, borrador
---
```

---

# 🎨 FLUJO E2E OBLIGATORIO PARA {PRODUCTO} - {PORTAL}

**Proveedor:** {PORTAL} Ecuador  
**Portal:** {URL_PORTAL}  
**Tecnología:** {TECNOLOGIA}  
**Modelo de pago:** {MODELO_PAGO}  

---

## 📦 PROVEEDORES DISPONIBLES

**Proveedor:** {PROVEEDOR}  
**Otros proveedores (si aplica):** Lista aquí

**Notas específicas del proveedor:**
- Característica 1
- Característica 2
- Característica 3

---

## 📋 PASOS OBLIGATORIOS DEL FLUJO E2E

**IMPORTANTE:** Siempre incluir estos pasos desde login:

**PLANTILLA DE PASOS (Completar y expandir):**

1. Ingresar a la URL {URL_PORTAL} | Portal cargado correctamente
2. Realizar login con usuario y contraseña válidos | Login exitoso y acceso al home
3. Click en la opción {PRODUCTO} | Se muestra el formulario de búsqueda de {PRODUCTO}
4. [Paso específico del producto] | [Resultado esperado]
5. [Paso específico del producto] | [Resultado esperado]
6. [Continuar con más pasos...]
...
15. [Paso de disponibilidad/resultados] | Se muestran opciones disponibles
...
20. [Paso de checkout] | Campos obligatorios visibles
...
25. [Paso de confirmación] | Código de reserva visible
...
30. [Validación en admin] | Reserva emitida correctamente

**GUÍA DE ESTRUCTURA RECOMENDADA:**
- Pasos 1-2: Login
- Pasos 3-4: Navegación al producto
- Pasos 5-14: Formulario de búsqueda
- Pasos 15-17: Disponibilidad/resultados
- Pasos 18-23: Checkout
- Pasos 24-26: Confirmación
- Pasos 27-30: Validación admin

---

## 🔄 VARIACIONES SEGÚN ESCENARIO

**[Característica 1]:**
- Opción A
- Opción B
- Opción C

**[Característica 2]:**
- Escenario X
- Escenario Y
- Escenario Z

**[Característica 3]:**
- Variante 1
- Variante 2

**Notas sobre variaciones:**
[Explicar cómo impactan las variaciones en el flujo]

---

## ✅ VALIDACIONES CRÍTICAS

**COMPLETAR con validaciones específicas del producto:**

✅ **Integridad de datos:** [Describir qué debe ser consistente entre pantallas]  
✅ **Campos obligatorios:** [Lista de campos que DEBEN validarse]  
✅ **Cálculo de millas:** [Fórmula o regla de cálculo]  
✅ **Botones habilitados:** [Cuándo se habilitan botones críticos]  
✅ **Links funcionales:** [Qué links deben validarse]  
✅ **Estados de reserva:** [Estados esperados en admin]  
✅ **Proveedor:** [Validación específica del proveedor]  
✅ **[Validación específica 1]:** [Descripción]  
✅ **[Validación específica 2]:** [Descripción]  
✅ **[Validación específica 3]:** [Descripción]  

**Para PM específicamente:**
✅ **Fee de procesamiento:** [Si aplica]  
✅ **Lightbox:** [Si aplica]  
✅ **Dispersión:** [Si aplica con SABRE EDIFACT]  
✅ **Emisión automática:** Siempre inmediata  

**Para BGR específicamente:**
✅ **Slider funcional:** Validar mínimos (vuelos 2875, otros 20%)  
✅ **Millas + Plata:** Tarjeta solo si se selecciona pago mixto  
✅ **Emisión:** Automática (100% millas) / Manual (mixto)  
✅ **Admin - Solo Millas:** Estado EMITIDA automáticamente  
✅ **Admin - Millas + Plata:** Proceso manual (debitar → emitir cash)  

---

## 📝 FORMATO DE TÍTULO

```
[{PORTAL}] {PRODUCTO} - [Escenario] - [Variante] - [Característica especial]
```

**Ejemplos:**
- `[{PORTAL}] {PRODUCTO} - [Escenario A] - [Variante X] - {PROVEEDOR}`
- `[{PORTAL}] {PRODUCTO} - [Escenario B] - [Variante Y] - [Característica especial]`
- `[{PORTAL}] {PRODUCTO} - [Escenario C] - [Múltiples opciones]`

**Para PM:**
```
[PM] {PRODUCTO} - [Escenario] - [Variante] - {PROVEEDOR}
```

**Para BGR:**
```
[BGR] {PRODUCTO} - [Escenario] - [Modelo de pago] - {PROVEEDOR}
```

---

## 🖼️ RECURSOS VISUALES (Opcional)

**Si existen capturas de pantalla del flujo:**

Agregar a `.github/imagenes/{PORTAL}/{producto}/`:
- Home-{producto}-{PORTAL}.png
- Disponibilidad-{producto}-{PORTAL}.png
- Checkout-{producto}-{PORTAL}.png
- Confirmacion-{producto}-{PORTAL}.png
- Admin.png

**Referencias en Descriptions:**
```html
<strong>📸 Imágenes de referencia del flujo:</strong><br>
• Home-{producto}-{PORTAL}.png - Pantalla principal<br>
• Disponibilidad-{producto}-{PORTAL}.png - Resultados de búsqueda<br>
• Checkout-{producto}-{PORTAL}.png - Pantalla de checkout<br>
• Confirmacion-{producto}-{PORTAL}.png - Confirmación de reserva<br>
• Admin.png - Módulo administrativo<br>
```

---

## ⚙️ CONFIGURACIÓN TÉCNICA

**Tecnología:** {TECNOLOGIA}  
**Framework:** [Especificar si es Angular con TypeScript, Meteor con MongoDB, etc.]  
**Proveedor externo:** {PROVEEDOR}  
**API de integración:** [Si aplica]  
**Proceso de emisión:** [Automático/Manual/Mixto]  

---

## 📊 MATRIZ DE ESCENARIOS

| Escenario | Variante | Validaciones clave | Prioridad |
|-----------|----------|-------------------|-----------|
| [Escenario A] | [Variante X] | [Lista de validaciones] | Alta |
| [Escenario B] | [Variante Y] | [Lista de validaciones] | Media |
| [Escenario C] | [Variante Z] | [Lista de validaciones] | Baja |

---

## 🔗 REFERENCIAS

**Documentación relacionada:**
- [{PORTAL}_COMMON_RULES.md](../shared/{PORTAL}_COMMON_RULES.md) - Reglas comunes del portal
- [SHARED_QA_RULES.md](../shared/SHARED_QA_RULES.md) - Fundamentos ISTQB

**Documentación del proveedor:**
- [Link a documentación oficial del proveedor si está disponible]

---

## ✅ CHECKLIST FINAL (Verificar antes de commit)

- [ ] Metadata YAML completa
- [ ] Portal correcto (PM o BGR)
- [ ] Pasos E2E completos (mínimo 15-30)
- [ ] Inicio desde login (paso 1)
- [ ] Cada paso tiene resultado esperado
- [ ] Validaciones críticas documentadas
- [ ] Variaciones según escenario incluidas
- [ ] Formato de título definido
- [ ] Proveedor identificado
- [ ] Modelo de pago descrito
- [ ] Referencias a COMMON_RULES
- [ ] Imágenes agregadas (si aplica)
- [ ] CHANGELOG.md actualizado
- [ ] Agente actualizado con referencia a este archivo
- [ ] COMMON_RULES actualizado con nuevo producto
- [ ] Sin duplicación de información compartida

---

## 🚀 PRÓXIMOS PASOS

Después de completar este archivo:

1. **Actualizar agente:**
   ```markdown
   En {PORTAL}_QA_Assistant.agent.md agregar:
   🎨 [{PORTAL}_{PRODUCTO}.md](../products/{PORTAL}_{PRODUCTO}.md) - Flujo E2E completo de {PRODUCTO}
   ```

2. **Actualizar COMMON_RULES:**
   ```markdown
   En {PORTAL}_COMMON_RULES.md agregar a estructura de proveedores:
   ├─ 🎨 {PRODUCTO} [{TECNOLOGIA}]
   │  └─ {PROVEEDOR}
   ```

3. **Documentar en CHANGELOG:**
   ```markdown
   ## [Unreleased]
   ### Added
   - ✅ {PORTAL}_{PRODUCTO}.md (X pasos E2E)
   - ✅ Proveedor: {PROVEEDOR}
   - ✅ Tecnología: {TECNOLOGIA}
   ```

4. **Validar:**
   ```powershell
   .\validation\validate-structure.ps1
   ```

---

**Template versión:** 1.0.0  
**Fecha creación:** 2026-01-05  
**Mantenido por:** QA Team Ultragroup
