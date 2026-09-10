# Finanzas Sommos — Interpretación ejecutiva

## Propósito

Definir cómo interpretar y comunicar los KPIs de:

- Runway Mensual
- Dashboard

Esta referencia pertenece a:

`finanzas-runway-dashboard`

Su objetivo es evitar conclusiones incorrectas a partir de métricas aisladas.

---

# Cash

Cash representa dinero disponible o equivalente según la metodología del modelo.

No incluye automáticamente:

- CxC;
- grants futuros;
- presupuesto;
- revenue devengado;
- financiamiento no recibido.

---

# Cash bajo no implica automáticamente insolvencia

Debe analizarse junto con:

- cobros próximos;
- pagos próximos;
- grants;
- financiamiento;
- runway;
- obligaciones.

---

# Runway Cash

`Cash / Core Burn`

Responde:

**¿cuántos meses cubre la caja actual si mantenemos este burn y no consideramos nuevas entradas?**

Es una métrica conservadora.

---

# Runway Forecast

Responde:

**¿cuándo cruza cero la caja bajo el escenario completo?**

Incluye:

- ingresos;
- cobros;
- pagos;
- grants;
- financiamiento;
- otros flujos del forecast.

---

# Por qué dos runways pueden diferir

Es completamente posible que:

`Runway Cash = 0.5 meses`

pero:

`Runway Forecast > 0.5 meses`

si existen cobros previstos.

No es una contradicción.

Son preguntas diferentes.

---

# Core Burn

Debe interpretarse como costo recurrente de operación.

No necesariamente coincide con:

- total de egresos bancarios;
- total de P&L;
- net cash burn.

---

# Net Burn

Cuando se use:

debe definirse claramente.

Puede significar:

`Cash outflows - cash inflows`

u otra metodología.

No utilizar el término “burn” sin indicar qué cálculo representa.

---

# CxC

CxC representa dinero que Sommos tiene derecho a cobrar.

No es cash.

Una CxC elevada puede ser:

- normal;
- señal de crecimiento;
- riesgo de cobranza;
- problema de timing.

Debe analizarse con aging.

---

# CxC vencida

Una CxC vencida merece atención porque el cobro no ocurrió en la fecha esperada.

Pero:

`vencido ≠ incobrable`

No provisionar o dar de baja automáticamente desde el Dashboard.

---

# CxP

CxP representa obligaciones pendientes.

No es equivalente al gasto del mes.

Una CxP alta puede reflejar:

- timing de pagos;
- acumulación operativa;
- retrasos;
- proveedores importantes.

---

# CxP Sueldos

Debe tratarse con especial atención por su prioridad operativa.

No mezclarla conceptualmente con proveedores ordinarios cuando el Dashboard la separa.

---

# Cobros próximos 30 días

Indica cash esperado de corto plazo.

No debe interpretarse como cash garantizado.

Analizar:

- vencimiento;
- calidad del deudor;
- historial;
- grants;
- riesgo de retraso.

---

# Pagos próximos 30 días

Representa presión de liquidez inmediata.

Debe compararse contra:

- cash actual;
- cobros próximos;
- financiamiento;
- reservas.

---

# Cobros vs pagos próximos

Si:

`Pagos próximos > Cobros próximos`

existe presión neta de caja.

Pero el análisis debe considerar también:

`Cash actual`

No concluir insolvencia solo por esa comparación.

---

# Revenue

Revenue del Dashboard viene de P&L.

No significa necesariamente cash recibido.

---

# EBITDA

Sirve para evaluar desempeño operativo según la definición del modelo.

Un EBITDA negativo no significa automáticamente que la caja cayó en el mismo importe.

Capital de trabajo y financiamiento pueden modificar cash.

---

# Resultado neto

Incluye más elementos que EBITDA.

Puede verse afectado por:

- resultado financiero;
- FX;
- impuestos;
- otras partidas.

---

# Budget vs Actual

Una desviación debe interpretarse según tipo de cuenta.

## Ingreso

Actual > Budget
→ generalmente favorable.

## Gasto

Actual > Budget
→ generalmente desfavorable.

No usar signo positivo/negativo sin contexto.

---

# Caja mínima

Muestra el punto de mayor tensión dentro del horizonte.

Es útil incluso si nunca cruza cero.

---

# Primer mes negativo

Es una señal de planificación.

No significa necesariamente que el evento vaya a ocurrir exactamente ese día.

Depende de los supuestos del escenario.

---

# Escenario Sin Grants

Mide dependencia de financiamiento no dilutivo/grants.

Una caída fuerte frente al Base indica alta dependencia de esos desembolsos.

---

# Escenario Grants +1 mes

Mide sensibilidad al timing.

Puede ser especialmente relevante cuando el runway es corto.

---

# Escenarios no son predicciones

Un escenario representa:

**qué ocurre si estos supuestos se cumplen**

No:

**qué ocurrirá con certeza**

Siempre comunicar la diferencia.

---

# Cierre mensual

`✓ CERRADO`

debe interpretarse como:

- datos bancarios conciliados;
- categorización completa;
- modelo financiero consistente;
- checks correctos;

según los criterios de cierre vigentes.

No significa que no pueda existir una corrección posterior con nueva evidencia.

---

# Checks del modelo

`OK`

significa que las relaciones financieras están dentro de tolerancia.

No significa que toda clasificación económica sea necesariamente perfecta.

Los checks matemáticos son necesarios, pero no sustituyen juicio contable.

---

# Alertas

Una alerta debe provocar investigación, no una corrección automática.

Ejemplo:

`CxC vencida alta`

→ revisar cuentas.

No:

→ eliminar la CxC.

---

# Materialidad

Priorizar por:

- impacto USD;
- impacto en runway;
- repetición;
- probabilidad;
- urgencia.

No enfocarse excesivamente en centavos.

---

# Histórico vs Forecast

Siempre indicar si una cifra es:

- histórica;
- actual;
- forecast;
- escenario.

Una cifra futura no debe presentarse con el mismo nivel de certeza que un saldo bancario conciliado.

---

# Comunicación ejecutiva

Una buena lectura del Dashboard debería poder resumirse en cuatro partes:

1. Liquidez actual
2. Riesgos próximos
3. Desempeño económico
4. Qué requiere acción

---

# Ejemplo conceptual

Una interpretación útil sería:

`Cash actual bajo y runway cash corto. Los pagos próximos 30 días superan los cobros próximos, y el escenario sin grants deteriora significativamente la caja. Prioridad: cobranza, timing de grants y control de burn.`

No afirmar causalidad sin haber revisado las fuentes.

---

# Evitar alarmismo

Un KPI rojo no significa automáticamente crisis.

Debe contextualizarse con:

- tendencia;
- calendario;
- financiamiento;
- calidad de CxC;
- flexibilidad de gasto.

---

# Evitar complacencia

Un Dashboard con checks verdes tampoco implica que la liquidez sea saludable.

Un modelo puede estar matemáticamente perfecto y mostrar un runway muy corto.

---

# Regla final

Interpretar Dashboard y Runway requiere separar:

**exactitud del modelo**

de:

**salud financiera de la empresa**

Son dos preguntas distintas.
