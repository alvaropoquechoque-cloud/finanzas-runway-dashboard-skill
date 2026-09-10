---
name: finanzas-runway-dashboard
description: Mantiene y audita el Runway Mensual y Dashboard ejecutivo de Sommos, integrando caja, core burn, escenarios, capital de trabajo, desempeño, próximos 30 días y controles de cierre del modelo financiero.
---

# Finanzas Sommos — Runway y Dashboard

## Propósito

Gestionar la capa ejecutiva y prospectiva del workflow financiero de Sommos.

Esta skill opera principalmente sobre:

- `Runway Mensual`
- `Dashboard`

Debe transformar el modelo financiero detallado en información útil para responder rápidamente:

1. ¿Cuánta caja tiene Sommos?
2. ¿Cuánto está quemando mensualmente?
3. ¿Cuánto runway queda?
4. ¿Cuándo podría volverse negativa la caja?
5. ¿Qué debemos cobrar próximamente?
6. ¿Qué debemos pagar próximamente?
7. ¿Cómo estamos rindiendo frente al presupuesto?
8. ¿El modelo financiero está correctamente cerrado?

Esta skill es principalmente:

- analítica;
- ejecutiva;
- prospectiva.

No debe convertirse en una nueva fuente contable.

---

# Archivo principal

Google Sheet:

`Finanzas Sommos — Workflow y Control`

Spreadsheet ID:

`1RXy19WZMPQePflFaFeIIHnh09BpJbwOnk6Wumw8bW4E`

URL:

`https://docs.google.com/spreadsheets/d/1RXy19WZMPQePflFaFeIIHnh09BpJbwOnk6Wumw8bW4E/edit`

---

# Pestañas principales

Esta skill opera principalmente:

- `Runway Mensual`
- `Dashboard`

Debe consultar según corresponda:

- `Bancos`
- `Balance Sheet`
- `Cash Flow`
- `Real P&L`
- `CxC Mensual`
- `CxP Mensual`
- `CxP Sueldos`
- `Operative incomes`
- `Real S&A`
- `Sueldos 2026`
- `Presupuesto`
- `Transacciones`

También puede consultar:

- `Config`
- `TC BCB`

---

# Principio fundamental

Runway y Dashboard son:

**vistas derivadas**

No son fuentes originales del modelo.

Si una cifra del Dashboard parece incorrecta:

no corregir primero el Dashboard.

Identificar la fuente correcta aguas arriba.

Ejemplos:

Cash incorrecto
→ revisar Bancos / Balance Sheet

Revenue incorrecto
→ revisar Real P&L / Operative incomes

CxC incorrecta
→ revisar CxC Mensual

CxP incorrecta
→ revisar CxP Mensual / CxP Sueldos

Runway incorrecto
→ revisar Cash, core burn y escenario

---

# Arquitectura actual

La arquitectura ejecutiva es:

`Bancos`
→ cash histórico conciliado

`Real P&L`
→ desempeño económico

`CxC Mensual`
→ cuentas por cobrar

`CxP Mensual`
+
`CxP Sueldos`
→ obligaciones por pagar

`Balance Sheet`
+
`Cash Flow`
→ forecast financiero oficial

`Real S&A`
+
`Sueldos 2026`
→ core burn

`Presupuesto`
→ Budget vs Actual

Todo lo anterior alimenta:

`Runway Mensual`
→ `Dashboard`

---

# No reconstruir el modelo dentro del Dashboard

El Dashboard debe consumir resultados de fuentes ya validadas.

No replicar grandes fórmulas contables dentro del Dashboard si existe una fuente oficial.

Preferir:

`Dashboard → Real P&L`

en lugar de volver a reconstruir Revenue desde Operative incomes.

Preferir:

`Dashboard → Balance Sheet`

para caja de cierre cuando corresponda.

Preferir:

`Dashboard → CxC/CxP`

para capital de trabajo.

Esto reduce:

- duplicación;
- divergencias;
- mantenimiento;
- riesgo de errores.

---

# Runway Mensual

## Propósito

`Runway Mensual` proyecta la evolución de caja y permite evaluar escenarios de liquidez.

Debe distinguir claramente:

- caja real;
- forecast oficial;
- core burn;
- escenarios;
- runway sobre caja actual;
- runway proyectado.

---

# Referencia histórica

El Runway del Control antiguo contenía conceptos útiles que deben conservarse conceptualmente:

- Cash
- Net Change
- Grants
- Financing
- Core Burn
- sensibilidades por retraso de grants

El modelo nuevo mejora esta lógica utilizando los estados financieros ya construidos.

---

# Caja actual

La caja actual debe provenir del último cierre financiero confiable.

Prioridad conceptual:

`Bancos conciliados`
→ histórico

y:

`Balance Sheet`
→ posición financiera oficial del cierre

No sumar:

- CxC;
- grants futuros;
- financiamiento no recibido;

al cash disponible actual.

---

# Forecast 2026

Para meses futuros de 2026:

`Runway Mensual`

debe utilizar principalmente el forecast oficial ya contenido en:

- `Cash Flow`
- `Balance Sheet`

No reconstruir Sep–Dic únicamente desde filas `Pendiente` de `Transacciones`.

La razón es que los estados financieros ya incorporan:

- devengos;
- CxC;
- CxP;
- sueldos;
- grants;
- financiamiento;
- capital de trabajo.

---

# Proyección posterior a 2026

Cuando el modelo de tres estados no contenga forecast completo para 2027:

utilizar una metodología explícita y conservadora.

La metodología actual utiliza un:

`Core Burn`

construido principalmente desde:

- `Sueldos 2026`
- `Real S&A`

como base recurrente.

Actualmente puede utilizarse el promedio mensual anual 2026 de esas fuentes para extender el escenario base de 2027.

No asumir:

`Burn 2027 = 0`

simplemente porque no existan transacciones pendientes cargadas.

---

# Core Burn

## Definición

Core Burn representa el costo mensual recurrente necesario para mantener la operación.

Debe distinguirse de:

- gastos extraordinarios;
- grants;
- financiamiento;
- transferencias internas;
- movimientos puramente contables;
- cash no recurrente.

La metodología vigente debe estar documentada.

---

# Fuente de Core Burn

La base actual utiliza principalmente:

`Real S&A`
+
`Sueldos 2026`

No utilizar como única fuente:

`Transacciones Pagadas`

porque eso convierte el burn en una medición de timing bancario y no necesariamente de costo operativo recurrente.

---

# Gastos extraordinarios

Antes de incluir un gasto grande dentro del Core Burn revisar si es:

- recurrente;
- one-off;
- cierre legal;
- viaje extraordinario;
- impuesto excepcional;
- proyecto específico.

No inflar artificialmente el burn recurrente con un gasto que no se repetirá.

Si la metodología viva ya incluye determinado gasto:

preservarla hasta realizar un cambio explícito.

---

# Runway sobre caja disponible

Debe distinguirse explícitamente de otros conceptos.

Fórmula conceptual:

`Runway Cash = Cash disponible / Core Burn mensual`

si:

`Core Burn > 0`

Este KPI responde:

**¿cuántos meses podría operar Sommos si dependiera únicamente de la caja actual y del core burn?**

No incorpora necesariamente:

- cobros futuros;
- grants;
- financiamiento.

---

# Runway según forecast

También puede existir una lectura basada en la proyección completa.

Este indicador debe considerar:

- cash inicial;
- ingresos/cobros proyectados;
- pagos;
- grants;
- financiamiento;
- core burn;
- resto de flujos del escenario.

Una forma útil de expresarlo es mediante:

- primer mes de caja negativa;
- caja mínima;
- meses hasta cash-out.

No confundirlo con:

`Cash / Core Burn`

---

# Escenario Base

El escenario Base debe representar:

- forecast oficial disponible;
- calendario actual de grants;
- ingresos previstos;
- costos previstos;
- financiamiento considerado en el modelo.

No modificar supuestos silenciosamente.

---

# Escenario Sin grants

Debe permitir evaluar la dependencia de grants.

Conceptualmente:

`Escenario Sin Grants = Base - cobros futuros de grants`

manteniendo iguales los demás supuestos salvo que exista una razón explícita para modificarlos.

Este escenario ayuda a responder:

**¿cuánto runway tiene Sommos sin depender de nuevos grants?**

---

# Escenario Grants +1 mes

Debe desplazar los cobros futuros de grants un mes hacia adelante.

No eliminar el grant.

No modificar su importe.

Debe mostrar el impacto de:

`timing`

sobre la liquidez.

---

# Escenarios adicionales

No crear escenarios nuevos sin una pregunta de negocio clara.

Posibles escenarios futuros podrían incluir:

- revenue downside;
- hiring freeze;
- nuevo financiamiento;
- reducción de gastos.

Pero deben mantenerse separados y documentados.

---

# Primer mes de caja negativa

Este indicador debe identificar:

el primer periodo en que:

`Cash proyectado < 0`

Si no ocurre dentro del horizonte:

indicar claramente que no existe cash-out dentro del periodo proyectado.

No devolver un mes inventado.

---

# Caja mínima

Debe mostrar:

- importe mínimo proyectado;
- periodo en que ocurre.

Es una métrica importante incluso si la caja no llega a ser negativa.

---

# Saldo inicial de escenarios

Todos los escenarios comparables deben partir de la misma caja actual validada, salvo que la definición del escenario cambie explícitamente el punto inicial.

---

# Horizonte

Mantener un horizonte suficientemente útil para planificación.

Actualmente el Runway puede extenderse aproximadamente 12 meses o hacia 2027.

No proyectar indefinidamente con supuestos constantes sin advertirlo.

---

# Dashboard

## Propósito

El Dashboard debe permitir entender el estado financiero de Sommos en pocos segundos.

No debe convertirse en una réplica de todas las pestañas.

Debe priorizar:

- liquidez;
- capital de trabajo;
- desempeño;
- forecast;
- riesgos;
- estado del cierre.

---

# Bloques ejecutivos

La estructura actual se organiza conceptualmente en cuatro bloques principales:

## Liquidez y Runway

Puede incluir:

- Cash disponible
- Core Burn
- Runway Cash
- primer mes negativo

## Capital de trabajo

Puede incluir:

- CxC clientes
- Grants por cobrar
- CxP proveedores
- CxP Sueldos

## Desempeño

Puede incluir:

- ingresos
- EBITDA
- resultado neto
- Budget vs Actual

## Forecast y Alertas

Puede incluir:

- caja Dic-26
- caja mínima
- vencidos
- obligaciones próximas
- checks del modelo

---

# Cash disponible

La fuente debe ser la caja oficial del modelo.

Para último periodo cerrado:

preferir el resultado reconciliado con:

`Bancos`

y presentado en:

`Balance Sheet`

No sumar cuentas por cobrar al cash.

---

# CxC clientes

Fuente:

`CxC Mensual`

No calcular CxC simplemente como:

`Ingreso Pendiente en Transacciones`

La CxC oficial incorpora:

- devengo;
- cobros;
- roll-forward.

---

# Grants por cobrar

Fuente:

bloque correspondiente de:

`CxC Mensual`

Mantener separado de CxC clientes cuando el Dashboard así lo presenta.

---

# CxP proveedores

Fuente:

`CxP Mensual`

No utilizar únicamente egresos pendientes de `Transacciones`.

---

# CxP Sueldos

Fuente:

`CxP Sueldos`

No duplicar dentro de CxP proveedores si el Dashboard muestra ambas métricas separadamente.

---

# Cobros próximos 30 días

Debe calcularse desde el calendario financiero oficial.

Fuentes principales:

- `CxC Mensual`
- calendario/vencimientos relacionados

Debe representar derechos de cobro esperados en:

`hoy → hoy + 30 días`

No depender exclusivamente de filas pendientes de Transacciones.

---

# Pagos próximos 30 días

Debe incorporar según corresponda:

- `CxP Mensual`
- `CxP Sueldos`

y sus vencimientos/calendarios.

Debe representar obligaciones esperadas en:

`hoy → hoy + 30 días`

No contar dos veces una obligación presente en más de una vista.

---

# Aging / vencidos

Cuando se muestre CxC vencida:

debe representar saldo pendiente cuyo vencimiento ya pasó.

No confundir:

- vencido;
- incobrable.

Una CxC vencida continúa siendo un activo mientras siga vigente.

---

# Revenue

Para lectura ejecutiva:

usar principalmente:

`Real P&L`

No reconstruir revenue desde cobros de banco.

---

# EBITDA

Fuente:

`Real P&L`

Preservar la definición contable vigente.

No recalcular EBITDA con una fórmula distinta dentro del Dashboard.

---

# Resultado neto

Fuente:

`Real P&L`

No utilizar flujo de caja neto como resultado neto.

---

# Budget vs Actual

Fuente:

`Presupuesto`

y/o `Real P&L`

según la fórmula viva.

La comparación debe preservar la lógica:

`Budget vs Real P&L`

No Budget vs cash.

---

# Forecast de caja

La principal fuente debe ser:

`Runway Mensual`

que, a su vez, consume:

- Cash Flow;
- Balance Sheet;
- escenarios.

El Dashboard no debe mantener una segunda proyección independiente.

---

# Gráfico de escenarios

El Dashboard puede mostrar un gráfico de:

- Base
- Sin grants
- Grants +1 mes

El gráfico debe:

- compartir mismo horizonte;
- compartir mismo saldo inicial;
- utilizar las mismas unidades;
- mostrar claramente cuándo la caja cruza cero.

No utilizar escalas engañosas.

---

# Cierre mensual

El Dashboard contiene un bloque resumido de cierre.

Puede mostrar:

- Último mes cerrado
- Bancos cerrados
- Por categorizar
- Sin conciliar
- Estado cierre

Este bloque es una vista ejecutiva.

La lógica completa de cierre pertenecerá a:

`finanzas-cierre-mensual`

---

# Último mes cerrado

Debe representar el último periodo que cumple todos los controles requeridos.

No avanzar este indicador únicamente porque cambió el calendario.

Un nuevo mes solo se considera cerrado cuando haya sido validado.

---

# Bancos cerrados

Debe mostrar conceptualmente:

`Bancos conciliados / Bancos activos`

No hardcodear permanentemente:

`5/5`

si cambia la cantidad de cuentas activas.

---

# Por categorizar

Debe contar movimientos que aún requieren clasificación según la estructura viva.

Fuente principal:

`Transacciones`

y/o estado equivalente del workflow.

La expectativa para cierre es:

`0`

---

# Sin conciliar

Debe contar movimientos bancarios que aún requieran conciliación.

No confundir con:

- Pendiente de pago;
- CxP;
- CxC.

La expectativa para un periodo cerrado es:

`0`

---

# Checks de tres estados

El Dashboard debe mostrar de manera ejecutiva el resultado de:

- Modelo de 3 estados
- Cash Flow vs Balance Sheet

La lógica completa pertenece a:

`finanzas-estados-financieros`

No reconstruir estos checks de manera diferente dentro del Dashboard.

---

# Estado cierre

Puede mostrarse como:

`✓ CERRADO`

solo cuando todos los criterios aplicables estén correctos.

Si existe cualquier check requerido fallando:

mostrar:

`⚠ REVISAR`

No ocultar alertas mediante formato.

El texto debe ser autoexplicativo aun sin color.

---

# Regla importante sobre OK

Nunca hardcodear:

`OK`

`CERRADO`

o:

`✓`

si el valor puede calcularse desde controles reales.

Un indicador debe poder fallar cuando algo está mal.

---

# Alertas

Las alertas deben utilizarse para priorizar atención.

Ejemplos:

- cash negativo;
- runway bajo;
- CxC vencida alta;
- pagos próximos superiores a cobros;
- check financiero fallando;
- banco sin cerrar;
- movimientos sin categorizar.

No utilizar rojo para diferencias pequeñas sin materialidad.

---

# Interpretación de liquidez

No presentar un único runway como si fuera una verdad absoluta.

Distinguir:

## Runway Cash

Caja disponible / Core Burn.

## Runway Forecast

Tiempo hasta caja negativa bajo escenario Base.

## Runway Sin Grants

Liquidez sin nuevos grants.

Estas métricas responden preguntas diferentes.

---

# Cobros vs pagos próximos 30 días

Comparar:

`Cobros próximos 30d`

vs:

`Pagos próximos 30d`

ayuda a detectar presión de liquidez inmediata.

No concluir automáticamente que:

`Pagos > Cobros`

significa insolvencia.

También deben considerarse:

- cash actual;
- grants;
- financiamiento;
- otros flujos.

---

# Current vs Forecast

Todo KPI debe dejar claro si representa:

- actual;
- último cierre;
- forecast;
- escenario.

No mezclar valores de distinto carácter sin etiquetarlos.

---

# Periodo del Dashboard

Los KPIs de desempeño deben usar un periodo consistente.

Preferir:

`último mes cerrado`

para Actual.

No utilizar un mes parcialmente cargado como si fuera cierre completo.

---

# Formato visual

El Dashboard debe ser ejecutivo y limpio.

Preservar:

- lenguaje visual Sommos;
- jerarquía clara;
- tarjetas KPI;
- pocos colores;
- alertas comprensibles;
- números legibles;
- unidades visibles;
- gráficos simples.

Evitar agregar demasiados KPIs.

El Dashboard debe responder rápidamente las preguntas principales, no mostrar todo el modelo.

---

# Regla de densidad

Antes de agregar un nuevo KPI preguntar:

**¿qué decisión permite tomar esta métrica que no permiten las actuales?**

Si no existe una respuesta clara:

no añadirlo.

---

# Precisión

Dashboard y Runway pueden redondear visualmente.

Las fuentes subyacentes deben mantener precisión.

No modificar valores fuente para mejorar la apariencia de una tarjeta.

---

# Auditoría de KPI inesperado

Si un KPI parece incorrecto:

1. identificar la fórmula;
2. identificar la fuente;
3. comprobar periodo;
4. comprobar si es Actual/Forecast;
5. revisar la fuente aguas arriba;
6. revisar signos;
7. revisar exclusiones;
8. comprobar duplicados;
9. comprobar checks relacionados.

Corregir la fuente correcta.

No hardcodear el KPI.

---

# Auditoría de Runway inesperado

Si el runway cambia significativamente:

revisar:

1. Cash actual;
2. Core Burn;
3. periodo utilizado;
4. Real S&A;
5. Sueldos 2026;
6. forecast del Cash Flow;
7. grants;
8. financiamiento;
9. escenario;
10. gastos extraordinarios.

No atribuir automáticamente el cambio a cash.

---

# Mes parcialmente cerrado

Si el periodo actual todavía no está cerrado:

el Dashboard debe distinguirlo del último periodo cerrado.

No actualizar automáticamente:

`Último mes cerrado`

solo porque existan datos parciales del siguiente mes.

---

# Relación con Presupuesto

El Dashboard puede mostrar variación contra Budget.

La lógica detallada debe venir de:

`finanzas-presupuesto-vs`

No reconstruir Budget vs Actual usando cash.

---

# Relación con Estados Financieros

El Dashboard consume:

- P&L;
- Balance Sheet;
- Cash Flow;
- checks.

No modifica sus fórmulas salvo que el usuario solicite una corrección de fuente y se utilice la skill correspondiente.

---

# Relación con CxC/CxP

El Dashboard consume los schedules oficiales.

No reconstruir capital de trabajo desde pendientes de `Transacciones` si existe una vista reconciliada de CxC/CxP.

---

# Relación con Bancos

Cash histórico debe estar respaldado por bancos conciliados.

Si el Dashboard muestra cash diferente al Balance/Bancos:

investigar.

No escoger arbitrariamente uno de los valores.

---

# QA antes de modificar Runway

- [ ] Leí fórmulas actuales.
- [ ] Identifiqué caja inicial.
- [ ] Identifiqué frontera histórico/forecast.
- [ ] Revisé Core Burn.
- [ ] Revisé grants.
- [ ] Revisé Cash Flow.
- [ ] Revisé Balance Sheet.
- [ ] Revisé escenarios.
- [ ] Confirmé horizonte.

---

# QA después de modificar Runway

Comprobar:

- caja inicial;
- escenario Base;
- Sin grants;
- Grants +1 mes;
- core burn;
- caja mínima;
- primer mes negativo;
- runway cash;
- continuidad mensual;
- gráfico del Dashboard.

---

# QA antes de modificar Dashboard

- [ ] Identifiqué fuente de cada KPI.
- [ ] Identifiqué periodo.
- [ ] Confirmé Actual vs Forecast.
- [ ] Revisé checks.
- [ ] Revisé cierre mensual.
- [ ] Evité duplicar lógica existente.

---

# QA después de modificar Dashboard

Comprobar:

- Cash;
- Core Burn;
- Runway;
- primer mes negativo;
- CxC;
- CxP;
- CxP Sueldos;
- próximos 30 días;
- ingresos;
- EBITDA;
- resultado neto;
- Budget vs Actual;
- caja forecast;
- checks;
- estado de cierre;
- gráfico.

Buscar:

- `#REF!`
- `#VALUE!`
- `#N/A`
- `#DIV/0!`
- `#ERROR!`

---

# Guardrails

- No reconstruir CxC/CxP únicamente desde Transacciones.
- No usar cash como revenue.
- No usar pagos como gasto devengado.
- No asumir burn cero porque no existan pendientes.
- No sumar CxC al cash.
- No sumar grants futuros al cash actual.
- No usar Budget como cash forecast histórico.
- No hardcodear OK/CERRADO.
- No esconder checks fallidos.
- No modificar estados financieros desde Dashboard para mejorar KPIs.
- No crear escenarios sin documentar sus supuestos.
- No eliminar gastos extraordinarios del burn sin revisar metodología.
- No declarar runway sin explicar qué definición se está usando.
- No modificar históricos cerrados silenciosamente.
- No reportar como terminado sin releer el archivo vivo.

---

# Regla de finalización

Una modificación de Runway/Dashboard solamente está terminada cuando:

- fuentes correctas;
- periodos correctos;
- escenarios correctos;
- KPIs correctos;
- checks financieros correctos;
- cierre mensual correctamente representado;
- fórmulas releídas;
- ausencia de errores.

---

# Coordinación con otras skills

## `finanzas-config-categorizacion`

Usar para:

- categorías;
- taxonomía.

## `finanzas-transacciones-tc`

Usar para:

- movimientos;
- cash realizado;
- TC;
- categorización transaccional.

## `finanzas-devengo-operativo`

Usar para:

- Operative incomes;
- Real S&A;
- Sueldos 2026;
- base operativa del core burn.

## `finanzas-cxc-cxp`

Usar para:

- CxC;
- CxP;
- CxP Sueldos;
- vencimientos;
- próximos cobros/pagos.

## `finanzas-bancos-conciliacion`

Usar para:

- cash histórico;
- bancos cerrados;
- conciliación.

## `finanzas-estados-financieros`

Usar para:

- Real P&L;
- Balance Sheet;
- Cash Flow;
- checks de tres estados.

## `finanzas-presupuesto-vs`

Usar para:

- Budget vs Actual;
- variaciones.

## `finanzas-cierre-mensual`

Cuando exista, usar para:

- criterios completos de cierre;
- determinar formalmente si un mes puede considerarse `✓ CERRADO`.

---

# Referencias

Consultar cuando corresponda:

- `references/runway.md`
- `references/dashboard.md`
- `references/interpretacion.md`

---

# Alcance final

Esta skill debe transformar el modelo financiero en una respuesta clara a:

**¿Dónde estamos hoy?**

**¿Qué pasa con la caja si seguimos así?**

**¿Qué entra y qué sale próximamente?**

**¿Qué riesgos debemos mirar?**

**¿Podemos confiar en los números que estamos viendo?**

Runway y Dashboard deben servir para tomar decisiones, no solamente para visualizar cifras.
