# Stack tecnologico

## Frontend
- Runtime/UI: React 19, React DOM 19.
- Lenguaje/build: TypeScript 6, Vite 8, plugin React para Vite.
- Estilos/utilidades UI: Tailwind CSS 4, class-variance-authority, clsx, tailwind-merge.
- Data viz e iconos: Recharts, lucide-react.
- Calidad frontend: ESLint 9, typescript-eslint, Vitest 4, coverage v8.

## Backend
- Lenguaje/runtime: Python (imagen base python:3.13-slim).
- Framework API: FastAPI.
- Servidor ASGI: Uvicorn (uvicorn[standard]).
- Modelado/validacion: Pydantic (usado en BaseModel en rutas).
- Test backend: pytest, pytest-cov, httpx (cliente para tests de API), TestClient de FastAPI.
- Debug dev: debugpy (expuesto en puerto 5678).

## Infraestructura y tooling
- Orquestacion: Docker Compose con 2 servicios (frontend y backend).
- Contenedores:
  - Frontend en puerto 5173.
  - Backend en puertos 8000 (API) y 5678 (debug).
- Dev flow:
  - `docker compose up --build` para levantar todo.
  - Proxy de Vite para `/api` por defecto (sin env extra en local).

## Dependencias clave por capa
- Frontend critico para negocio visual: react, recharts.
- Frontend critico para DX/calidad: vite, typescript, vitest, eslint.
- Backend critico para API: fastapi, uvicorn.
- Backend critico para validacion/testing: pydantic, pytest, httpx.

## Evidencia en el repo
- Dependencias y scripts frontend: frontend/package.json
- Dependencias backend: backend/requirements.txt
- Imagen/arranque backend: backend/Dockerfile
- Compose y puertos: docker-compose.yml
- Nota de proxy `/api`: README.md
