# Regla: API contratos y filtros consistentes

## Proposito
Prevenir regresiones en payloads y semantica de filtros.

## Alcance
Endpoints bajo /api/metrics y variantes segmentadas.

## Disparadores
- Se agrega query param.
- Se cambia response model o estructura JSON.
- Se altera filtrado por fechas, categoria, tipo o business_type.

## Fuera de alcance
- Refactors internos sin cambio de contrato.
- Cambios de UI que no consumen API.

## Checklist verificable
- Todo endpoint nuevo declara contrato de respuesta.
- Filtros de fecha mantienen comportamiento inclusivo.
- Respuestas listadas mantienen orden cronologico cuando corresponde.
- Nuevos parametros incluyen validacion y prueba.

## Contexto de repositorio
- backend/app/routes.py
- backend/tests/test_routes.py
