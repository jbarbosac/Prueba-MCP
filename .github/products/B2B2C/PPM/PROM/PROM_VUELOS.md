# 🛫 FLUJO E2E OBLIGATORIO PARA VUELOS - PROMERICA REWARDS

**Portal:** [PENDIENTE DEFINIR URL]  
**Modelo de pago:** [PENDIENTE DEFINIR: 100% Millas o Slider Millas+Plata]  

---

## 📦 PROVEEDORES DISPONIBLES

⚠️ **PENDIENTE DE DEFINIR**

**Proveedores potenciales:**
- AGGREGATOR - NETACTICA
- AGGREGATOR - SABRE
- SABRE EDIFACT
- [Otros por confirmar]

---

## 📋 PASOS OBLIGATORIOS DEL FLUJO E2E

⚠️ **TEMPLATE PARA COMPLETAR**

**Siempre incluir estos pasos desde login para el flujo de Vuelos:**

1. Ingresar al portal [URL PENDIENTE] | El portal carga correctamente y muestra la pantalla de inicio
2. Realizar login con usuario y contraseña válidos | Login exitoso y acceso al home
3. [COMPLETAR SEGÚN NAVEGACIÓN ESPECÍFICA DE PROMERICA]
4. [BUSCAR VUELOS - DEFINIR CAMPOS ESPECÍFICOS]
5. [DISPONIBILIDAD - DEFINIR FILTROS Y OPCIONES]
6. [DETALLE - DEFINIR INFORMACIÓN MOSTRADA]
7. [CHECKOUT - DEFINIR CAMPOS Y VALIDACIONES]
8. [CONFIRMACIÓN - DEFINIR DATOS MOSTRADOS]
9. [ADMIN - DEFINIR VALIDACIONES DE EMISIÓN]

**🔍 ACCIÓN REQUERIDA:** Completar flujo específico según portal Promerica

---

## 🔄 VARIACIONES SEGÚN ESCENARIO

**Tipo de vuelo:**
- Solo ida
- Ida y vuelta
- Multi-destino (si aplica)

**Pasajeros:**
- 1 a N pasajeros
- Tipos: Adultos, Niños, Infantes (definir rangos de edad)

**Clase:**
- Económica
- Ejecutiva (si aplica)
- Primera clase (si aplica)

**Proveedor:**
- [Completar según proveedores definidos]

**Modelo de pago:**
- [Si es 100% Millas: Solo definir millas]
- [Si es Slider: Solo Millas vs Millas + Plata]

**Fee:**
- [Definir si aplica fee de procesamiento]
- [Definir cómo se paga: lightbox, formulario, etc.]

---

## ✅ VALIDACIONES CRÍTICAS

⚠️ **COMPLETAR SEGÚN MODELO DE NEGOCIO DEFINIDO**

### VALIDACIONES BÁSICAS:
✅ **Navegación:** [Definir ruta específica a vuelos]  
✅ **Campos obligatorios:** Origen, destino, fechas, pasajeros  
✅ **Botón buscar:** Habilitado solo con campos completos  
✅ **Disponibilidad:** Lista de vuelos con precios/millas  
✅ **Detalle:** Información completa del vuelo seleccionado  
✅ **Checkout:** Datos de pasajeros, contacto, pago  
✅ **Confirmación:** Código de reserva, resumen de pago  
✅ **Admin:** Reserva localizable con datos correctos  

### VALIDACIONES ESPECÍFICAS (según modelo):

**SI ES MODELO FIJO (100% Millas):**
✅ Validar cálculo de millas por vuelo  
✅ Validar fee si aplica (lightbox/formulario)  
✅ Validar emisión automática inmediata  

**SI ES MODELO SLIDER (Millas + Plata):**
✅ Validar visibilidad del slider en disponibilidad  
✅ Validar mínimo de millas (definir: ¿2875 o 20%?)  
✅ Validar cálculo: Millas + Plata = Total  
✅ Validar solicitud de tarjeta cuando hay copago  
✅ Validar emisión según tipo de pago  

---

## 📝 FORMATO DE TÍTULO

```
[PROM] Vuelos - [Tipo de vuelo] - [Proveedor] - [Clase] - [Pasajeros] - [Modelo de pago]
```

**Ejemplos (ajustar según modelo definido):**
- `[PROM] Vuelos - Ida y vuelta - SABRE - Económica - 1 adulto - Solo Millas automático`
- `[PROM] Vuelos - Solo ida - AGGREGATOR NETACTICA - Económica - 2 adultos 1 niño - Millas + Plata`
- `[PROM] Vuelos - Multi-destino - SABRE EDIFACT - Ejecutiva - 3 adultos - Solo Millas con fee`

---

## 🚀 PRÓXIMOS PASOS PARA COMPLETAR ESTE ARCHIVO

1. ✅ Definir URL del portal Promerica
2. ✅ Identificar proveedores de vuelos específicos
3. ✅ Documentar navegación completa paso a paso
4. ✅ Definir campos de búsqueda específicos
5. ✅ Documentar pantalla de disponibilidad
6. ✅ Documentar checkout y validaciones
7. ✅ Definir modelo de pago (fijo vs slider)
8. ✅ Documentar proceso de emisión
9. ✅ Agregar screenshots de referencia (opcional)
10. ✅ Realizar pruebas piloto del flujo

---

**Última actualización:** 2026-01-20  
**Versión:** 0.1 (Template)  
**Estado:** 🔄 Pendiente de completar información específica  
**Referencia:** Usar PM_VUELOS.md o BGR_VUELOS.md como guía según modelo definido
