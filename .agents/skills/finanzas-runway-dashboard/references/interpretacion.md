# Interpretación financiera

## Propósito

Definir reglas comunes para interpretar correctamente las cifras del modelo financiero de Sommos.

Estas reglas deben aplicarse al revisar:

- `Dashboard`
- `Runway Mensual`
- `Transacciones`
- `Bancos`
- `CxC Mensual`
- `CxP Mensual`
- `Operative incomes`
- `Real S&A`
- `Presupuesto`
- `Sueldos 2026`
- `CxP Sueldos`

## Fuente principal

`Transacciones` es la fuente de verdad operativa.

Las demás pestañas:

- resumen;
- proyectan;
- agrupan;
- concilian;
- presentan información.

No deben crear una versión independiente de la misma operación.

## Cash

Cash significa dinero real disponible.

La referencia principal debe ser el último saldo bancario conciliado.

No sumar automáticamente:

- CxC;
- grants futuros;
- presupuesto;
- proyecciones.

## CxC

CxC significa dinero registrado pendiente de cobrar.

En `Transacciones`:

- Tipo = `Ingreso`
- Estado = `Pendiente`

CxC no es cash.

Una cuenta por cobrar deja de estar pendiente cuando se registra correctamente el cobro.

## CxP

CxP significa obligación registrada pendiente de pago.

En `Transacciones`:

- Tipo = `Egreso`
- Estado = `Pendiente`

CxP no es un egreso realizado hasta que ocurre el pago.

## Realizado

Un movimiento realizado debe tener estado:

`Pagado/Cobrado`

Solo movimientos realizados deben afectar directamente:

- caja;
- conciliación bancaria;
- ingresos realizados;
- gastos realizados;
- burn histórico.

## Fecha de pago o cobro

Cuando una factura tiene una fecha de emisión/vencimiento distinta a la fecha bancaria del pago, conservar ambas.

La columna `Fecha pago / cobro` permite registrar cuándo ocurrió realmente el movimiento bancario sin perder la fecha original de la obligación.

## Transferencias internas

Las transferencias entre cuentas de Sommos no son ingresos ni gastos.

Categoría:

`Transferencias internas`

Deben indicar correctamente:

- Cuenta origen
- Cuenta destino

El movimiento debe afectar los bancos involucrados pero no el P&L ni el burn.

No utilizar transferencias internas para cuadrar artificialmente una conciliación.

## Bancos

Los saldos bancarios deben reconciliarse con movimientos realizados.

Fórmula conceptual:

`Saldo final calculado = Saldo inicial + Ingresos - Egresos`

Luego:

`Diferencia = Saldo final banco - Saldo final calculado`

Una diferencia debe investigarse.

Nunca inventar una transacción para hacer que la diferencia sea cero.

## Ingresos operativos

`Operative incomes` presenta ingresos por cliente y mes.

Debe distinguir:

- ingresos operativos;
- grants;
- otros ingresos;
- intereses.

Algunos meses históricos fueron cargados desde archivos financieros anteriores.

Los meses recientes pueden derivarse de `Transacciones`.

No utilizar esta vista como sustituto del registro transaccional.

## Real S&A

`Real S&A` presenta gastos administrativos y operativos por concepto y mes.

Puede contener histórico proveniente de archivos anteriores y periodos recientes derivados de `Transacciones`.

No asumir que el total de `Real S&A` equivale automáticamente al burn total.

Puede haber otros egresos fuera de esta matriz.

## Sueldos

`Sueldos 2026` representa principalmente planificación y estructura de nómina.

`CxP Sueldos` representa obligaciones, adelantos, pagos y saldos relacionados con personal.

Distinguir:

- sueldo presupuestado;
- sueldo devengado;
- sueldo pendiente;
- sueldo pagado.

No duplicar obligaciones salariales entre `CxP Sueldos` y `Transacciones`.

## Presupuesto

Presupuesto significa autorización o planificación financiera.

No equivale a cash.

No equivale a gasto realizado.

La comparación conceptual es:

`Real vs Budget`

Una desviación presupuestaria no implica necesariamente un problema de caja.

## Burn

Burn representa egresos reales de operación.

Debe calcularse desde movimientos realizados.

Excluir:

`Transferencias internas`

No usar presupuesto como burn.

No usar CxP pendiente como burn realizado.

## Grants

Distinguir:

- grant aprobado;
- grant recibido;
- grant pendiente;
- desembolso exigible.

El total aprobado no debe registrarse automáticamente como CxC.

Un grant debe incorporarse a CxC o runway únicamente cuando exista una obligación de desembolso identificable.

## Histórico vs actual

Algunas vistas contienen información histórica proveniente de PDFs o modelos anteriores.

Estas cifras deben conservarse como histórico cuando sean necesarias para continuidad financiera.

Si un dato histórico contradice una transacción bancaria o un registro reciente, no modificarlo silenciosamente.

Se debe identificar:

- fuente histórica;
- dato actual;
- diferencia;
- tratamiento propuesto.

## Actual, comprometido y proyectado

Toda interpretación financiera debe distinguir explícitamente entre:

**Actual**
- ocurrió;
- fue pagado/cobrado;
- puede afectar banco.

**Comprometido**
- existe obligación o derecho;
- todavía está pendiente;
- corresponde a CxC o CxP.

**Proyectado**
- expectativa futura;
- presupuesto;
- forecast;
- no necesariamente existe como obligación contable.

## Estados financieros

La estructura actual prepara información para construir posteriormente:

- Estado de Resultados
- Balance General
- Flujo de Caja

Reglas generales:

- ingresos y gastos realizados alimentan resultados;
- bancos alimentan efectivo;
- CxC pendiente alimenta activos;
- CxP pendiente alimenta pasivos;
- CxP Sueldos puede alimentar pasivos laborales;
- transferencias internas no generan resultado;
- grants requieren clasificación según su naturaleza contable.

Antes de construir estados financieros definitivos, validar criterios contables y periodificación.

## Principio final

Nunca interpretar una cifra únicamente por el nombre de la pestaña.

Rastrear siempre:

`Indicador → fórmula → fuente → transacción → banco/documento`

Si existe una inconsistencia, corregir la fuente y permitir que las vistas derivadas se actualicen.
