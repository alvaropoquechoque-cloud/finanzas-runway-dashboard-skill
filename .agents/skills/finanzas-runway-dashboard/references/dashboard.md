# Finanzas Sommos — Dashboard

## Propósito

Documentar la lógica del Dashboard ejecutivo de Sommos.

Esta referencia pertenece a:

`finanzas-runway-dashboard`

La pestaña principal es:

`Dashboard`

---

# Objetivo

El Dashboard debe permitir entender rápidamente:

- liquidez;
- runway;
- capital de trabajo;
- desempeño;
- forecast;
- riesgos;
- estado del cierre.

No debe reemplazar los estados financieros.

---

# Principio fundamental

Cada KPI debe tener:

- una fuente clara;
- un periodo claro;
- una definición clara.

No reconstruir lógica contable compleja dentro del Dashboard si ya existe una fuente oficial.

---

# Bloque Liquidez y Runway

Puede incluir:

- Cash disponible
- Core Burn
- Runway Cash
- Primer mes negativo

---

# Cash disponible

Fuente principal:

`Balance Sheet`

respaldada para histórico por:

`Bancos`

No sumar:

- CxC;
- grants futuros;
- financiamiento no recibido.

---

# Core Burn

Fuente:

`Runway Mensual`

La metodología subyacente debe provenir de:

- Real S&A;
- Sueldos 2026;

según la lógica vigente.

---

# Runway

Mostrar claramente qué definición se utiliza.

Preferir que la tarjeta principal identifique:

`Runway sobre caja disponible`

si utiliza:

`Cash / Core Burn`

---

# Primer mes negativo

Fuente:

`Runway Mensual`

Debe corresponder al escenario Base salvo que se etiquete otro escenario.

---

# Bloque Capital de Trabajo

Puede incluir:

- CxC clientes
- Grants por cobrar
- CxP proveedores
- CxP Sueldos
- Cobros próximos 30 días
- Pagos próximos 30 días

---

# CxC clientes

Fuente:

`CxC Mensual`

No usar directamente:

`Ingreso Pendiente en Transacciones`

como sustituto.

---

# Grants por cobrar

Fuente:

bloque de grants en:

`CxC Mensual`

Mantener separado de clientes operativos.

---

# CxP proveedores

Fuente:

`CxP Mensual`

---

# CxP Sueldos

Fuente:

`CxP Sueldos`

No duplicar dentro de CxP proveedores si se muestran ambos indicadores.

---

# Cobros próximos 30 días

Debe utilizar el calendario oficial de cobros.

Fuente principal:

- CxC Mensual;
- vencimientos/documentación relacionados.

Ventana:

`TODAY() → TODAY()+30`

No incluir derechos ya cobrados.

---

# Pagos próximos 30 días

Debe utilizar:

- CxP Mensual;
- CxP Sueldos;
- calendarios/vencimientos.

No duplicar obligaciones.

---

# Bloque Desempeño

Puede incluir:

- ingresos;
- EBITDA;
- resultado neto;
- Budget vs Actual.

---

# Ingresos

Fuente:

`Real P&L`

Utilizar el periodo cerrado correspondiente.

No utilizar cobros.

---

# EBITDA

Fuente:

`Real P&L`

No recalcular con una definición distinta.

---

# Resultado neto

Fuente:

`Real P&L`

No confundir con cambio neto de caja.

---

# Budget vs Actual

Fuente:

`Presupuesto`

y lógica de:

`finanzas-presupuesto-vs`

Debe comparar Budget contra P&L, no contra cash.

---

# Bloque Forecast y Alertas

Puede incluir:

- caja Dic-26;
- caja mínima;
- CxC vencida;
- CxP total;
- checks financieros;
- escenarios.

---

# Caja futura

Fuente:

`Runway Mensual`

No mantener otra proyección independiente dentro del Dashboard.

---

# CxC vencida

Debe representar saldo pendiente vencido.

No confundir vencido con incobrable.

---

# Checks

Mostrar de forma resumida:

- Modelo de 3 estados
- Cash Flow vs Balance Sheet

La lógica completa pertenece a:

`finanzas-estados-financieros`

---

# Cierre mensual

El Dashboard puede mostrar:

- Último mes cerrado
- Bancos cerrados
- Por categorizar
- Sin conciliar
- Estado cierre

La lógica completa pertenecerá a:

`finanzas-cierre-mensual`

---

# Estado cierre

Mostrar:

`✓ CERRADO`

solo cuando los criterios aplicables estén correctos.

Si no:

`⚠ REVISAR`

No usar únicamente color.

El texto debe ser autoexplicativo.

---

# Último mes cerrado

No depende simplemente del mes calendario.

Debe corresponder al último periodo completamente validado.

---

# Bancos cerrados

Mostrar:

`Bancos conciliados / Bancos activos`

No hardcodear permanentemente un denominador fijo.

---

# Por categorizar

Fuente:

`Transacciones`

Debe reflejar movimientos que requieren clasificación.

Para un cierre ideal:

`0`

---

# Sin conciliar

Fuente:

controles de conciliación.

No confundir con pagos pendientes.

Para un cierre ideal:

`0`

---

# Alertas

Una alerta puede activarse por:

- runway bajo;
- cash negativo;
- CxC vencida;
- pagos próximos elevados;
- check financiero fallando;
- bancos abiertos;
- movimientos por categorizar;
- movimientos sin conciliar.

---

# Colores

Usar colores para ayudar, no para ocultar lógica.

Preferir:

- morado para estructura;
- neutros para información;
- rojo/alerta para problemas;
- verde/OK cuando corresponda.

No depender exclusivamente del color.

---

# Densidad

No agregar demasiadas tarjetas.

El Dashboard debe responder preguntas, no replicar todas las pestañas.

Antes de añadir un KPI preguntar:

**¿qué decisión mejora esta métrica?**

---

# Periodo

Los KPIs de Actual deben utilizar un periodo consistente.

Preferir:

`último mes cerrado`

No mezclar agosto cerrado con septiembre parcial sin indicarlo.

---

# Forecast

Etiquetar claramente cualquier cifra proyectada.

No presentarla como cash real.

---

# Gráficos

Los gráficos deben:

- ser simples;
- tener unidades claras;
- representar datos ya validados;
- complementar, no reemplazar, KPIs.

---

# QA

Después de modificar Dashboard comprobar:

- fuentes;
- periodos;
- Cash;
- Core Burn;
- Runway;
- CxC;
- CxP;
- próximos 30 días;
- Revenue;
- EBITDA;
- Net Income;
- Budget;
- caja forecast;
- checks;
- cierre;
- gráfico.

Buscar errores de fórmula.

---

# Guardrails

- No hardcodear OK.
- No hardcodear CERRADO.
- No reconstruir estados financieros.
- No sumar CxC al cash.
- No usar cash como revenue.
- No mezclar Actual y Forecast sin etiqueta.
- No ocultar alertas.
- No usar KPIs duplicados sin propósito.

---

# Regla final

El Dashboard debe permitir entender el estado financiero de Sommos en segundos sin sacrificar la precisión del modelo.
