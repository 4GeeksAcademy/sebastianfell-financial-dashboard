# Regla: Frontera de nombres API vs UI

## Proposito
Evitar errores por mezclar convenciones snake_case y camelCase sin control.

## Alcance
Tipos, mapeos de datos y utilidades en frontend/src/lib y capas de consumo API.

## Disparadores
- Se agrega campo nuevo de API.
- Se define o cambia un type/interface de datos financieros.
- Se incorpora normalizacion de respuesta.

## Fuera de alcance
- Literales de texto en componentes.
- Convenciones de CSS.

## Checklist verificable
- El contrato API conserva snake_case en frontera.
- Si UI usa camelCase, el mapeo esta centralizado y explicito.
- No se mezclan ambas convenciones en el mismo objeto de dominio interno.
- Nuevos campos backend quedan reflejados en tipos frontend.

## Contexto de repositorio
- frontend/src/lib/financial-types.ts
- frontend/src/lib/financial-utils.ts
