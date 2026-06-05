# Regla: Pruebas minimas por tipo de cambio

## Proposito
Garantizar cobertura minima util sin bloquear iteracion.

## Alcance
Cambios funcionales en backend y frontend.

## Disparadores
- Se modifica endpoint o filtro backend.
- Se modifica utilidad de calculo financiero.
- Se altera flujo de fetch o manejo de error en UI.

## Fuera de alcance
- Cambios de formato sin impacto funcional.
- Renombres internos sin cambio de comportamiento.

## Checklist verificable
- Cambio en endpoint: al menos 1 prueba de contrato y 1 de filtro/caso borde.
- Cambio en utilidades: al menos 1 prueba de caso normal y 1 de borde.
- Cambio de fetch UI: prueba de error o fallback visible.
- El cambio no se marca completo si faltan pruebas afectadas.

## Contexto de repositorio
- backend/tests/test_routes.py
- frontend/src/lib/financial-utils.test.ts
