# 💼 CORPORATIVO USD - Agente QA

> Agente especializado para portal B2B corporativo de vuelos en USD

---

## 📋 IDENTIFICACIÓN DEL MODELO

| Aspecto | Detalle |
|---------|---------|
| **Nombre** | CORPORATIVO USD |
| **Tipo** | B2B (Business to Business) |
| **Agente** | [CORPORATIVO_USD_QA_Assistant](../../../agents/CORPORATIVO_USD_QA_Assistant.agent.md) |
| **Prefijo** | [CORP-USD] |
| **Moneda** | USD (Dólares) |
| **Cliente** | Empresas Corporativas |
| **URL** | [Pendiente definir] |
| **Célula** | [Pendiente asignar] |

---

## 🎯 CARACTERÍSTICAS DEL MODELO

### **Modelo de Negocio B2B**

CORPORATIVO USD es un portal especializado para clientes corporativos:

- ✅ **Cliente:** Empresas (no consumidores finales)
- ✅ **Usuario:** Empleados con credenciales corporativas
- ✅ **Moneda:** Todas las transacciones en USD
- ✅ **Producto:** SOLO Vuelos (especializado)
- ✅ **Facturación:** Empresarial (RUC/NIT/Tax ID)
- ✅ **Centro de Costos:** Obligatorio para trazabilidad
- ✅ **Aprobaciones:** [Pendiente definir]

### **Productos Disponibles**

| Producto | Estado | Documentación |
|----------|--------|---------------|
| **Vuelos** | ✅ DISPONIBLE | [CORPORATIVO_VUELOS.md](./CORPORATIVO_VUELOS.md) |
| Hoteles | ❌ NO DISPONIBLE | - |
| Autos | ❌ NO DISPONIBLE | - |
| Actividades | ❌ NO DISPONIBLE | - |
| Disney | ❌ NO DISPONIBLE | - |

**IMPORTANTE:** Este modelo está especializado SOLO en vuelos corporativos.

---

## 🎯 CÓMO USAR EL AGENTE

### **Para QA (Ejecución Táctica)**

Selecciona el agente **CORPORATIVO_USD_QA_Assistant** cuando necesites:

```
✅ Crear casos de prueba de vuelos corporativos
✅ Validar flujos E2E en USD
✅ Probar facturación empresarial
✅ Validar centro de costos
✅ Probar flujos de aprobación (si aplica)
```

**Ejemplo:**
```
"Genera un caso de vuelos corporativos ida y vuelta SABRE para 1 adulto"
```

### **Para Lead de QA (Visión Estratégica)**

Usa el agente padre `QA_LEAD_Assistant` para:
- Comparar CORPORATIVO USD con otros modelos (PM, BGR, etc.)
- Generar casos para múltiples portales
- Análisis de cobertura consolidado

**Ejemplo:**
```
"Compara el flujo de checkout entre CORPORATIVO USD y PM"
```

---

## 📚 DOCUMENTACIÓN DISPONIBLE

### **Documentación del Agente**

📋 [CORPORATIVO_USD_QA_Assistant.agent.md](../../../agents/CORPORATIVO_USD_QA_Assistant.agent.md)  
Configuración completa del agente QA especializado

### **Reglas y Validaciones**

📋 [CORPORATIVO_COMMON_RULES.md](../../../shared/Corporativo/CORPORATIVO_COMMON_RULES.md)  
Reglas comunes, modelo de negocio, validaciones estándar

### **Flujos Detallados por Producto**

🛫 [CORPORATIVO_VUELOS.md](./CORPORATIVO_VUELOS.md)  
Flujo End-to-End completo de Vuelos, escenarios, validaciones

### **Documentación Compartida**

📋 [SHARED_QA_RULES.md](../../../shared/SHARED_QA_RULES.md)  
Fundamentos ISTQB y Azure DevOps (compartido con todos los agentes)

📋 [AGENT_CONTEXT_VALIDATION.md](../../../shared/AGENT_CONTEXT_VALIDATION.md)  
Validación de contexto de agentes

---

## 🔧 CONFIGURACIÓN PENDIENTE

**Los siguientes aspectos requieren definición:**

- [ ] URL del portal corporativo
- [ ] Célula asignada (Kepler, Pixel, Rocket, Skynet, Transversales)
- [ ] Proveedores de vuelos específicos
- [ ] Tecnología frontend/backend
- [ ] Proceso de emisión (Automático/Manual)
- [ ] Métodos de pago corporativos disponibles
- [ ] Flujo de aprobación (si aplica)
- [ ] Políticas corporativas específicas
- [ ] Team Lead y Product Owner asignados

**Una vez definidos, actualizar:**
1. `CORPORATIVO_COMMON_RULES.md`
2. `CORPORATIVO_VUELOS.md`
3. `CORPORATIVO_USD_QA_Assistant.agent.md`

---

## 💡 DIFERENCIAS CON OTROS MODELOS

### **vs Modelos B2B2C (PM, BGR, CME, CMP, PROM)**

| Aspecto | CORPORATIVO USD | PM/BGR/CME/CMP/PROM |
|---------|----------------|---------------------|
| **Tipo** | B2B | B2B2C |
| **Cliente** | Empresas | Tarjetahabientes banco |
| **Moneda** | USD | Millas (+USD en BGR) |
| **Productos** | Solo Vuelos | 5 productos |
| **Facturación** | Empresarial | Personal |
| **Centro Costos** | Obligatorio | No aplica |
| **Aprobaciones** | Posible | No |

### **vs Modelos B2C (AVASA, VACACIONAL)**

| Aspecto | CORPORATIVO USD | AVASA/VACACIONAL |
|---------|----------------|------------------|
| **Tipo** | B2B | B2C |
| **Cliente** | Empresas | Consumidor final |
| **Autenticación** | Corporativa | Personal/Guest |
| **Facturación** | Empresarial | Personal |
| **Centro Costos** | Obligatorio | No |

---

## 🚀 INICIO RÁPIDO

### **Paso 1: Seleccionar Agente**

Abre el agente especializado:
```
.github/agents/CORPORATIVO_USD_QA_Assistant.agent.md
```

### **Paso 2: Cargar Documentación Base**

El agente cargará automáticamente:
- `CORPORATIVO_COMMON_RULES.md` (reglas comunes)
- `CORPORATIVO_VUELOS.md` (flujo de vuelos)
- `SHARED_QA_RULES.md` (fundamentos ISTQB)

### **Paso 3: Proporcionar Contexto Azure DevOps**

Necesitarás:
- `planId`: ID del Test Plan
- `suiteId`: ID del Test Suite
- `organization`: Organización Azure DevOps
- `project`: Proyecto Azure DevOps

### **Paso 4: Solicitar Creación de Caso**

Ejemplo:
```
"Crea un caso de vuelos ida y vuelta SABRE para 1 adulto corporativo
planId: 12345
suiteId: 67890"
```

### **Paso 5: Validar Resultado**

El agente:
1. Generará el caso con prefijo [CORP-USD]
2. Incluirá las 11 imágenes del flujo
3. Agregará criterios de aceptación
4. Creará pasos desde login hasta confirmación
5. Agregará el caso a la suite
6. Reportará el resultado con ID generado

---

## 📊 FORMATO DE TÍTULOS

**Estructura obligatoria:**
```
[CORP-USD] Vuelos - [Tipo] - [Proveedor] - [Config]
```

**Ejemplos:**
```
[CORP-USD] Vuelos - Ida y vuelta - SABRE - 1 adulto
[CORP-USD] Vuelos - Solo ida - NETACTICA - 2 adultos
[CORP-USD] Vuelos - Multidestino - Amadeus - 3 adultos
[CORP-USD] Vuelos - Ida y vuelta - SABRE - Clase ejecutiva
```

---

## ✅ CHECKLIST DE VALIDACIÓN

**Antes de dar OK a un caso de CORPORATIVO USD:**

- [ ] Prefijo correcto: `[CORP-USD]`
- [ ] Producto correcto: Solo `Vuelos`
- [ ] Formato de título válido
- [ ] Descriptions incluye 11 imágenes del flujo
- [ ] Considerations con criterios claros
- [ ] Pasos inician desde LOGIN corporativo
- [ ] Validación de centro de costos incluida
- [ ] Validación de facturación empresarial incluida
- [ ] Precios en USD validados
- [ ] Notificaciones corporativas validadas
- [ ] Prioridad definida (1-4)

---

## 📞 SOPORTE

**Para consultas técnicas:**
- Revisar documentación en esta carpeta
- Consultar con QA_LEAD_Assistant para comparaciones
- Contactar Product Owner [Pendiente definir]

**Para problemas con el agente:**
- Verificar que usas CORPORATIVO_USD_QA_Assistant
- Verificar contexto Azure DevOps
- Revisar logs de errores

---

**Última actualización:** 22 de enero de 2026  
**Versión:** 1.0  
**Estado:** Inicial - Pendiente configuración específica

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
