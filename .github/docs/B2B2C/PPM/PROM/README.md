# 🏆 Promerica Rewards - Modelo PPM

> Portal de redención Promerica Rewards - Célula Kepler

---

## 📋 Información General

| Campo | Valor |
|-------|-------|
| **Nombre Completo** | Promerica Rewards (PROM) |
| **Portal** | [PENDIENTE DEFINIR URL] |
| **País** | [PENDIENTE DEFINIR] |
| **Modelo de Negocio** | B2B2C |
| **Plataforma** | PPM (Plataforma de Puntos y Millas) |
| **Célula** | Kepler |
| **Prefijo** | [PROM] |
| **Agente QA** | PROM_QA_Assistant |
| **Estado** | 🔄 En configuración |

---

## 💰 Modelo de Negocio

⚠️ **PENDIENTE DE DEFINIR**

**Opciones posibles:**

### Opción A: Modelo Fijo (como Pichincha Miles)
```
Producto = 100% MILLAS
Fee (solo vuelos) = TARJETA DE CRÉDITO
Emisión = AUTOMÁTICA
```

### Opción B: Modelo Slider (como BGR Miles / Club Miles Ecuador)
```
Producto = MILLAS + PLATA (ajustable)
Mínimo = [DEFINIR: 20% o 2875 millas según producto]
Emisión = Condicional (automática 100% / manual mixto)
```

**🔍 ACCIÓN REQUERIDA:** Confirmar modelo de negocio específico de Promerica

---

## 📦 Productos Disponibles

| Producto | Estado | Proveedor | Archivo de Flujo |
|----------|--------|-----------|------------------|
| 🛫 **Vuelos** | 🔄 Pendiente | [Por definir] | [PROM_VUELOS.md](../../../products/B2B2C/PPM/PROM/PROM_VUELOS.md) |
| 🏨 **Hoteles** | 🔄 Pendiente | [Por definir] | [PROM_HOTELES.md](../../../products/B2B2C/PPM/PROM/PROM_HOTELES.md) |
| 🚗 **Autos** | 🔄 Pendiente | [Por definir] | [PROM_AUTOS.md](../../../products/B2B2C/PPM/PROM/PROM_AUTOS.md) |
| 🎢 **Actividades** | 🔄 Pendiente | [Por definir] | [PROM_ACTIVIDADES.md](../../../products/B2B2C/PPM/PROM/PROM_ACTIVIDADES.md) |
| 🎠 **Tickets Disney** | 🔄 Pendiente | [Por definir] | [PROM_DISNEY.md](../../../products/B2B2C/PPM/PROM/PROM_DISNEY.md) |

---

## 🔧 Tecnologías

⚠️ **PENDIENTE DE DEFINIR**

| Producto | Framework | Notas |
|----------|-----------|-------|
| Vuelos | [Por definir] | Angular, React, otro |
| Hoteles | [Por definir] | Angular, React, otro |
| Autos | [Por definir] | Meteor, otro |
| Actividades | [Por definir] | Angular, React, otro |
| Disney | [Por definir] | React, otro |

---

## 📚 Documentación

### **Reglas y Configuración:**
- [PROM_COMMON_RULES.md](../../../shared/Kepler/PROM_COMMON_RULES.md) - Reglas comunes del modelo

### **Agente QA:**
- [PROM_QA_Assistant.agent.md](../../../agents/PROM_QA_Assistant.agent.md) - Agente especializado

### **Flujos E2E por Producto:**
- [PROM_VUELOS.md](../../../products/B2B2C/PPM/PROM/PROM_VUELOS.md)
- [PROM_HOTELES.md](../../../products/B2B2C/PPM/PROM/PROM_HOTELES.md)
- [PROM_AUTOS.md](../../../products/B2B2C/PPM/PROM/PROM_AUTOS.md)
- [PROM_ACTIVIDADES.md](../../../products/B2B2C/PPM/PROM/PROM_ACTIVIDADES.md)
- [PROM_DISNEY.md](../../../products/B2B2C/PPM/PROM/PROM_DISNEY.md)

---

## 🚀 Próximos Pasos

### Fase 1: Definición (Actual)
- [ ] Confirmar URL del portal
- [ ] Definir país(es) de operación
- [ ] Definir modelo de negocio (fijo vs slider)
- [ ] Identificar proveedores por producto
- [ ] Definir tipo de emisión

### Fase 2: Documentación
- [ ] Completar PROM_COMMON_RULES.md con modelo definitivo
- [ ] Documentar flujos E2E de los 5 productos
- [ ] Validar navegación y pantallas del portal
- [ ] Definir validaciones críticas

### Fase 3: Configuración Técnica
- [ ] Configurar Azure DevOps (Area Path, Iteration)
- [ ] Validar acceso al portal de pruebas
- [ ] Crear usuarios de prueba
- [ ] Validar acceso al admin

### Fase 4: Pruebas Piloto
- [ ] Generar casos de prueba piloto con PROM_QA_Assistant
- [ ] Validar creación en Azure DevOps
- [ ] Ejecutar casos de prueba
- [ ] Ajustar documentación según resultados

---

## 📊 Estadísticas

| Métrica | Valor | Estado |
|---------|-------|--------|
| **Agente QA** | PROM_QA_Assistant | ✅ Creado |
| **Reglas comunes** | PROM_COMMON_RULES.md | ✅ Template creado |
| **Productos documentados** | 0/5 | 🔄 Pendiente |
| **Flujos E2E completos** | 0/5 | 🔄 Pendiente |
| **Casos de prueba creados** | 0 | ⏳ Sin crear |
| **Proveedores definidos** | 0/5 | 🔄 Pendiente |

---

## 🔄 Comparación con Otros Modelos de Kepler

⚠️ **Actualizar cuando se defina el modelo de Promerica**

| Aspecto | PM | BGR | CME | PROM |
|---------|----|----|-----|------|
| **Modelo** | 100% Millas | Slider | Slider | [DEFINIR] |
| **Fee** | Sí (vuelos) | No | Sí (vuelos) | [DEFINIR] |
| **Emisión** | Automática | Auto/Manual | Automática | [DEFINIR] |
| **Slider** | No | Sí | Sí | [DEFINIR] |
| **Mínimo** | N/A | 2875 millas vuelos, 20% otros | 20% todos | [DEFINIR] |

---

## 📞 Contacto y Soporte

**Célula Kepler:**
- **Líder TM:** Oscar Julian Buitrago Castro
- **Líder TL:** Fernando Zapata Montes
- **Equipo QA:** Jose Eulises Barbosa, Jesus Ernesto Marin, Jeferson Daniel Romero

**Para configuración de Promerica:**
- Contactar al equipo Kepler
- Revisar documentación de PM, BGR o CME como referencia según modelo definido

---

## 🔗 Enlaces Relacionados

- [Documentación Célula Kepler](../../../README.md)
- [Comparativa Modelos Kepler](../../../docs/comparisons/Kepler_Models_Comparison.md)
- [Guía Rápida: Agregar Modelo](../../../docs/QUICK_ADD_MODEL.md)

---

**Última actualización:** 2026-01-20  
**Versión:** 0.1 (Template inicial)  
**Estado:** 🔄 En configuración - Pendiente de información específica  
**Mantenido por:** Equipo QA Célula Kepler
