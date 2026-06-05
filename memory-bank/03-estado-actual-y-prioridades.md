# Estado actual, gaps y prioridades

## Features implementadas (estado actual)
### Backend
- `GET /health`.
- `GET /api/metrics` con filtros por fecha, categoria y operation_type.
- `GET /api/metrics/facets` para opciones de filtros.
- `GET /api/metrics/summary` con `group_by` y filtro opcional por `business_type`.
- `GET /api/metrics/categories/top` con `limit` y filtros.
- `GET /api/metrics/comparison` para delta entre periodo actual y anterior.
- `GET /api/metrics/alerts` para deteccion de picos de egreso.
- `GET /api/metrics/b2b` y `GET /api/metrics/b2c`.

### Frontend
- Fetch de datos financieros desde `/api/metrics`.
- Render de dashboard con header, KPI row y 2 graficos.
- Manejo de loading y error en la vista principal.
- Utilidades de calculo para KPIs, series mensuales y formato de valores.

### Calidad y pruebas
- Tests backend para filtros, estructura de payloads, orden cronologico y endpoints analiticos.
- Tests frontend para utilidades financieras y formateadores.

## Gaps conocidos
1. Backend monolitico en un solo modulo de rutas: logica de dominio y transporte HTTP estan acoplados.
2. No hay persistencia real: los datos son mock generados por seed.
3. Cobertura frontend limitada al dominio utilitario; faltan tests del flujo de fetch/render/error de la App.
4. Defaults de desarrollo en seguridad:
   - CORS abierto (`allow_origins=["*"]`).
   - debugpy expuesto y arranque con `--reload`.
5. El frontend principal consume solo `/api/metrics`; no explota aun summary/top/comparison/alerts en UI.

## Siguientes prioridades recomendadas
1. Separar logica de dominio backend fuera de `routes.py` (servicios + funciones puras testeables).
2. Introducir capa de datos real (DB o fuente persistente) manteniendo contratos actuales.
3. Agregar pruebas frontend de integracion basica para `App` (loading, error, estado exitoso).
4. Parametrizar seguridad por entorno (CORS y debug solo en dev).
5. Expandir la UI para consumir endpoints analiticos ya disponibles (summary, top, comparison, alerts).

## Evidencia en el repo
- Endpoints y logica backend: backend/app/routes.py
- Config API/CORS: backend/app/main.py
- Contenedor backend con debug/reload: backend/Dockerfile
- Flujo UI principal: frontend/src/App.tsx
- Tests backend: backend/tests/test_routes.py
- Tests frontend utilitarios: frontend/src/lib/financial-utils.test.ts
