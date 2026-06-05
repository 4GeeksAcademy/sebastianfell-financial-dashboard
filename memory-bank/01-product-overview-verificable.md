# Product overview (evidencia verificable)

## Que es el producto
Financial Metrics Dashboard es una aplicacion full-stack para visualizar desempeno financiero con una UI React+TypeScript y API en FastAPI.

## Problema que resuelve
Permite ver de forma ejecutiva ingresos, egresos y rentabilidad, junto con series temporales y cortes analiticos para analisis financiero.

## Flujo funcional principal
1. El frontend consulta `GET /api/metrics`.
2. El backend responde movimientos financieros mock (ordenados por fecha).
3. El frontend calcula KPIs y agregaciones mensuales para pintar tarjetas y graficos.

## Capacidades del producto hoy
- KPI cards de total income, total outcome, profit y profitPercent.
- Grafico de ingresos vs egresos por mes.
- Grafico de profitPercent por mes.
- Estado loading y estado de error en la pantalla principal.
- API con endpoints para filtros, facetas, summary, top categorias, comparacion, alertas y segmentacion B2B/B2C.

## Evidencia en el repo
- Definicion del producto y ejecucion local: README.md
- Flujo UI principal y estados de carga/error: frontend/src/App.tsx
- Calculo de KPIs y agregacion mensual: frontend/src/lib/financial-utils.ts
- Endpoints y contratos de datos: backend/app/routes.py
- Cobertura de comportamiento API: backend/tests/test_routes.py
