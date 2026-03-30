# Guía de Configuración de un Proyecto con Docker en WSL

Este documento contiene los pasos y comandos esenciales para configurar
un proyecto usando **Docker en WSL**.

------------------------------------------------------------------------

## 1. Instalación y Configuración

-   Instalar **Docker Desktop** en Windows.
-   Asegurarse de que **WSL2** esté habilitado.
-   Integrar Docker con la distribución de WSL desde la configuración de
    Docker Desktop.
-   Verificar instalación:

``` bash
docker --version
docker info
```

------------------------------------------------------------------------

## 2. Estructura del Proyecto

Ejemplo de proyecto básico:

    mi-proyecto/
    │── app/
    │    └── main.py
    │── requirements.txt
    │── Dockerfile
    │── docker-compose.yml

------------------------------------------------------------------------

## 3. Dockerfile

Ejemplo de un `Dockerfile` para Python:

``` dockerfile
# Imagen base
FROM python:3.10

# Directorio de trabajo
WORKDIR /app

# Copiar dependencias
COPY requirements.txt .
RUN pip install -r requirements.txt

# Copiar el código
COPY . .

# Comando por defecto
CMD ["python", "main.py"]
```

------------------------------------------------------------------------

## 4. Construir la imagen

``` bash
docker build -t mi_proyecto .
```

------------------------------------------------------------------------

## 5. Ejecutar el contenedor

-   Ejecutar en segundo plano con puerto expuesto:

``` bash
docker run -d -p 5000:5000 mi_proyecto
```

-   Ejecutar con volumen para desarrollo en caliente:

``` bash
docker run -d -p 5000:5000 -v $(pwd):/app mi_proyecto
```

------------------------------------------------------------------------

## 6. Docker Compose

Ejemplo de `docker-compose.yml`:

``` yaml
version: "3.8"
services:
  app:
    build: .
    ports:
      - "5000:5000"
    volumes:
      - .:/app
    depends_on:
      - db

  db:
    image: postgres:15
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
      POSTGRES_DB: mi_db
    ports:
      - "5432:5432"
```

Levantar los servicios:

``` bash
docker compose up -d
```

Detener los servicios:

``` bash
docker compose down
```

------------------------------------------------------------------------

## 7. Comandos Útiles

-   Listar imágenes:

``` bash
docker images
```

-   Listar contenedores:

``` bash
docker ps -a
```

-   Entrar a un contenedor:

``` bash
docker exec -it <container_id> bash
```

-   Eliminar contenedores detenidos:

``` bash
docker container prune
```

-   Eliminar imágenes sin uso:

``` bash
docker image prune -a
```

------------------------------------------------------------------------

## 8. Mantenimiento en WSL

-   Verificar uso de disco:

``` bash
docker system df
```

-   Limpiar todo (contenedores, volúmenes e imágenes sin uso):

``` bash
docker system prune -a --volumes
```
