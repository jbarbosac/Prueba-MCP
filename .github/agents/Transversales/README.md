# 🔄 Célula Transversales - Agentes QA

> Célula Transversales - Espacio para agregar agentes especializados de QA

---

## 📋 Modelos de la Célula Transversales

**Esta célula aún no tiene modelos configurados.**

Cuando agregues modelos, actualiza esta tabla:

| Modelo | Agente | Prefijo | País | URL | Estado |
|--------|--------|---------|------|-----|--------|
| [MODELO1] | [MODELO1]_QA_Assistant.agent.md | [PREFIX] | [PAÍS] | [URL] | ⏳ Pendiente |

---

## 🚀 Cómo Agregar un Modelo a Transversales

### **Paso 1: Crear el Agente**

```powershell
# Copiar template
Copy-Item .github/templates/portal-template.md .github/agents/Transversales/MODELO_QA_Assistant.agent.md
```

**Editar y completar:**
- Nombre del agente
- Prefijo del modelo (ej: [TRV1])
- URL del portal
- País
- Productos disponibles
- Modelo de negocio

### **Paso 2: Crear Reglas Comunes**

```powershell
# Crear archivo de reglas
New-Item .github/shared/Transversales/MODELO_COMMON_RULES.md
```

**Documentar:**
- ✅ Modelo de negocio
- ✅ Estructura de proveedores
- ✅ Validaciones comunes
- ✅ Estados de reserva
- ✅ Formato de título

### **Paso 3: Crear Productos**

```powershell
# Crear carpeta del modelo
New-Item -ItemType Directory .github/products/Transversales/MODELO/

# Copiar templates de productos
Copy-Item .github/templates/product-template.md .github/products/Transversales/MODELO/MODELO_VUELOS.md
Copy-Item .github/templates/product-template.md .github/products/Transversales/MODELO/MODELO_HOTELES.md
# ... etc para cada producto
```

### **Paso 4: Actualizar este README**

Agregar el modelo a la tabla de arriba con toda la información.

### **Paso 5: Actualizar QA_LEAD_Assistant**

El agente padre ya está preparado para incluir modelos de Transversales. Verifica que aparezca en:
```
.github/agents/QA_LEAD_Assistant.agent.md
```

---

## 📦 Estructura Esperada

```
Transversales/
├── agents/Transversales/
│   ├── README.md                          (este archivo)
│   ├── MODELO1_QA_Assistant.agent.md
│   ├── MODELO2_QA_Assistant.agent.md
│   └── ...
│
├── shared/Transversales/
│   ├── MODELO1_COMMON_RULES.md
│   ├── MODELO2_COMMON_RULES.md
│   └── ...
│
└── products/Transversales/
    ├── MODELO1/
    │   ├── MODELO1_PRODUCTO1.md
    │   ├── MODELO1_PRODUCTO2.md
    │   └── ...
    ├── MODELO2/
    └── ...
```

---

## 🔗 Recursos

- [Template de agente](../../templates/portal-template.md)
- [Template de producto](../../templates/product-template.md)
- [Reglas compartidas ISTQB](../../shared/SHARED_QA_RULES.md)
- [Documentación principal](../../README.md)
- [Ejemplo: Célula Kepler](../Kepler/README.md)

---

**Célula:** Transversales  
**Estado:** ⏳ Sin modelos configurados  
**Última actualización:** 2026-01-06  
**Mantenido por:** Equipo QA Transversales
