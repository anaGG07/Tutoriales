
# Despliegue de Aplicaciones Web con Docker

## 1. Introducción a Docker
- **Conceptos básicos**
  - Imagen: Plantilla base para contenedores.
  - Contenedor: Ejecución de una imagen.
  - Volumen: Almacén persistente para datos.
  - Red: Conexión entre contenedores y el exterior.
- **Instalación**
  - En Linux (Ubuntu):
    ```bash
    sudo apt update
    sudo apt install docker.io
    sudo systemctl enable docker
    sudo systemctl start docker
    ```
  - Verificar instalación:
    ```bash
    docker --version
    ```

## 2. Ejecutar y gestionar contenedores
- **Crear y gestionar contenedores**
  - Crear un contenedor interactivo:
    ```bash
    docker run -it --name test_container ubuntu /bin/bash
    ```
    - *¿Dónde?*: Host.
    - *Uso*: Configuración inicial.
  - Crear un contenedor en segundo plano:
    ```bash
    docker run -d -p 8080:80 --name web_server nginx
    ```
    - *¿Dónde?*: Host.
    - *Uso*: Aplicaciones listas para producción.
  - Listar contenedores:
    ```bash
    docker ps -a
    ```
    - *¿Dónde?*: Host.
  - Parar un contenedor:
    ```bash
    docker stop test_container
    ```
  - Eliminar un contenedor:
    ```bash
    docker rm test_container
    ```

## 3. Gestión de imágenes
- **Obtener y gestionar imágenes**
  - Descargar una imagen específica:
    ```bash
    docker pull mysql:8.0
    ```
  - Ver imágenes descargadas:
    ```bash
    docker images
    ```
  - Borrar una imagen:
    ```bash
    docker rmi mysql:8.0
    ```
  - Crear imagen desde un contenedor:
    ```bash
    docker commit <container_id> my_custom_image
    ```

## 4. Persistencia y volúmenes
- **Volúmenes**
  - Crear un volumen:
    ```bash
    docker volume create my_volume
    ```
  - Usar un volumen en un contenedor:
    ```bash
    docker run -v my_volume:/data ubuntu
    ```
- **Bind Mount**
  - Crear un bind mount:
    ```bash
    docker run -v /host/dir:/container/dir nginx
    ```
    - *¿Dónde?*: Host.

## 5. Redes en Docker
- **Tipos de redes**
  - Crear una red personalizada:
    ```bash
    docker network create my_network
    ```
  - Conectar contenedores a la red:
    ```bash
    docker run --network my_network --name db mysql
    ```
  - Listar redes:
    ```bash
    docker network ls
    ```

## 6. Docker Compose
- **Configurar múltiples servicios**
  - Crear un archivo `docker-compose.yml`:
    ```yaml
    version: '3.8'
    services:
      web:
        image: nginx
        ports:
          - "8080:80"
      db:
        image: mysql:8.0
        environment:
          MYSQL_ROOT_PASSWORD: example
    ```
  - Levantar servicios:
    ```bash
    docker-compose up
    ```

## 7. Dockerfile
- **Crear imágenes personalizadas**
  - Crear un archivo `Dockerfile`:
    ```dockerfile
    FROM python:3.9
    WORKDIR /app
    COPY . /app
    RUN pip install -r requirements.txt
    CMD ["python", "app.py"]
    ```
  - Construir imagen:
    ```bash
    docker build -t my_python_app .
    ```

## 8. Ejemplos Avanzados
- **Configurar un contenedor WordPress**
  - Crear archivo `docker-compose.yml`:
    ```yaml
    version: '3.8'
    services:
      wordpress:
        image: wordpress:latest
        ports:
          - "8080:80"
        environment:
          WORDPRESS_DB_HOST: db
          WORDPRESS_DB_USER: user
          WORDPRESS_DB_PASSWORD: password
          WORDPRESS_DB_NAME: wordpress
      db:
        image: mysql:5.7
        environment:
          MYSQL_ROOT_PASSWORD: root
    ```

## Consejos
- Consultar logs de un contenedor:
  ```bash
  docker logs <container_id>
  ```
- Depurar redes:
  ```bash
  docker network inspect my_network
  ```
