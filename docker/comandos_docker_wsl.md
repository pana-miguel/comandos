# Comandos básicos de Docker en WSL

## Instalación en WSL

-   Instalar **Docker Desktop** en Windows.
-   Asegurarse de que **WSL2** esté habilitado.
-   Integrar Docker con la distribución de WSL desde la configuración de
    Docker Desktop.
-   Verificar instalación con:

``` bash
docker --version
```

## Comandos iniciales

``` bash
docker version
docker info
```

## Manejo de imágenes

``` bash
docker pull ubuntu
docker images
docker rmi ubuntu
```

## Manejo de contenedores

``` bash
docker run -it ubuntu bash
docker ps
docker ps -a
docker stop <container_id>
docker rm <container_id>
```

## Volúmenes y redes

``` bash
docker volume ls
docker network ls
```

## Construcción de imágenes con Dockerfile

``` bash
docker build -t mi_imagen .
```

## Ejecución con puertos y volúmenes

``` bash
docker run -d -p 8080:80 mi_imagen
docker run -v $(pwd):/app mi_imagen
```

## Uso de Docker Compose

``` bash
docker compose up -d
docker compose down
```
