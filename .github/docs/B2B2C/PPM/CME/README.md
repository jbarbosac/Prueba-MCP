# � ClubMiles Ecuador (CME) - Modelo PPM con Copago

> Portal de lealtad con modelo flexible: Millas o Millas + Plata (Copago)

---

## 📋 Información General

| Campo | Valor |
|-------|-------|
| **Nombre Completo** | ClubMiles Ecuador (CME) |
| **Portal Test** | https://clubmiles-ec.developppm.com/ |
| **Portal Demo** | https://clubmiles-ec.preprodppm.com/ |
| **País** | Ecuador 🇪🇨 |
| **Modelo de Negocio** | B2B2C (Modelo de Lealtad) |
| **Plataforma** | PPM (Plataforma de Puntos y Millas) |
| **Célula** | Kepler |
| **Prefijo** | [CME] |
| **Cliente Final** | Diners Club |
| **Agente QA** | CME_QA_Assistant |

---

## 🏢 Cadena de Valor

```
UltraGroup (desarrollador)
    ↓
PPM (distribuidor)
    ↓
Diners Club (cliente)
    ↓
Socios (usuarios finales)
```

**Descripción:**
1. **UltraGroup** desarrolla CME
2. **PPM** compra y distribuye CME
3. **Diners Club** ofrece CME como programa de fidelización
4. **Socios** (clientes Diners) usan CME para canjear millas

---

## 💰 Modelo de Negocio

**Métodos de Pago:**
- **Solo Millas:** 100% del producto en millas (sin tarjeta, excepto fee vuelos)
- **Millas + Plata (Copago):** Slider ajustable en checkout (mínimo 20% millas) + USD vía PlacetoPay
- **Emisión:** Automática tipo "Cash" para ambos métodos

> 📖 **Detalles técnicos:** Ver [CME_COMMON_RULES.md](../../../../shared/Kepler/CME_COMMON_RULES.md)

---

## 📦 Productos Disponibles

**Catálogo:**
- 🛫 Vuelos (AGGREGATOR, SABRE, EDIFACT)
- 🏨 Hoteles (HotelBeds)
- 🚗 Autos (Sabre: Hertz, Dollar, Thrifty)
- 🎢 Actividades (HotelBeds)
- 🎠 Disney (Proveedor TBD)

**Características Comunes:**
- Slider ajustable en checkout (20%-100% millas)
- Pasarela PlacetoPay para copago
- Emisión automática tipo "Cash"
- Navegación sin login hasta Disponibilidad

> 📖 **Flujos E2E detallados:** Ver sección "Documentación de Referencia" abajo

---

## 📊 Matriz de Productos

**Características Especiales:**
- ✅ Login con OTP (portal PPM externo)
- ✅ Navegación sin login permitida hasta Disponibilidad
- ✅ Fee de vuelos dentro de checkout (NO lightbox)

| Producto | Proveedor | Slider | Fee | Pasarela | Emisión |
|----------|-----------|--------|-----|----------|---------|
| **Vuelos** | AGGREGATOR, SABRE, EDIFACT | ✅ 20%-100% | ✅ TC | PlacetoPay | Automática |
| **Hoteles** | HotelBeds | ✅ 20%-100% | ❌ No | PlacetoPay | Automática |
| **Autos** | Sabre | ✅ 20%-100% | ❌ No | PlacetoPay | Automática |
| **Actividades** | HotelBeds | ✅ 20%-100% | ❌ No | PlacetoPay | Automática |
| **Disney** | TBD | ✅ 20%-100% | ❌ No | PlacetoPay | Automática |

---

## 🎯 Diferencias Clave vs PM y BGR

| Aspecto | CME | PM | BGR |
|---------|-----|----|----|
| **Slider** | ✅ 20%-100% | ❌ No | ✅ Variable |
| **Copago** | ✅ Sí | ❌ No | ✅ Sí |
| **Fee Vuelos** | ✅ En checkout | ✅ Lightbox | ❌ No |
| **Pasarela** | PlacetoPay bash | Lightbox | Checkout |
| **Emisión** | Automática Cash | Automática | Auto/Manual |
| **Login** | Portal PPM + OTP | Portal PM | Portal BGR |
| **Navegación sin login** | ✅ Hasta Disponibilidad | ❌ No | ❌ No |

---

## 📚 Documentación de Referencia

**Reglas de Negocio:**
- [CME_COMMON_RULES.md](../../../shared/Kepler/CME_COMMON_RULES.md) - Reglas comunes CME

**Flujos por Producto:**
- [CME_VUELOS.md](../../../products/B2B2C/PPM/CME/CME_VUELOS.md) - Flujo E2E Vuelos
- [CME_HOTELES.md](../../../products/B2B2C/PPM/CME/CME_HOTELES.md) - Flujo E2E Hoteles
- [CME_AUTOS.md](../../../products/B2B2C/PPM/CME/CME_AUTOS.md) - Flujo E2E Autos
- [CME_ACTIVIDADES.md](../../../products/B2B2C/PPM/CME/CME_ACTIVIDADES.md) - Flujo E2E Actividades
- [CME_DISNEY.md](../../../products/B2B2C/PPM/CME/CME_DISNEY.md) - Flujo E2E Disney

**Agente QA:**
- [CME_QA_Assistant](../../../agents/CME_QA_Assistant.agent.md) - Agente especializado CME

---

## 📞 Contacto

**Agente QA:** CME_QA_Assistant  
**Ubicación:** `.github/agents/CME_QA_Assistant.agent.md`

**Para:**
- Crear casos de prueba CME
- Análisis de HU CME
- Consultas técnicas CME

---

**Última actualización:** 2026-01-20  
**Versión:** 2.0 (Optimizado - Sin duplicidad)  
**Estado:** ✅ Activo

