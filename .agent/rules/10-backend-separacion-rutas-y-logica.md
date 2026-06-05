# Regla: Backend separacion de rutas y logica

## Proposito
Reducir acoplamiento en endpoints FastAPI y facilitar pruebas.

## Alcance
Cambios en backend/app/routes.py y nuevos modulos de dominio backend/app.

## Disparadores
- Se agrega o modifica endpoint.
- Se anade logica de calculo o agregacion financiera.

## Fuera de alcance
- Ajustes de estilo sin cambios funcionales.
- Cambios de infraestructura no relacionados con rutas.

## Checklist verificable
- El endpoint solo orquesta validacion, llamada de dominio y respuesta.
- Logica de negocio nueva no se agrega en routes.py si supera complejidad trivial.
- El contrato de respuesta se declara explicitamente.
- El cambio incluye al menos una prueba de endpoint afectado.

## Contexto de repositorio
- backend/app/routes.py
- backend/tests/test_routes.py
