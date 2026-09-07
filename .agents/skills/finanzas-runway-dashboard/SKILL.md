---
name: finanzas-runway-dashboard
description: Calcula y audita cash, burn, runway, proyección mensual y KPIs ejecutivos del modelo financiero de Sommos.
---

# Finanzas Sommos — Runway y Dashboard

## Propósito

Analizar la posición financiera y la proyección de caja de Sommos usando como fuente principal el Google Sheet:

- Spreadsheet ID: `1RXy19WZMPQePflFaFeIIHnh09BpJbwOnk6Wumw8bW4E`
- URL: `https://docs.google.com/spreadsheets/d/1RXy19WZMPQePflFaFeIIHnh09BpJbwOnk6Wumw8bW4E/edit`

Esta skill es principalmente analítica.

No crear, duplicar ni modificar transacciones salvo que el usuario lo solicite expresamente y la operación haya sido validada.

## Pestañas principales

Opera principalmente sobre:

- `Runway Mensual`
- `Dashboard`

Puede consultar:

- `Transacciones`
- `Bancos`
- `CxC Mensual`
- `CxP Mensual`
- `Operative incomes`
- `Real S&A`
- `Presupuesto`
- `Sueldos 2026`
- `CxP Sueldos`

## Fuente de verdad

`Transacciones` es la fuente de verdad operativa.

Las vistas mensuales y ejecutivas no deben convertirse en fuentes paralelas de movimientos.

En particular:

- `CxC Mensual` es una vista de control de cuentas por cobrar.
- `CxP Mensual` es una vista de control de cuentas por pagar.
- `Operative incomes` es una vista mensual de ingresos.
- `Real S&A` es una vista mensual de gastos administrativos y comerciales.
- `CxP Sueldos` controla pasivos y pagos relacionados con nómina.
- `Bancos` representa caja real y conciliada.

Si una vista contradice `Transacciones`, investigar la diferencia antes de modificar datos.

## Arquitectura actual

Las antiguas pestañas `CxC` y `CxP` fueron eliminadas.

Por lo tanto:

- `Runway Mensual` debe obtener cobros esperados directamente desde `Transacciones`.
- `Runway Mensual` debe obtener pagos comprometidos directamente desde `Transacciones`.
- `Dashboard` debe obtener CxC pendiente, CxP pendiente y vencimientos directamente desde `Transacciones`.

No recrear dependencia con las antiguas pestañas `CxC` o `CxP`.

## Runway Mensual

La pestaña `Runway Mensual` proyecta la posición mensual de caja.

Conceptos principales:

- Mes
- Saldo inicial USD
- Cobros esperados CxC
- Otros ingresos USD
- Pagos comprometidos CxP
- Otros egresos USD
- Flujo neto USD
- Saldo final USD
- Burn proyectado USD
- Burn histórico promedio
- Runway meses
- Comentario

## Saldo inicial

Para el primer mes proyectado:

- usar el último cierre bancario real y conciliado disponible.

Para meses posteriores:

`Saldo inicial mes N = Saldo final proyectado mes N-1`

No sustituir saldos bancarios reales por proyecciones cuando ya existe un cierre conciliado.

## Cobros esperados CxC

Fuente:

`Transacciones`

Condiciones conceptuales:

- Tipo = `Ingreso`
- Estado pago = `Pendiente`
- Fecha vencimiento dentro del mes proyectado

La fecha de vencimiento determina el mes esperado de cobro.

No tratar como CxC:

- grants aprobados pero todavía no exigibles;
- compromisos sin obligación de pago definida;
- ingresos ya cobrados.

## Pagos comprometidos CxP

Fuente:

`Transacciones`

Condiciones conceptuales:

- Tipo = `Egreso`
- Estado pago = `Pendiente`
- Fecha vencimiento dentro del mes proyectado

No incluir como pago futuro un movimiento que ya se encuentre `Pagado/Cobrado`.

## Realizado versus pendiente

`Pagado/Cobrado` representa movimiento realizado.

`Pendiente` representa obligación o derecho todavía no realizado.

Por lo tanto:

- CxC no es cash.
- CxP no es egreso realizado.
- Un pendiente no debe afectar directamente la caja bancaria.
- Un movimiento realizado no debe permanecer simultáneamente como obligación pendiente.

## Burn histórico

El burn histórico debe calcularse utilizando movimientos reales:

- Tipo = `Egreso`
- Estado pago = `Pagado/Cobrado`
- excluir `Transferencias internas`

Usar hasta tres meses reales anteriores cuando exista suficiente información.

No utilizar directamente:

- presupuesto;
- CxP pendiente;
- saldo proyectado;
- transferencias internas.

## Runway

Fórmula conceptual:

`Runway = Saldo disponible / Burn histórico promedio`

cuando:

`Burn histórico promedio > 0`

El runway debe interpretarse como una aproximación.

Siempre distinguir entre:

- runway basado en cash actual;
- runway proyectado con CxC/CxP;
- runway basado en supuestos futuros.

## Dashboard

El `Dashboard` resume KPIs ejecutivos.

KPIs principales conocidos:

- Cash disponible
- CxC pendiente
- CxP pendiente
- Ingresos último mes con datos
- Burn último mes con datos
- Runway
- CxC vencida
- Presupuesto disponible

## Cash disponible

Debe provenir de bancos/cuentas conciliadas.

No sumar CxC pendiente al cash.

No usar saldos proyectados como saldo bancario real.

## CxC pendiente

Calcular desde `Transacciones` considerando:

- Tipo = `Ingreso`
- Estado pago = `Pendiente`

## CxP pendiente

Calcular desde `Transacciones` considerando:

- Tipo = `Egreso`
- Estado pago = `Pendiente`

Los pasivos de nómina pueden requerir consulta adicional a `CxP Sueldos` cuando se preparen estados financieros, pero no deben duplicarse si ya existen en `Transacciones`.

## CxC vencida

Debe considerar:

- Tipo = `Ingreso`
- Estado pago = `Pendiente`
- Fecha vencimiento anterior a la fecha actual

Una cuenta vencida sigue siendo CxC; no es pérdida automáticamente.

## Ingresos

Para análisis ejecutivo distinguir:

### Ingresos operativos

Consultar principalmente:

- `Operative incomes`
- `Transacciones`

### Grants y financiamiento

No confundir grants con ingresos operativos recurrentes.

La categoría:

`Other financing cash flow`

debe analizarse separadamente cuando corresponda.

## Gastos

Para análisis de gastos consultar:

- `Transacciones`
- `Real S&A`
- `Sueldos 2026`
- `CxP Sueldos`

No confundir:

- gasto real;
- obligación pendiente;
- presupuesto;
- pago bancario;
- transferencia interna.

## Presupuesto

`Presupuesto` sirve para comparar Budget versus ejecución.

No utilizar el total del P&L presupuestario automáticamente como burn total.

Puede haber categorías de `Transacciones` que no estén representadas en la matriz visible del presupuesto.

## Conciliación bancaria

Antes de utilizar cash para análisis ejecutivo:

- comprobar que el cierre bancario esté conciliado;
- revisar diferencias;
- no corregir saldos artificialmente;
- investigar movimientos faltantes o duplicados.

Solo movimientos realizados deben afectar bancos.

## Estados financieros

Esta skill puede apoyar la preparación futura de:

- Estado de Resultados
- Balance General
- Flujo de Caja

Pero no debe confundir las vistas administrativas actuales con estados financieros contables completos.

Fuentes conceptuales:

### Estado de Resultados
- ingresos operativos;
- grants según tratamiento contable definido;
- Real S&A;
- nómina;
- otros gastos e ingresos.

### Balance General
- Bancos;
- CxC;
- CxP;
- CxP Sueldos;
- otros activos y pasivos disponibles.

### Flujo de Caja
- movimientos efectivamente realizados;
- bancos;
- clasificación operativa, inversión y financiamiento cuando corresponda.

Antes de construir estados financieros formales se debe definir tratamiento contable y criterios de devengamiento.

## Auditoría de un KPI inesperado

Si un KPI parece incorrecto:

1. revisar la fórmula;
2. identificar su fuente;
3. revisar filtros y fechas;
4. comparar con `Transacciones`;
5. comprobar estado `Pendiente` versus `Pagado/Cobrado`;
6. revisar vencimientos;
7. revisar conciliación bancaria;
8. revisar TC;
9. buscar duplicados;
10. corregir el dato aguas arriba, no el KPI directamente.

## Tipo de cambio

Respetar las reglas definidas en la skill de Transacciones y TC.

Reglas conocidas:

- USD → 1
- SOL → 0.28
- BOB → TC oficial BCB según fecha
- otras monedas → TC manual cuando corresponda

No reemplazar arbitrariamente el TC utilizado por `Transacciones`.

## Validaciones obligatorias

Antes de modificar fórmulas de Runway o Dashboard:

1. leer encabezados actuales;
2. leer fórmulas actuales;
3. identificar dependencias;
4. comprobar que no existan errores previos;
5. comparar resultados antes y después;
6. verificar `Transacciones`;
7. verificar `Bancos`;
8. buscar `#REF!`, `#VALUE!`, `#N/A` y `#ERROR!`.

## Reglas transversales

- El Google Sheet vivo prevalece sobre snapshots almacenados en GitHub.
- Nunca asumir posiciones históricas de columnas.
- Leer el Sheet antes de escribir.
- No duplicar transacciones.
- No inventar fechas, cuentas, responsables o movimientos.
- No crear movimientos para hacer cuadrar bancos o KPIs.
- Mantener trazabilidad entre dato fuente y vista ejecutiva.
- Explicar claramente si una cifra es real, pendiente, presupuestada o proyectada.
