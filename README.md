# Práctica de Entrega Continua

## Descripción

Aplicación web "Hola Mundo" desarrollada con Flask y empaquetada mediante Docker.

## Objetivo

El flujo realizado en esta práctica es:

1. Desarrollo de la aplicación web con Flask.
2. Creación de la imagen Docker.
3. Ejecución del contenedor.
4. Publicación de la imagen en Docker Hub.

## Tecnologías

- Python
- Flask
- Docker
- Docker Hub
- Git
- GitHub

## Estructura del proyecto

```text
practica-entrega-continua/
├── app.py
├── requirements.txt
├── Dockerfile
├── .dockerignore
├── .gitignore
├── README.md
├── templates/
│   └── index.html
└── .github/
    └── workflows/
        └── ci-cd.yml
```

## Ejecución local

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt
python app.py
```

La aplicación estará disponible en:

```text
http://localhost:5000
```

## Construcción de la imagen

```powershell
docker build -t practica-entrega-continua .
```

## Ejecución del contenedor

```powershell
docker run -d --name practica-entrega-contenedor -p 5000:5000 practica-entrega-continua
```

## Verificación

```powershell
docker ps
docker logs practica-entrega-contenedor
docker images
```

## Publicación en Docker Hub

```powershell
docker tag practica-entrega-continua:latest dmeshell99/practica-entrega-continua:latest
docker login
docker push dmeshell99/practica-entrega-continua:latest
```

## Enlaces

GitHub:

```text
https://github.com/DmeshellHeredia/practica-entrega-continua
```

Docker Hub:

```text
https://hub.docker.com/r/dmeshell99/practica-entrega-continua
```

## Entrega continua con GitHub Actions

Cada `push` a la rama `main` ejecuta automáticamente el siguiente flujo:

```text
GitHub
   ↓
GitHub Actions
   ↓
Construcción de imagen Docker
   ↓
Docker Hub
   ↓
API de Render
   ↓
Aplicación en producción
```

### Detalles del workflow

- **Nombre del workflow:** `CI/CD Docker Hub y Render`
- **Ruta del archivo:** `.github/workflows/ci-cd.yml`
- **Eventos que lo activan:** `push` a la rama `main` y ejecución manual mediante `workflow_dispatch`.
- **Imagen publicada:** `dmeshell99/practica-entrega-continua`, con las etiquetas `latest` y `sha-<commit>`.
- **Despliegue:** tras publicar la imagen en Docker Hub, el workflow solicita a la API de Render que despliegue el servicio a partir de esa misma imagen (`docker.io/dmeshell99/practica-entrega-continua:latest`).
- **Verificación:** el workflow consulta la ruta `/health` del servicio en producción con reintentos limitados hasta confirmar que responde correctamente.
- **URL pública de producción:** [https://practica-entrega-continua-9qcv.onrender.com](https://practica-entrega-continua-9qcv.onrender.com)

### Ejecución manual del workflow

En GitHub, ir a la pestaña `Actions`, seleccionar el workflow `CI/CD Docker Hub y Render` y usar la opción `Run workflow`.

### Secretos requeridos

Estos valores se configuran en `Settings → Secrets and variables → Actions` del repositorio. Solo se almacenan sus nombres aquí, nunca sus valores:

| Secreto | Uso |
|---|---|
| `DOCKERHUB_USERNAME` | Usuario de Docker Hub utilizado para iniciar sesión desde el workflow. |
| `DOCKERHUB_TOKEN` | Personal Access Token de Docker Hub, usado en lugar de la contraseña para publicar la imagen. |
| `RENDER_API_KEY` | API key de Render utilizada para autenticar la solicitud de despliegue. |
| `RENDER_SERVICE_ID` | Identificador del servicio de Render (`srv-...`) sobre el que se solicita el despliegue. |
| `RENDER_SERVICE_URL` | URL pública del servicio en Render, usada para verificar la ruta `/health` tras el despliegue. |
