# Utiliza la imagen base de Node.js versión 14
FROM node:14
WORKDIR /app

# Copia los archivos package.json y package-lock.json al directorio de trabajo
COPY package*.json ./

# Instala las dependencias definidas en package.json
RUN npm install

# Copia todos los archivos del proyecto al directorio de trabajo
COPY . .

# Expone el puerto 5000 para que la aplicación sea accesible desde fuera del contenedor
EXPOSE 5000

# Define el comando por defecto para ejecutar la aplicación
CMD ["node", "index.js"]
