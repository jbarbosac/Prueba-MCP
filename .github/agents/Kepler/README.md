# 🚀 Célula Kepler - Agentes QA

> Agentes especializados para portales de redención de millas de la célula Kepler

---

## 📋 Modelos de la Célula

| Modelo | Agente | Prefijo | País | URL |
|--------|--------|---------|------|-----|
| **Pichincha Miles** | PM_QA_Assistant.agent.md | [PM] | Ecuador | pichinchamiles-ec.preprodppm.com |
| **BGR Miles** | BGR_QA_Assistant.agent.md | [BGR] | Ecuador | bgrmiles-ec.preprodppm.com |
| **Correos Millas Ecuador** | CME_QA_Assistant.agent.md | [CME] | Ecuador | [URL pendiente] |
| **Correos Millas Panamá** | CMP_QA_Assistant.agent.md | [CMP] | Panamá | [URL pendiente] |
| **Promerica Rewards** | PROM_QA_Assistant.agent.md | [PROM] | [País] | [URL pendiente] |

---

## 🎯 Cómo Usar los Agentes de Kepler

### **Para QA de Kepler (Ejecución Táctica)**

Selecciona el agente correspondiente al modelo que vas a probar:

```
Pichincha Miles → PM_QA_Assistant
BGR Miles → BGR_QA_Assistant
Correos Ecuador → CME_QA_Assistant
Correos Panamá → CMP_QA_Assistant
Promerica → PROM_QA_Assistant
```

**Ejemplo:**
```
"Genera un caso de vuelos para PM con SABRE ida y vuelta"
```

### **Para Lead de Kepler (Visión Estratégica)**

Usa el agente padre `QA_LEAD_Assistant` para:
- Comparar modelos dentro de Kepler
- Generar casos para múltiples modelos
- Análisis de cobertura consolidado

**Ejemplo:**
```
"Crea un caso de hoteles para todos los modelos de Kepler"
```

---

## 📦 Estructura de Archivos Kepler

```
Kepler/
├── agents/Kepler/
│   ├── PM_QA_Assistant.agent.md
│   ├── BGR_QA_Assistant.agent.md
│   ├── CME_QA_Assistant.agent.md
│   ├── CMP_QA_Assistant.agent.md
│   └── PROM_QA_Assistant.agent.md
│
├── shared/Kepler/
│   ├── PM_COMMON_RULES.md
│   ├── BGR_COMMON_RULES.md
│   ├── CME_COMMON_RULES.md
│   ├── CMP_COMMON_RULES.md
│   └── PROM_COMMON_RULES.md
│
└── products/Kepler/
    ├── PM/
    │   ├── PM_VUELOS.md
    │   ├── PM_HOTELES.md
    │   └── ...
    ├── BGR/
    │   ├── BGR_VUELOS.md
    │   └── ...
    ├── CME/
    ├── CMP/
    └── Promerica/
```

---

## 🔗 Recursos

- [Comparación de modelos Kepler](../../docs/comparisons/Kepler_Models_Comparison.md)
- [Reglas compartidas ISTQB](../../shared/SHARED_QA_RULES.md)
- [Documentación principal](../../README.md)

---

**Célula:** Kepler  
**Última actualización:** 2026-01-06  
**Mantenido por:** Equipo QA Kepler
