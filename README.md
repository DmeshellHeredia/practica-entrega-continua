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
└── templates/
    └── index.html
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
