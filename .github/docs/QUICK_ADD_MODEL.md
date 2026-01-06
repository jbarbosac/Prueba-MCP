# ➕ Guía Rápida: Agregar Nuevo Modelo

> Instrucciones paso a paso para agregar un modelo a cualquier célula

---

## 🎯 Prerrequisitos

- [ ] Determinar célula (Kepler, Pixel, Rocket, Skynet, Transversales)
- [ ] Definir prefijo del modelo (ej: [MOD])
- [ ] URL del portal (si aplica)
- [ ] País/región
- [ ] Lista de productos disponibles
- [ ] Modelo de negocio

---

## 📝 Pasos para Agregar Modelo

### **Paso 1: Crear Agente Especializado**

```powershell
# Copiar template
Copy-Item .github/templates/portal-template.md .github/agents/[CELULA]/[MODELO]_QA_Assistant.agent.md

# Ejemplo para Pixel:
Copy-Item .github/templates/portal-template.md .github/agents/Pixel/PIXMOD_QA_Assistant.agent.md
```

**Editar el archivo y reemplazar:**
- `{PREFIJO}` → [PIXMOD]
- `{PORTAL_NOMBRE}` → Nombre completo del portal
- `{PAIS}` → Ecuador, Perú, etc.
- `{URL_PORTAL}` → https://portal.example.com/
- `{MODELO_NEGOCIO}` → Descripción del modelo
- `{PRODUCTOS}` → Vuelos, Hoteles, etc.

### **Paso 2: Crear Reglas Comunes**

```powershell
# Crear archivo de reglas
New-Item .github/shared/[CELULA]/[MODELO]_COMMON_RULES.md -ItemType File

# Ejemplo:
New-Item .github/shared/Pixel/PIXMOD_COMMON_RULES.md -ItemType File
```

**Documentar en el archivo:**
```markdown
# REGLAS COMUNES [MODELO]

## Identificación
- Portal: [URL]
- País: [PAÍS]
- Prefijo: [PREFIX]

## Modelo de Negocio
[Descripción completa]

## Estructura de Proveedores
[Lista de proveedores por producto]

## Validaciones Comunes
[Validaciones específicas del modelo]

## Formato de Título
[PREFIX] [Producto] - [Escenario] - [Variante]
```

### **Paso 3: Crear Carpeta de Productos**

```powershell
# Crear carpeta del modelo
New-Item -ItemType Directory .github/products/[CELULA]/[MODELO]/

# Ejemplo:
New-Item -ItemType Directory .github/products/Pixel/PIXMOD/
```

### **Paso 4: Crear Documentos de Productos**

```powershell
# Por cada producto, copiar template
Copy-Item .github/templates/product-template.md .github/products/[CELULA]/[MODELO]/[MODELO]_VUELOS.md
Copy-Item .github/templates/product-template.md .github/products/[CELULA]/[MODELO]/[MODELO]_HOTELES.md
Copy-Item .github/templates/product-template.md .github/products/[CELULA]/[MODELO]/[MODELO]_AUTOS.md
# ... etc

# Ejemplo:
Copy-Item .github/templates/product-template.md .github/products/Pixel/PIXMOD/PIXMOD_VUELOS.md
```

**En cada archivo documentar:**
- Flujo E2E completo (login → checkout → confirmación)
- Validaciones específicas
- Variantes de escenarios
- Proveedores específicos

### **Paso 5: Actualizar README de la Célula**

Editar `.github/agents/[CELULA]/README.md` y agregar:

```markdown
| [MODELO] | [MODELO]_QA_Assistant.agent.md | [PREFIX] | [PAÍS] | [URL] | ✅ Activo |
```

### **Paso 6: Actualizar Referencias en el Agente**

Verificar que el agente tenga las rutas correctas:

```markdown
**REGLAS COMPARTIDAS:**
📋 [SHARED_QA_RULES.md](../../shared/SHARED_QA_RULES.md)
📋 [[MODELO]_COMMON_RULES.md](../../shared/[CELULA]/[MODELO]_COMMON_RULES.md)

**FLUJOS DETALLADOS POR PRODUCTO:**
🛫 [[MODELO]_VUELOS.md](../../products/[CELULA]/[MODELO]/[MODELO]_VUELOS.md)
🏨 [[MODELO]_HOTELES.md](../../products/[CELULA]/[MODELO]/[MODELO]_HOTELES.md)
# ... etc
```

### **Paso 7: Probar el Agente**

1. Selecciona el agente recién creado
2. Pide que cargue las reglas comunes
3. Pide que genere un caso de prueba simple
4. Verifica que las referencias funcionen correctamente

---

## ✅ Checklist Final

- [ ] Agente creado en `agents/[CELULA]/`
- [ ] Reglas comunes en `shared/[CELULA]/`
- [ ] Carpeta de productos en `products/[CELULA]/[MODELO]/`
- [ ] Al menos 1 producto documentado
- [ ] README de célula actualizado
- [ ] Referencias de rutas correctas
- [ ] Agente probado exitosamente

---

## 📦 Estructura Final Esperada

```
[CELULA]/
├── agents/[CELULA]/
│   ├── README.md                          (actualizado)
│   └── [MODELO]_QA_Assistant.agent.md    ← NUEVO
│
├── shared/[CELULA]/
│   └── [MODELO]_COMMON_RULES.md          ← NUEVO
│
└── products/[CELULA]/
    └── [MODELO]/                          ← NUEVO
        ├── [MODELO]_VUELOS.md
        ├── [MODELO]_HOTELES.md
        └── ...
```

---

## 🔄 Siguiente Paso: Alimentar Conocimiento

Una vez creada la estructura, alimenta cada archivo con:

1. **COMMON_RULES.md:**
   - Modelo de negocio específico
   - Proveedores por producto
   - Validaciones comunes
   - Estados de reserva
   - Proceso de emisión

2. **Archivos de Productos:**
   - Flujo E2E completo (15-30 pasos)
   - Inicio SIEMPRE desde login
   - Validaciones específicas por paso
   - Variantes de escenarios
   - Ejemplos de títulos de casos

3. **Agente:**
   - Identificación clara del alcance
   - Referencias a documentación
   - Reglas críticas específicas
   - Formato de título obligatorio

---

## 💡 Consejos

1. **Usa Kepler como referencia:** Es la única célula completa
2. **Documenta progresivamente:** Empieza con 1 producto bien documentado
3. **Prueba frecuentemente:** Verifica que el agente funciona antes de continuar
4. **Mantén consistencia:** Sigue los patrones de nombrado establecidos
5. **Actualiza el LEAD:** El agente padre ya está preparado, solo actualiza si necesario

---

**Última actualización:** 2026-01-06  
**Mantenido por:** Sistema QA Multi-Célula
