---
name: finanzas-runway-dashboard
description: Calcula y audita cash, burn, runway, proyección mensual y KPIs ejecutivos de Sommos.
---

# Finanzas Sommos — Runway y Dashboard

## Propósito

Interpretar y auditar la capa ejecutiva del modelo financiero de Sommos.

Archivo principal:
- Spreadsheet ID: `1RXy19WZMPQePflFaFeIIHnh09BpJbwOnk6Wumw8bW4E`
- URL: `https://docs.google.com/spreadsheets/d/1RXy19WZMPQePflFaFeIIHnh09BpJbwOnk6Wumw8bW4E/edit`

## Alcance principal

Esta skill opera principalmente:
- `Runway Mensual`
- `Dashboard`

También puede consultar:
- `Bancos`
- `CxC`
- `CxP`
- `Transacciones`
- `Presupuesto`

Esta skill es principalmente analítica.

No debe crear o modificar transacciones salvo que el usuario lo solicite expresamente y el caso corresponda claramente a una operación financiera.

## Runway mensual

La proyección debe distinguir entre:
- caja real
- cobros esperados
- pagos comprometidos
- otros ingresos
- otros egresos
- flujo neto
- saldo proyectado
- burn histórico
- runway

## Estructura funcional conocida

Campos principales:
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
- Runway en meses
- Comentario

## Saldo inicial

El saldo inicial debe provenir del último cierre bancario real disponible.

No usar una proyección anterior como saldo real si existe un cierre bancario posterior.

## Cobros esperados

Los cobros esperados deben venir de `CxC` según fecha de vencimiento.

Solo incluir obligaciones todavía pendientes.

CxC no equivale a cash disponible.

## Pagos comprometidos

Los pagos comprometidos deben venir de `CxP` según fecha de vencimiento.

Solo incluir obligaciones todavía pendientes.

CxP no equivale a egreso realizado.

## Burn histórico

Para calcular burn histórico, usar movimientos de `Transacciones` que cumplan:

- Tipo = `Egreso`
- Estado pago = `Pagado/Cobrado`
- excluir `Transferencias internas`

Usar hasta los últimos 3 meses reales disponibles anteriores al mes proyectado, según la lógica vigente en el Sheet.

## Runway

Fórmula conceptual:

`Runway = Saldo disponible o proyectado / Burn histórico promedio`

Solo calcular cuando el burn histórico sea mayor que cero.

El resultado es una aproximación y depende de:
- saldo utilizado
- burn utilizado
- cobros esperados
- pagos comprometidos
- calidad de las fechas de vencimiento

## Dashboard

KPIs ejecutivos conocidos:

- Cash disponible
- CxC pendiente
- CxP pendiente
- Ingresos último mes con datos
- Burn último mes con datos
- Runway
- CxC vencida
- Presupuesto disponible

## Regla de interpretación

No confundir:

- Cash con CxC
- CxP con gasto realizado
- Presupuesto con burn
- Saldo proyectado con saldo bancario real
- Grant aprobado con CxC exigible

## Auditoría de KPIs

Si un KPI parece incorrecto:

1. identificar la fórmula;
2. identificar la pestaña fuente;
3. revisar filtros y criterios;
4. validar las transacciones origen;
5. revisar fechas;
6. revisar estado de pago;
7. revisar TC;
8. corregir la fuente, no el KPI directamente.

## Proyecciones

Toda proyección debe dejar claros sus supuestos.

Si faltan:
- fechas de vencimiento
- gastos recurrentes futuros
- ingresos previstos
- saldos bancarios actualizados

debe indicarse que el runway puede estar incompleto o subestimado/sobrestimado.

## Reglas transversales obligatorias

- El Google Sheet `Finanzas Sommos — Workflow y Control` es la fuente viva.
- `Transacciones` es la fuente de verdad operativa.
- Antes de concluir o modificar, leer en vivo las fuentes relevantes.
- Nunca asumir posiciones históricas de columnas.
- Nunca inventar ingresos o egresos para completar una proyección.
- Distinguir siempre datos reales de datos proyectados.
- Después de cualquier modificación, verificar Dashboard y Runway.
- Los snapshots en GitHub documentan contexto; si contradicen el Sheet, prevalece el Sheet.
