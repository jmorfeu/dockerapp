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


