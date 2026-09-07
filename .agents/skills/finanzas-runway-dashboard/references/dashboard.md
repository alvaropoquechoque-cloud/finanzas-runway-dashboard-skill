# Dashboard

## Propósito

El `Dashboard` es la capa ejecutiva del modelo financiero de Sommos.

Resume indicadores para toma de decisiones, pero no debe utilizarse como fuente primaria para registrar o corregir información.

Archivo principal:
- Spreadsheet ID: `1RXy19WZMPQePflFaFeIIHnh09BpJbwOnk6Wumw8bW4E`
- Hoja: `Dashboard`

## Fuentes principales

El Dashboard debe alimentarse principalmente de:

- `Transacciones`
- `Bancos`
- `Runway Mensual`
- `Presupuesto`

Puede utilizar vistas auxiliares para análisis:

- `CxC Mensual`
- `CxP Mensual`
- `Operative incomes`
- `Real S&A`
- `CxP Sueldos`
- `Sueldos 2026`

Estas vistas auxiliares no sustituyen a `Transacciones` como fuente de verdad operativa.

## KPIs principales

Indicadores conocidos:

- Cash disponible
- CxC pendiente
- CxP pendiente
- Ingresos del último mes con datos
- Burn del último mes con datos
- Runway en meses
- CxC vencida
- Presupuesto disponible

## Cash disponible

El cash debe representar dinero real disponible.

Fuente preferida:

- último cierre bancario conciliado de `Bancos`

No sumar CxC al cash.

No considerar ingresos pendientes como efectivo disponible.

## CxC pendiente

Debe calcularse directamente desde `Transacciones`.

Condiciones conceptuales:

- Tipo = `Ingreso`
- Estado pago = `Pendiente`

El total representa derechos de cobro registrados, no caja.

## CxP pendiente

Debe calcularse directamente desde `Transacciones`.

Condiciones conceptuales:

- Tipo = `Egreso`
- Estado pago = `Pendiente`

Representa obligaciones registradas pendientes de pago.

## CxC vencida

Debe considerar únicamente:

- Tipo = `Ingreso`
- Estado = `Pendiente`
- Fecha de vencimiento anterior a la fecha actual

Una CxC sin fecha de vencimiento no debe clasificarse automáticamente como vencida.

## Ingresos

Para indicadores de ingresos realizados utilizar movimientos:

- Tipo = `Ingreso`
- Estado = `Pagado/Cobrado`

Distinguir ingresos operativos de:

- grants
- intereses
- otros ingresos
- financiamiento

`Other financing cash flow` no debe tratarse automáticamente como ingreso operativo.

## Burn

El burn debe provenir de egresos realmente realizados.

Considerar:

- Tipo = `Egreso`
- Estado = `Pagado/Cobrado`

Excluir:

- `Transferencias internas`

El presupuesto no sustituye al burn.

`Real S&A` puede utilizarse para análisis de gasto operativo, pero no necesariamente contiene todos los egresos del negocio.

## Presupuesto disponible

Debe provenir de `Presupuesto`.

La lógica conceptual es:

`Presupuesto total - ejecución real`

No confundir presupuesto disponible con cash disponible.

## Vistas históricas

Algunas pestañas mensuales contienen información histórica cargada desde archivos financieros anteriores.

Actualmente pueden existir periodos históricos manuales y periodos recientes conectados a `Transacciones`.

Ejemplos:

- `Operative incomes`
- `Real S&A`
- `CxC Mensual`
- `CxP Mensual`

Estas vistas sirven para continuidad histórica y presentación.

Si existe una diferencia entre una vista histórica y la fuente operativa actual, señalarla y no modificar datos silenciosamente.

## Auditoría de un KPI

Si un indicador parece incorrecto:

1. revisar la fórmula del KPI;
2. identificar la fuente;
3. revisar los filtros y criterios;
4. validar las transacciones relacionadas;
5. revisar estados `Pendiente` vs `Pagado/Cobrado`;
6. revisar fechas de vencimiento y pago;
7. revisar banco y conciliación si afecta cash;
8. revisar TC cuando corresponda;
9. corregir el problema aguas arriba.

Nunca corregir manualmente un KPI para hacerlo coincidir con una cifra esperada.

## Principio central

El Dashboard resume.

No registra operaciones.

No reemplaza a:

- `Transacciones`
- `Bancos`
- `Presupuesto`
- `Runway Mensual`

Si una cifra del Dashboard está mal, corregir primero la fuente que la genera.
