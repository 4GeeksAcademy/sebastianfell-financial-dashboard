# Contexto del Proyecto: Financial Metrics Dashboard

## 1. ¿Qué es este proyecto?
Es un dashboard de métricas financieras full-stack orientado a visualizar ingresos, egresos y rentabilidad de forma ejecutiva.

La solución está compuesta por:
- Un frontend en React + TypeScript que consume una API.
- Un backend en FastAPI que expone endpoints de métricas.
- Contenedores Docker para ejecutar ambos servicios de forma coordinada.

## 2. Objetivo funcional
El sistema muestra una vista de alto nivel del desempeño financiero con:
- KPIs principales: ingresos totales, egresos totales, utilidad y margen de utilidad.
- Evolución mensual de ingresos vs egresos.
- Evolución del porcentaje de margen de utilidad.

También existe una API más amplia (facetas, resúmenes, top categorías, comparación de periodos y alertas) que prepara el backend para escenarios de análisis más avanzados.

## 3. Stack tecnológico

### Frontend
- React 19
- TypeScript
- Vite 8
- Tailwind CSS 4
- Recharts (gráficas)
- Lucide React (iconografía)
- Vitest (testing)
- ESLint (linting)

### Backend
- Python 3.13
- FastAPI
- Uvicorn
- Pydantic
- Pytest
- Debugpy (debug remoto)

### Infraestructura
- Docker + Docker Compose
- Arquitectura de 2 servicios: frontend (5173) y backend (8000)

## 4. Arquitectura y flujo de datos
1. El navegador carga el frontend en el puerto 5173.
2. El frontend solicita datos a /api/metrics.
3. Vite hace proxy de /api hacia el contenedor backend en http://backend:8000.
4. FastAPI genera datos mock deterministas (seed fija) y responde JSON.
5. El frontend calcula KPIs y agregaciones mensuales en cliente para pintar tarjetas y charts.

## 5. Backend: qué hace exactamente
El backend no usa base de datos en este estado del proyecto. Genera movimientos financieros mock de un año completo:
- 12 meses.
- 30 movimientos por mes.
- Total: 360 registros.

Cada movimiento incluye:
- create_date
- amount
- operation_type (income u outcome)
- category (suppliers, sales, operational, administrative, others)
- business_type (B2B o B2C)

Capacidades principales de la API:
- Salud del servicio.
- Listado de movimientos con filtros por fecha, categoría y tipo de operación.
- Facetas para filtros (tipos, categorías, rango de fechas).
- Resúmenes agregados por día/semana/mes.
- Top categorías por monto (limitable).
- Comparación entre periodo actual y periodo anterior equivalente.
- Alertas por incremento anómalo de egresos respecto al baseline histórico.
- Endpoints segmentados para B2B y B2C.

## 6. Frontend: qué realiza actualmente
La UI principal consume el endpoint de movimientos y renderiza:
- Header del dashboard con periodo.
- Fila de 4 KPI cards.
- Gráfico de líneas de ingresos vs egresos por mes.
- Gráfico de líneas de margen de utilidad mensual.

Comportamiento relevante:
- Estado de carga con skeletons.
- Manejo de error de fetch con mensaje en UI.
- Cálculo de KPIs y agregación mensual en utilidades de frontend.
- Diseño responsive para móvil y desktop.

## 7. Calidad y pruebas
Existe cobertura de pruebas en ambos lados:
- Backend: pruebas de endpoints, filtros, orden cronológico y contratos de respuesta.
- Frontend: pruebas unitarias para utilidades de cálculo (KPIs, agregación mensual y formateadores).

## 8. Ejecución local
El proyecto está preparado para ejecutarse con Docker Compose:
- Frontend: http://localhost:5173
- Backend: http://localhost:8000
- Docs API: http://localhost:8000/docs

## 9. Estado actual y alcance
Es una base sólida para un dashboard financiero educativo/demostrativo:
- La API ya soporta consultas analíticas más ricas de las que la UI actual consume.
- La fuente de datos es simulada (mock), por lo que no hay persistencia ni integración con sistemas financieros reales.

## 10. Posibles siguientes pasos técnicos
- Conectar el backend a una base de datos real y reemplazar generación mock.
- Exponer en frontend filtros avanzados (rango de fechas, B2B/B2C, categoría).
- Consumir en la UI los endpoints de summary, top categories, comparison y alerts.
- Añadir autenticación/autorización para escenarios productivos.
- Incorporar observabilidad (logs estructurados, métricas y tracing).
