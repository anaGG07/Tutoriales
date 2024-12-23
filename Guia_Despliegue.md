# Tareas para Configurar Apache en un Contenedor de Ubuntu

## Instalación y Configuración Básica (Tarea 1)

### Crear Contenedor de Ubuntu

#### Opción 1: Usar un comando Docker
- **Comando Docker**:
  ```bash
  docker run -dit --name apacheU2_AMG -p 80:80 -p 443:443 \
  -v /ruta/local/www:/var/www/ \
  -v /ruta/local/apache2:/etc/apache2 \
  ubuntu:latest
  ```
  - `-p 80:80`: Publicar puerto HTTP.
  - `-p 443:443`: Publicar puerto HTTPS.
  - `-v`: Crear bind mounts hacia las carpetas locales.

#### Opción 2: Crear desde un Dockerfile
1. **Crear el archivo Dockerfile**:
   ```dockerfile
   FROM ubuntu:latest
   RUN apt update && apt install -y apache2 apache2-utils
   CMD ["apache2ctl", "-D", "FOREGROUND"]
   ```
2. **Construir la imagen**:
   ```bash
   docker build -t apache_image .
   ```
3. **Ejecutar el contenedor**:
   ```bash
   docker run -dit --name apacheU2_AMG -p 80:80 -p 443:443 \
   -v /ruta/local/www:/var/www/ \
   -v /ruta/local/apache2:/etc/apache2 \
   apache_image
   ```

#### Opción 3: Usar Docker Compose
1. **Crear el archivo `docker-compose.yml`**:
   ```yaml
   version: '3.8'
   services:
     apache:
       image: ubuntu:latest
       container_name: apacheU2_AMG
       ports:
         - "80:80"
         - "443:443"
       volumes:
         - /ruta/local/www:/var/www/
         - /ruta/local/apache2:/etc/apache2
       command: bash -c "apt update && apt install -y apache2 apache2-utils && apache2ctl -D FOREGROUND"
   ```
2. **Levantar el contenedor**:
   ```bash
   docker-compose up -d
   ```

### Instalar Apache en el Contenedor
1. **Actualizar Ubuntu**:
   ```bash
   apt update && apt upgrade -y
   ```
2. **Instalar Apache**:
   ```bash
   apt install apache2 apache2-utils -y
   ```
3. **Verificar Instalación**:
   - Mostrar versión:
     ```bash
     apache2 -v
     ```
   - Estado del servicio:
     ```bash
     service apache2 status
     ```

### Configurar Permisos
- Asegurar permisos 775 en `/var/www/html/`:
  ```bash
  chmod -R 775 /var/www/html
  ls -la /var/www/html
  ```

### Configurar Seguridad
- Editar `/etc/apache2/apache2.conf` para ocultar versión y directorios:
  ```bash
  nano /etc/apache2/apache2.conf
  ```
  - Añadir:
    ```
    ServerSignature Off
    ServerTokens Prod
    ```
  - Reiniciar Apache:
    ```bash
    service apache2 restart
    ```

## Configuración de Virtual Hosts (Tarea 2)

### Crear Carpetas y Archivos HTML
1. **Crear Directorios para Sitios**:
   ```bash
   mkdir -p /var/www/html/dominio1AMG /var/www/html/dominio2AMG
   ```
2. **Crear Archivos HTML**:
   ```bash
   nano /var/www/html/dominio1AMG/index.html
   ```
   - Contenido:
     ```html
     <html>
     <head><title>Dominio1AMG</title></head>
     <body>
     <h1>Dominio1 de Alberto Zagalaz Anula</h1>
     </body>
     </html>
     ```
   - Repetir para `dominio2AMG`.

### Crear Archivos de Configuración
1. **Archivo VirtualHost para dominio1AMG**:
   ```bash
   nano /etc/apache2/sites-available/dominio1AMG.conf
   ```
   - Contenido:
     ```
     <VirtualHost *:80>
       ServerName dominio1AMG
       DocumentRoot /var/www/html/dominio1AMG
     </VirtualHost>
     ```
   - Repetir para `dominio2AMG`.

2. **Activar Sitios**:
   ```bash
   a2ensite dominio1AMG.conf
   a2ensite dominio2AMG.conf
   ```
3. **Reiniciar Apache**:
   ```bash
   service apache2 reload
   ```

### Modificar Archivo Hosts
- Editar `/etc/hosts` para asociar dominios:
  ```
  127.0.0.1 dominio1AMG
  127.0.0.1 dominio2AMG
  ```

### Probar en Navegador
- Verificar accesos a:
  - `http://dominio1AMG`
  - `http://dominio2AMG`

## Crear Certificado SSL (Tarea 3)

### Generar y Firmar Certificados con OpenSSL
1. **Crear Certificado sin Firmar**:
   ```bash
   mkdir -p /etc/apache2/certs-ssl
   openssl req -new -newkey rsa:2048 -nodes -keyout /etc/apache2/certs-ssl/clavePrivadaAMG.key \
   -out /etc/apache2/certs-ssl/certificadoAMG.csr
   ```
   - Información requerida:
     - País: `ES`
     - Provincia: `Granada`
     - Localidad: `Granada`
     - Organización: `Hermenegildo Lanz`
     - Unidad organizativa: `IES`
     - Nombre común: `Tu Nombre Completo`
     - Email: `AMG@hlanz.es`
     - Password: `root1234@`

2. **Firmar Certificado**:
   ```bash
   openssl x509 -req -days 365 -in /etc/apache2/certs-ssl/certificadoAMG.csr \
   -signkey /etc/apache2/certs-ssl/clavePrivadaAMG.key \
   -out /etc/apache2/certs-ssl/certificadoFirmadoAMG.crt
   ```

### Configurar Virtual Hosts para SSL
1. **Archivo VirtualHost para dominio1AMG**:
   ```bash
   nano /etc/apache2/sites-available/dominio1AMG-ssl.conf
   ```
   - Contenido:
     ```
     <VirtualHost *:443>
       ServerName dominio1AMG
       DocumentRoot /var/www/html/dominio1AMG
       SSLEngine on
       SSLCertificateFile /etc/apache2/certs-ssl/certificadoFirmadoAMG.crt
       SSLCertificateKeyFile /etc/apache2/certs-ssl/clavePrivadaAMG.key
     </VirtualHost>
     ```
   - Repetir para `dominio2AMG`.

2. **Activar SSL**:
   ```bash
   a2enmod ssl
   a2ensite dominio1AMG-ssl.conf
   a2ensite dominio2AMG-ssl.conf
   ```
3. **Reiniciar Apache**:
   ```bash
   service apache2 restart
   ```

### Verificar SSL en Navegador
- Navegar a:
  - `https://dominio1AMG`
  - `https://dominio2AMG`
- Mostrar detalles del certificado.
