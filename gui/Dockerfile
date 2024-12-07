# Utiliza la imagen oficial de Node.js
FROM node:20.15.1

# Establece el directorio de trabajo dentro del contenedor
WORKDIR /app

# Copia solo los archivos de package.json y package-lock.json (para optimizar el uso de caché)
COPY package*.json ./

# Instala las dependencias, asegurándose de que se manejen correctamente las dependencias peer
RUN npm install --legacy-peer-deps

# Copia el resto de los archivos de la aplicación al contenedor
COPY . .

# Expone el puerto en el que la aplicación React escuchará
EXPOSE 3000

# Comando para iniciar la aplicación React
CMD ["npm", "start"]
