# Dockerización de una WebApp

Este documento describe los pasos necesarios para dockerizar una aplicación web utilizando Docker. A continuación, se detallan las instrucciones para crear un Dockerfile, construir la imagen y ejecutar el contenedor.

## Crear el Dockerfile

En la raíz de tu proyecto, crea un archivo llamado `Dockerfile`. Este archivo contendrá las instrucciones para construir la imagen de Docker.

Ejemplo de un Dockerfile básico:

```bash
# Usa una imagen base de Node.js (si tu app está basada en Node.js)
FROM node:14

# Establece el directorio de trabajo dentro del contenedor
WORKDIR /usr/src/app

# Copia los archivos de la aplicación al contenedor
COPY package*.json ./

# Instala las dependencias de la aplicación
RUN npm install

# Copia el resto del código de la aplicación al contenedor
COPY . .

# Expone el puerto en el que correrá la aplicación
EXPOSE 3000

# Comando para iniciar la aplicación
CMD ["npm", "start"]
```
## Crear un archivo `.dockerignore`
Para evitar copiar archivos innecesarios al contenedor, crea un archivo .dockerignore en la raíz del proyecto.

Ejemplo de un .dockerignore básico:
```bash
node_modules
npm-debug.log
.env
```

## Construir la imagen de Docker
Para construir la imagen de Docker, abre una terminal en la raíz de tu proyecto y ejecuta el siguiente comando:

```bash
docker build -t nombre-de-la-imagen .
```
Nota: Reemplaza `nombre-de-la-imagen` con el nombre que deseas darle a tu imagen Docker.

## Ejecutar el contenedor
Una vez que la imagen esté construida, puedes ejecutar un contenedor basado en la imagen utilizando el siguiente comando:

```bash
docker run -p 3000:3000 nombre-de-la-imagen
```
Esto ejecutará la aplicación en el puerto 3000. Puedes acceder a tu aplicación desde el navegador en `http://localhost:3000`.

# Opcional: Crear un docker-compose.yml
Si tu aplicación tiene dependencias adicionales (como una base de datos), puedes utilizar Docker Compose para administrar los contenedores. Crea un archivo `docker-compose.yml` en la raíz de tu proyecto.

Ejemplo de `docker-compose.yml`:

```yaml
version: '3'
services:
  webapp:
    build: .
    ports:
      - "3000:3000"
    volumes:
      - .:/usr/src/app
    command: npm start
```
Ejecutar con Docker Compose
Con el archivo `docker-compose.yml` configurado, puedes iniciar tu aplicación y sus dependencias con el siguiente comando:

```bash
docker-compose up
```
Esto levantará todos los servicios definidos en el archivo `docker-compose.yml`.
