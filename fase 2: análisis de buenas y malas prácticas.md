# Fase 2: análisis de buenas y malas prácticas

## Resumen
- Buenas prácticas identificadas: 5
- Malas prácticas o riesgos identificados: 5

## Arquitectura
### Buena práctica 1
- Evidencia concreta: backend/app/routes.py y backend/app/main.py
- Qué está bien: los endpoints declaran contratos explícitos con response_model y modelos Pydantic (FinancialMovement, MetricsSummaryItem, etc.). Esto evita respuestas "ad hoc" y mantiene validación de tipos en frontera API.

### Riesgo 1
- Evidencia concreta: backend/app/routes.py
- Qué está mal/riesgo: el archivo concentra modelos, generación de datos mock, lógica de agregación, detección de alertas y definición de rutas. Es un módulo monolítico; cualquier cambio en reglas de negocio o transporte HTTP impacta el mismo archivo y aumenta acoplamiento.

## Testing
### Buena práctica 2
- Evidencia concreta: backend/tests/test_routes.py
- Qué está bien: hay pruebas de comportamiento real de endpoints (filtros por fecha/categoría/tipo, segmentación B2B/B2C, estructura de payloads y orden cronológico), no solo tests unitarios aislados.

### Riesgo 2
- Evidencia concreta: frontend/src/lib/financial-utils.test.ts y frontend/src/App.tsx
- Qué está mal/riesgo: en frontend solo se prueba la capa de utilidades; no hay pruebas para el flujo de fetch/render/error de App ni para componentes de gráficos. Un cambio en consumo de API o estados de carga puede romper UI sin alarma en CI.

## Documentación
### Buena práctica 3
- Evidencia concreta: README.md y README.es.md
- Qué está bien: documentación bilingue con comandos de ejecución reales (docker compose up --build), puertos publicados y referencia explícita a la URL de documentación de API.

### Riesgo 3
- Evidencia concreta: README.md y README.es.md vs backend/app/routes.py
- Qué está mal/riesgo: el README no describe el catálogo de endpoints ni parámetros clave (group_by, threshold, business_type, limit). La API es amplia, pero el onboarding depende de inspeccionar código o Swagger manualmente.

## Nombrado
### Buena práctica 4
- Evidencia concreta: backend/app/routes.py y frontend/src/lib/financial-types.ts
- Qué está bien: el dominio financiero usa un vocabulario consistente (income/outcome, category, business_type/B2B-B2C), y los tipos están explícitamente modelados en ambos lados.

### Riesgo 4
- Evidencia concreta: frontend/src/lib/financial-types.ts y frontend/src/lib/financial-utils.ts
- Qué está mal/riesgo: se mezclan convenciones snake_case (create_date, operation_type) con camelCase (totalIncome, profitPercent). Esa dualidad obliga a mapear mentalmente modelos de API y modelos de UI, y aumenta riesgo de errores al extender el contrato.

## Flujo operacional
### Buena práctica 5
- Evidencia concreta: docker-compose.yml y frontend/vite.config.ts
- Qué está bien: el flujo local está bien resuelto con dos servicios y proxy /api hacia backend por nombre de servicio (backend:8000). Reduce fricción de CORS en desarrollo y evita hardcodear localhost en el cliente.

### Riesgo 5
- Evidencia concreta: backend/Dockerfile y backend/app/main.py
- Qué está mal/riesgo: el contenedor backend arranca con debugpy expuesto (5678) y uvicorn --reload, mientras la app permite CORS abierto total (allow_origins=["*"]). Son defaults útiles para desarrollo, pero peligrosos si llegan sin ajuste a entornos no dev.
