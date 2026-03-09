# FastAPI + Docker + GitHub Actions CI/CD Pipeline

Este repositorio contiene una aplicación web sencilla construida con FastAPI, empaquetada en un contenedor Docker y configurada con un flujo de Integración Continua (CI/CD) utilizando GitHub Actions.

## Estructura del Proyecto

- `main.py`: Código de la aplicación FastAPI.
- `test_main.py`: Pruebas unitarias desarrolladas con pytest.
- `requirements.txt`: Dependencias del proyecto.
- `Dockerfile`: Instrucciones para construir la imagen Docker.
- `.dockerignore`: Archivos que no se incluirán en el contenedor.
- `.github/workflows/ci.yml`: Configuración del pipeline de GitHub Actions.
- `requirements.md`: Documento original de requisitos del proyecto.

## Requisitos Previos (Para ejecutar localmente)

- Python 3.11+
- Docker instalado en tu máquina.

## Ejecución Local (Sin Docker)

1. Instala las dependencias:
   ```bash
   pip install -r requirements.txt
   ```
2. Ejecuta el servidor:
   ```bash
   uvicorn main:app --host 0.0.0.0 --port 5000 --reload
   ```
3. Visita la aplicación en tu navegador: [http://localhost:5000](http://localhost:5000)

## Ejecución con Docker

1. Construye la imagen de Docker:
   ```bash
   docker build -t fastapi-app .
   ```
2. Ejecuta el contenedor:
   ```bash
   docker run -d -p 5000:5000 --name mi-fastapi fastapi-app
   ```
3. Visita la aplicación en tu navegador: [http://localhost:5000](http://localhost:5000)

## Pruebas Unitarias

Para ejecutar las pruebas localmente:
```bash
pip install pytest httpx
pytest test_main.py
```

## Configuración del Pipeline CI/CD (GitHub Actions)

El proyecto está configurado para ejecutar automáticamente pruebas y subir la imagen a Docker Hub cada vez que se hace un `push` a la rama `main`.

**Pasos requeridos en tu repositorio de GitHub:**
Para que el pipeline funcione correctamente, debes configurar los siguientes "Secrets" en la configuración de tu repositorio (`Settings` -> `Secrets and variables` -> `Actions`):

- `DOCKERHUB_USERNAME`: Tu nombre de usuario de Docker Hub.
- `DOCKERHUB_TOKEN`: Tu Access Token de Docker Hub (generado en la configuración de seguridad de Docker Hub).
