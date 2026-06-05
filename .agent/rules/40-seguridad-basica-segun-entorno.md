# Regla: Seguridad basica segun entorno

## Proposito
Evitar que configuraciones de desarrollo inseguras se propaguen fuera de dev.

## Alcance
Configuracion de backend y contenedores.

## Disparadores
- Se cambia CORS.
- Se exponen puertos nuevos.
- Se modifica arranque de servidor/debug.

## Fuera de alcance
- Reglas de autenticacion de negocio.
- Hardening de infraestructura externa al repo.

## Checklist verificable
- CORS permisivo solo para desarrollo explicito.
- Debug remoto habilitado solo en entorno de desarrollo.
- Configuracion sensible controlada por variables de entorno.
- Todo cambio de seguridad documenta riesgo y comportamiento esperado por entorno.

## Contexto de repositorio
- backend/app/main.py
- backend/Dockerfile
- docker-compose.yml
