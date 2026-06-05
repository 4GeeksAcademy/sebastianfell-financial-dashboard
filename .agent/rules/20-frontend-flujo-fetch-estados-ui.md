# Regla: Frontend flujo fetch y estados UI

## Proposito
Asegurar experiencia robusta en carga de datos y fallos de red.

## Alcance
Pantallas y componentes que consumen API desde frontend/src.

## Disparadores
- Se incorpora fetch nuevo.
- Se modifica flujo de carga de datos.
- Se cambia manejo de errores en pantalla.

## Fuera de alcance
- Componentes puramente visuales sin datos remotos.
- Estilos sin impacto en estados funcionales.

## Checklist verificable
- Se contempla estado loading, error y success.
- El error es visible para el usuario final.
- El calculo de datos para graficos vive en utilidades, no en JSX complejo.
- No se hardcodea host de backend en componentes.

## Contexto de repositorio
- frontend/src/App.tsx
- frontend/src/lib/financial-utils.ts
