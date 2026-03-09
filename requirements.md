# Proyecto: API con FastAPI, Docker y CI/CD

## Objetivo Principal
Crear y desplegar una aplicación web utilizando FastAPI, contenerizada con Docker y configurada con un pipeline de integración continua (CI) usando GitHub Actions.

## 1. Requisitos Técnicos

### 1.1. Aplicación Web (FastAPI)
- **Framework:** Python con FastAPI.
- **Endpoint Raíz (`/`):** Debe responder con un mensaje de saludo en formato JSON (ej. `{"mensaje": "Hola Mundo"}`).
- **Testing:** Pruebas automatizadas y unitarias utilizando `pytest` para verificar que el endpoint raíz responde correctamente (Código 200 y contenido esperado).

### 1.2. Contenerización (Docker)
- **Imagen Base:** Utilizar una imagen oficial de Python (ej. `python:3.11-slim`).
- **Dependencias:** Instalar las librerías necesarias desde un archivo `requirements.txt`.
- **Exposición de Puertos:** Exponer explícitamente el puerto `5000` para la aplicación FastAPI.
- **Comando de Ejecución:** Configurar el comando (`CMD` o `ENTRYPOINT`) para arrancar el servidor Uvicorn en el puerto 5000 y el host `0.0.0.0`.

### 1.3. Pipeline de Integración Continua (GitHub Actions)
- **Trigger:** Ejecución automática al realizar push al repositorio.
- **Etapas del Workflow:**
  1. Descargar el código fuente (`actions/checkout`).
  2. Configurar el entorno Python.
  3. Ejecutar las pruebas unitarias con `pytest`.
  4. Autenticarse en Docker Hub usando secretos de GitHub.
  5. Construir la imagen Docker a partir del `Dockerfile`.
  6. Subir (Push) la imagen Docker a Docker Hub.

## 2. Configuración Manual Requerida (Usuario)

1. **Repositorio:** Crear un repositorio en GitHub.
2. **Cuenta Docker Hub:** Asegurar acceso a una cuenta activa de Docker Hub.
3. **Secretos de GitHub:** Configurar los siguientes *Secrets* en el repositorio:
   - `DOCKERHUB_USERNAME`: Tu nombre de usuario en Docker Hub.
   - `DOCKERHUB_TOKEN`: Un token de acceso generado desde la configuración de seguridad de Docker Hub (recomendado sobre el uso de contraseña).

## 3. Entregables Finales

El repositorio debe contener:
- `main.py`: Código de la aplicación FastAPI.
- `test_main.py`: Pruebas unitarias con pytest.
- `requirements.txt`: Listado de dependencias.
- `Dockerfile`: Configuración para la creación de la imagen.
- `.dockerignore`: Archivos a excluir de la imagen.
- `.github/workflows/ci.yml`: Archivo de configuración del pipeline de GitHub Actions.
- `README.md`: Documentación con instrucciones claras sobre cómo construir y ejecutar la imagen Docker localmente, y detalles sobre el pipeline CI.