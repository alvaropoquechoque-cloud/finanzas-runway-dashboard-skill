# Runway Mensual

## Propósito

`Runway Mensual` proyecta la disponibilidad de caja de Sommos y estima cuántos meses puede operar la empresa con el nivel de burn observado.

Archivo principal:
- Spreadsheet ID: `1RXy19WZMPQePflFaFeIIHnh09BpJbwOnk6Wumw8bW4E`
- Hoja: `Runway Mensual`

## Fuente de verdad

El runway debe alimentarse directamente de:

- `Transacciones`
- `Bancos`

Puede consultar:

- `Dashboard`
- `Presupuesto`
- `CxC Mensual`
- `CxP Mensual`

Las antiguas pestañas `CxC` y `CxP` ya no forman parte del modelo.

## Estructura conceptual mensual

La proyección considera:

- Mes
- Saldo inicial USD
- Cobros esperados
- Otros ingresos
- Pagos comprometidos
- Otros egresos
- Flujo neto
- Saldo final proyectado
- Burn proyectado
- Burn histórico promedio
- Runway en meses
- Comentarios

## Saldo inicial

Para el primer mes proyectado:

- utilizar el último cierre bancario real conciliado disponible.

Para meses siguientes:

`Saldo inicial mes N = Saldo final proyectado mes N-1`

No utilizar CxC como saldo inicial.

## Cobros esperados

Deben calcularse desde `Transacciones`.

Condiciones:

- Tipo = `Ingreso`
- Estado = `Pendiente`
- Fecha de vencimiento dentro del mes proyectado

Utilizar `Monto USD`.

Si una cuenta pendiente no tiene fecha de vencimiento, no asignarla arbitrariamente a un mes.

## Pagos comprometidos

Deben calcularse desde `Transacciones`.

Condiciones:

- Tipo = `Egreso`
- Estado = `Pendiente`
- Fecha de vencimiento dentro del mes proyectado

Utilizar `Monto USD`.

No incluir una obligación futura que todavía no haya sido registrada o devengada salvo que el modelo la trate explícitamente como proyección.

## Flujo neto

Fórmula conceptual:

`Cobros esperados + Otros ingresos - Pagos comprometidos - Otros egresos`

## Saldo final proyectado

Fórmula conceptual:

`Saldo inicial + Flujo neto`

Este saldo es una proyección.

No debe confundirse con saldo bancario real.

## Burn histórico

El burn histórico debe calcularse a partir de movimientos realizados.

Condiciones:

- Tipo = `Egreso`
- Estado = `Pagado/Cobrado`
- excluir categoría `Transferencias internas`

Utilizar hasta los últimos 3 meses reales disponibles anteriores al mes proyectado.

Si hay menos de 3 meses completos, utilizar los meses disponibles e indicar la limitación.

## Runway

Fórmula conceptual:

`Runway = Saldo disponible / Burn histórico promedio`

Aplicar únicamente si:

`Burn histórico promedio > 0`

El runway debe expresarse en meses.

Si el burn es cero o no existe suficiente información, no inventar un resultado.

## Grants

Los grants requieren tratamiento especial.

El monto total aprobado de un grant no equivale automáticamente a CxC.

Solo debe entrar en runway cuando exista:

- un desembolso registrado;
- una cuenta por cobrar exigible;
- una fecha esperada o de vencimiento suficientemente definida.

Categoría conocida:

`Other financing cash flow`

No tratar grants automáticamente como ingresos operativos.

## CxC y CxP mensuales

`CxC Mensual` y `CxP Mensual` son vistas de control y presentación.

Pueden contener:

- histórico copiado de archivos anteriores;
- meses recientes derivados de `Transacciones`.

Para cálculo de runway utilizar preferentemente `Transacciones`, no los totales visuales de estas hojas.

## Salarios

Las pestañas:

- `Sueldos 2026`
- `CxP Sueldos`

pueden utilizarse para analizar planificación de nómina y pasivos laborales.

No duplicar un salario en runway si la obligación correspondiente ya existe como egreso pendiente en `Transacciones`.

## Presupuesto

`Presupuesto` puede utilizarse como referencia para escenarios futuros.

No utilizar automáticamente el presupuesto como pago comprometido.

Diferenciar:

- presupuesto
- obligación registrada
- egreso realizado

## Validación

Cuando el runway cambie de forma significativa revisar:

1. saldo bancario inicial;
2. conciliación de bancos;
3. CxC nuevas o modificadas;
4. CxP nuevas o modificadas;
5. fechas de vencimiento;
6. grants;
7. pagos realizados recientemente;
8. burn histórico;
9. transferencias internas;
10. duplicados.

## Principio central

El runway es una estimación.

Siempre distinguir entre:

- cash real;
- CxC;
- CxP;
- flujo comprometido;
- flujo proyectado.

No presentar una proyección como si fuera saldo bancario real.
