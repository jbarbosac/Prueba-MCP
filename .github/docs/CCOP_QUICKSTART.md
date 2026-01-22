# ⚡ INICIO RÁPIDO: Consolidación COP (CCOP)

Guía rápida de 5 minutos para comenzar con el nuevo modelo CCOP.

---

## 📋 LO QUE SE HA CREADO

✅ **5 documentos nuevos** listos para usar:

1. **CCOP_COMMON_RULES.md** - Reglas comunes del portal
2. **CCOP_QA_Assistant.agent.md** - Agente QA especializado
3. **CCOP_SETUP_GUIDE.md** - Guía completa de configuración (checklist 8 fases)
4. **CCOP_PRODUCT_TEMPLATE.md** - Template para documentar productos
5. **CCOP_README.md** - Resumen completo de todo lo creado

✅ **1 documento actualizado:**
- **Kepler_Models_Comparison.md** - Ahora incluye CCOP en la comparativa

---

## 🚀 EMPEZAR EN 3 PASOS

### **PASO 1: Revisar la estructura** (5 min)

Abre y lee brevemente:
- [CCOP_README.md](.github/docs/CCOP_README.md) - Para entender qué se creó

### **PASO 2: Planificar configuración** (30 min)

Abre y completa:
- [CCOP_SETUP_GUIDE.md](.github/docs/CCOP_SETUP_GUIDE.md)
- Marca con ✅ lo que YA conoces
- Marca con ⏳ lo que necesitas definir
- Asigna responsables

### **PASO 3: Completar información** (variable)

Edita:
- [CCOP_COMMON_RULES.md](.github/shared/Kepler/CCOP_COMMON_RULES.md)
- Reemplaza todos los `[A DEFINIR]` con datos reales
- Usa el modelo PM o BGR como referencia

---

## 📚 ORDEN RECOMENDADO DE LECTURA

1. **CCOP_README.md** ← EMPIEZA AQUÍ
2. **CCOP_SETUP_GUIDE.md** ← CHECKLIST COMPLETO
3. **CCOP_COMMON_RULES.md** ← REGLAS DEL PORTAL
4. **CCOP_QA_Assistant.agent.md** ← AGENTE QA
5. **CCOP_PRODUCT_TEMPLATE.md** ← PARA CREAR PRODUCTOS

---

## ⚙️ CONFIGURACIÓN MÍNIMA REQUERIDA

Antes de usar CCOP_QA_Assistant, DEBES definir:

- ✅ URL del portal
- ✅ Modelo de negocio (millas/puntos/efectivo/mixto)
- ✅ Tipo de emisión (automática/manual/semiautomática)
- ✅ Al menos 1 producto con su proveedor
- ✅ Azure DevOps (planId, 1 suiteId mínimo)

**Sin esto, el agente NO podrá crear casos de prueba.**

---

## 🤖 USAR EL AGENTE CCOP_QA_Assistant

Una vez configurado, puedes:

```
Usuario: "Crea un caso de [PRODUCTO] para CCOP"

CCOP_QA_Assistant:
1. Valida que es request para CCOP ✅
2. Lee CCOP_COMMON_RULES.md ✅
3. Lee CCOP_[PRODUCTO].md ✅
4. Confirma planId/suiteId
5. Genera caso de prueba
6. Crea en Azure DevOps vía MCP
7. Reporta resultado
```

---

## 🔗 ENLACES RÁPIDOS

**Documentos principales:**
- [CCOP_README.md](.github/docs/CCOP_README.md)
- [CCOP_SETUP_GUIDE.md](.github/docs/CCOP_SETUP_GUIDE.md)
- [CCOP_COMMON_RULES.md](.github/shared/Kepler/CCOP_COMMON_RULES.md)
- [CCOP_QA_Assistant.agent.md](.github/agents/CCOP_QA_Assistant.agent.md)
- [CCOP_PRODUCT_TEMPLATE.md](.github/templates/CCOP_PRODUCT_TEMPLATE.md)

**Comparativas:**
- [Kepler_Models_Comparison.md](.github/docs/comparisons/Kepler_Models_Comparison.md)

**Agentes:**
- QA_LEAD_Assistant (visión global)
- CCOP_QA_Assistant (especialista CCOP)

---

## 💡 PREGUNTAS FRECUENTES

**P: ¿Por dónde empiezo?**  
R: Lee [CCOP_README.md](.github/docs/CCOP_README.md) primero.

**P: ¿Qué necesito definir antes de crear casos?**  
R: Ve el checklist en [CCOP_SETUP_GUIDE.md](.github/docs/CCOP_SETUP_GUIDE.md).

**P: ¿Cómo documento un producto?**  
R: Copia [CCOP_PRODUCT_TEMPLATE.md](.github/templates/CCOP_PRODUCT_TEMPLATE.md) y complétalo.

**P: ¿Quién crea los casos de prueba?**  
R: CCOP_QA_Assistant (agente automático).

**P: ¿Cómo comparo CCOP con otros modelos?**  
R: Usa QA_LEAD_Assistant o lee [Kepler_Models_Comparison.md](.github/docs/comparisons/Kepler_Models_Comparison.md).

**P: ¿CCOP funciona ya?**  
R: No. Está en configuración inicial. Necesitas completar CCOP_COMMON_RULES.md primero.

---

## 📞 ¿NECESITAS AYUDA?

**Documentación:**
- Todo está en `.github/docs/` y `.github/shared/Kepler/`

**Agentes:**
- QA_LEAD_Assistant: Preguntas estratégicas, comparaciones
- CCOP_QA_Assistant: Creación de casos CCOP (cuando esté configurado)

**Equipo:**
- [Líder QA a definir]
- [PM/PO a definir]

---

**Creado:** 2026-01-22  
**Tiempo estimado setup completo:** 2-3 semanas  
**Tiempo mínimo para primeros casos:** 1 semana (con configuración mínima)

---

## 🎯 PRÓXIMO HITO

**Meta:** Crear el primer caso de prueba con CCOP_QA_Assistant

**Requisitos:**
1. ✅ CCOP_COMMON_RULES.md completo
2. ✅ Al menos 1 producto documentado
3. ✅ Azure DevOps configurado
4. ✅ Equipo capacitado

**¡Vamos!** 🚀
