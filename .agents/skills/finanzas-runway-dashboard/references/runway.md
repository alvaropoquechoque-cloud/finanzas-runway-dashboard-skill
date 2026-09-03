# Runway mensual

## Propósito

Estimar cuántos meses puede operar Sommos con la caja disponible y los flujos proyectados.

## Fuentes

El runway debe construirse a partir de:

- `Bancos` → cash real disponible
- `CxC` → cobros esperados
- `CxP` → pagos comprometidos
- `Transacciones` → burn histórico
- `Runway Mensual` → proyección consolidada

## Saldo inicial

El saldo inicial debe provenir del último cierre bancario real disponible.

No sustituir un cierre bancario real por una proyección.

## Cobros esperados

Usar CxC pendientes cuya fecha de vencimiento caiga dentro del mes proyectado.

No incluir:
- cuentas ya cobradas
- grants aprobados sin desembolso exigible
- ingresos sin fecha o compromiso suficientemente definido

## Pagos comprometidos

Usar CxP pendientes cuya fecha de vencimiento caiga dentro del mes proyectado.

Una obligación pendiente forma parte del forecast, pero no del burn realizado.

## Burn histórico

Usar movimientos que cumplan:

- Tipo = `Egreso`
- Estado pago = `Pagado/Cobrado`
- excluir `Transferencias internas`

Calcular usando hasta los últimos tres meses reales disponibles anteriores al mes analizado, según la lógica vigente del Sheet.

## Fórmula conceptual

`Flujo neto = Cobros esperados + Otros ingresos - Pagos comprometidos - Otros egresos`

`Saldo final = Saldo inicial + Flujo neto`

`Runway = Saldo final / Burn histórico promedio`

## Limitaciones

El runway puede quedar distorsionado cuando:

- faltan vencimientos en CxC
- faltan vencimientos en CxP
- no se han incluido gastos recurrentes futuros
- faltan cierres bancarios
- existe un burn histórico poco representativo
- existen ingresos extraordinarios

Siempre explicar los supuestos relevantes.
