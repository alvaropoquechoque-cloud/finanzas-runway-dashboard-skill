# Finanzas Sommos — Runway Mensual

## Propósito

Documentar la lógica de proyección de caja y runway de Sommos.

Esta referencia pertenece a:

`finanzas-runway-dashboard`

La pestaña principal es:

`Runway Mensual`

---

# Pregunta que responde

Runway debe ayudar a responder:

**¿Cuánto tiempo puede operar Sommos antes de quedarse sin caja bajo distintos escenarios?**

No debe confundirse con una simple tabla de pendientes.

---

# Fuentes principales

La lógica actual utiliza principalmente:

- `Balance Sheet`
- `Cash Flow`
- `Real S&A`
- `Sueldos 2026`
- `CxC Mensual`
- `CxP Mensual`
- `CxP Sueldos`

Puede consultar adicionalmente:

- `Bancos`
- `Operative incomes`
- `Presupuesto`
- `Transacciones`

---

# Principio fundamental

El Runway es una vista derivada.

No debe convertirse en una fuente paralela de:

- cash;
- ingresos;
- gastos;
- CxC;
- CxP.

Si una cifra fuente es incorrecta:

corregir aguas arriba.

---

# Caja inicial

La caja inicial debe partir del último saldo financiero confiable.

Para histórico:

preferir caja respaldada por:

`Bancos`

y presentada en:

`Balance Sheet`

Para forecast:

utilizar la continuidad oficial del modelo.

No sumar cuentas por cobrar al cash disponible.

---

# Forecast 2026

Para los meses proyectados de 2026:

usar principalmente el forecast oficial de:

- `Cash Flow`
- `Balance Sheet`

No reconstruir el forecast únicamente desde transacciones pendientes.

Esto permite incorporar correctamente:

- devengos;
- cobros;
- pagos;
- CxC;
- CxP;
- sueldos;
- grants;
- financiamiento.

---

# Proyección 2027

Si el modelo de tres estados no llega con detalle completo a 2027:

utilizar una metodología explícita.

La metodología actual utiliza un:

`Core Burn`

para extender la proyección.

No asumir gasto cero porque no existan transacciones pendientes futuras.

---

# Core Burn

## Definición

Core Burn representa el costo operativo recurrente mensual necesario para mantener la operación.

Debe excluir, cuando corresponda:

- grants;
- financiamiento;
- transferencias internas;
- ingresos;
- gastos extraordinarios no recurrentes.

La composición vigente debe estar documentada.

---

# Base actual del Core Burn

La lógica actual utiliza principalmente:

`Real S&A`
+
`Sueldos 2026`

como base de costos recurrentes.

Puede utilizarse el promedio mensual anual 2026 cuando se extiende la proyección más allá del detalle disponible.

---

# Gastos extraordinarios

Antes de incluir una partida en el Core Burn revisar si es:

- recurrente;
- one-off;
- legal;
- viaje extraordinario;
- proyecto puntual;
- impuesto excepcional.

No eliminar automáticamente una partida porque sea grande.

No incluir automáticamente una partida porque haya ocurrido una vez.

---

# Runway sobre caja disponible

Fórmula conceptual:

`Runway Cash = Cash disponible / Core Burn mensual`

cuando:

`Core Burn > 0`

Este KPI no incluye necesariamente cobros futuros.

Debe interpretarse como una medición conservadora de supervivencia basada en caja actual.

---

# Runway según forecast

Debe considerar el escenario completo.

Puede expresarse mediante:

- meses hasta caja negativa;
- primer mes negativo;
- caja mínima;
- saldo final del horizonte.

Este runway sí incorpora:

- cobros futuros;
- grants;
- pagos;
- financiamiento;
- otros flujos incluidos en el escenario.

---

# No confundir tipos de runway

Siempre distinguir entre:

## Runway Cash

Cash actual / Core Burn.

## Runway Base

Runway según forecast oficial.

## Runway Sin Grants

Runway sin nuevos cobros de grants.

Pueden mostrar resultados muy distintos y todos ser correctos.

---

# Escenario Base

Debe utilizar:

- forecast oficial;
- grants en su calendario vigente;
- ingresos proyectados;
- gastos proyectados;
- financiamiento vigente.

No alterar supuestos silenciosamente.

---

# Escenario Sin Grants

Debe eliminar únicamente los cobros futuros de grants.

No debe modificar automáticamente:

- gastos;
- revenue;
- financiamiento;
- caja inicial.

Sirve para medir dependencia de grants.

---

# Escenario Grants +1 mes

Debe desplazar los grants un mes.

Mantener:

- mismo monto;
- mismo número de desembolsos;
- resto de supuestos constantes.

Este escenario mide riesgo de timing.

---

# Primer mes negativo

Debe identificar el primer periodo donde:

`Cash < 0`

Si no existe dentro del horizonte:

mostrar claramente que no hay cash-out dentro del periodo proyectado.

---

# Caja mínima

Mostrar:

- importe mínimo;
- mes correspondiente.

Una caja muy baja puede ser relevante aunque no llegue a ser negativa.

---

# Horizonte de análisis

Debe ser suficientemente largo para tomar decisiones.

Evitar horizontes tan cortos que oculten un cash-out inmediato posterior.

Evitar extender indefinidamente un burn constante como si fuera un forecast detallado.

---

# Grants

Los grants deben tratarse según:

- calendario;
- probabilidad/supuesto vigente;
- escenario.

No sumar grants futuros al cash actual.

---

# Financiamiento

El financiamiento solo debe entrar cuando forme parte explícita del escenario.

No asumir una ronda o préstamo futuro sin soporte.

---

# Ingresos futuros

Cuando exista forecast oficial:

utilizarlo.

No inventar crecimiento para mejorar runway.

---

# Pagos futuros

Cuando exista schedule oficial:

utilizarlo.

No ignorar CxP o nómina simplemente porque no estén en Transacciones como pendientes.

---

# Caja negativa

No sustituir caja negativa por cero.

El objetivo del Runway es mostrar el momento en que la empresa cruza ese umbral.

---

# Visualización

Runway debe ser fácil de leer.

Puede incluir:

- mes;
- caja base;
- caja sin grants;
- caja grants +1 mes;
- core burn;
- primer mes negativo;
- runway.

No sobrecargar con cálculos técnicos que no aporten a la decisión.

---

# Gráfico

El gráfico de escenarios debe:

- utilizar el mismo horizonte;
- utilizar la misma caja inicial;
- mostrar claramente Base, Sin grants y Grants +1 mes;
- mantener la misma unidad;
- permitir identificar el cruce por cero.

---

# Actualización

Después de modificar:

- Operative incomes;
- Real S&A;
- Sueldos;
- CxC;
- CxP;
- grants;
- financiamiento;

el Runway debe recalcular correctamente.

No hardcodear cifras para mantener un gráfico anterior.

---

# QA

Comprobar:

- caja inicial;
- core burn;
- escenario Base;
- Sin grants;
- Grants +1 mes;
- caja mínima;
- primer mes negativo;
- runway cash;
- continuidad mensual;
- ausencia de errores.

Buscar:

- `#REF!`
- `#VALUE!`
- `#N/A`
- `#DIV/0!`
- `#ERROR!`

---

# Guardrails

- No asumir burn cero.
- No sumar CxC al cash.
- No sumar grants futuros a cash actual.
- No inventar financiamiento.
- No inventar revenue.
- No usar pendientes bancarios como único forecast.
- No ocultar caja negativa.
- No llamar runway a una cifra sin explicar su definición.
- No modificar fuentes contables desde Runway para mejorar el resultado.

---

# Regla final

Runway debe mostrar la realidad de liquidez bajo supuestos claros.

No debe intentar producir una cifra tranquilizadora.
