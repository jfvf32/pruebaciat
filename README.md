# pruebaciat: Juan Felipe Velasquez Franco - Aspirante a la vacante Desarrollador Full Stack 
### Climate Action Program.

### PROPUESTA:
 ### MONITOR AGRONOMO: OPTIMIZACION DE LAS OPERACIONES AGRICOLAS CON TECNOLOGIA  

### Definición del Alcance
- El objetivo del proyecto es desarrollar una aplicación que permita al personal de campo:

- Registrar las actividades agronómicas (siembra, riego, fertilización, cosecha).
- Visualizar las actividades registradas.
- Visualizar detalles de las parcelas (ubicación, tamaño, tipo de cultivo).

### Lista de Requerimientos
# Funcionales:
- Registro de Actividades:
  Permitir registrar nuevas actividades agronómicas con fecha, tipo de actividad, insumos utilizados y duración.
- Visualización de Actividades:
  Mostrar una lista de actividades agronómicas registradas.
### Gestión de Parcelas:
- Mostrar detalles de las parcelas de la finca (ubicación, tamaño, tipo de cultivo).
- Permitir agregar nuevas parcelas.

### No Funcionales:
- Despliegue:
La aplicación debe ser fácilmente desplegable utilizando Docker.
- Usabilidad:
La interfaz debe ser intuitiva y fácil de usar para los campesinos.

### Arquitectura de Software
La arquitectura propuesta es una aplicación web de dos capas:

- Frontend: Aplicación React que se comunica con el backend para mostrar y registrar información.
- Backend: API construida con Node.js y Express que maneja las operaciones CRUD y se comunica con una base de datos SQLite.

# Modelo de Base de Datos
Utilizaremos una base de datos SQLite con dos tablas principales:
Una para las parcelas y otra para la  actividades

# TPropuesta de tabla para parcelas:
- id: INTEGER PRIMARY KEY AUTOINCREMENT
- nombre: TEXT NOT NULL
- latitud: REAL NOT NULL
- longitud: REAL NOT NULL
- tamano: REAL NOT NULL
- cultivo: TEXT NOT NULL

# Propuesta de tabla actividades:
- id: INTEGER PRIMARY KEY AUTOINCREMENT
- parcela_id: INTEGER
- fecha: TEXT NOT NULL
- actividad: TEXT NOT NULL
- insumos_utilizados: TEXT
- duracion: REAL NOT NULL
- FOREIGN KEY (parcela_id) REFERENCES parcelas (id)

# Sistema de Información

### Paso 1: Crear Dockerfile para el Backend
backend/Dockerfile:
```
# Utiliza la imagen base de Node.js versión 14

FROM node:14

WORKDIR /app

#Copia los archivos package.json y package-lock.json al directorio de trabajo

COPY package*.json ./

#Instala las dependencias definidas en package.json

RUN npm install

# Copia todos los archivos del proyecto al directorio de trabajo

COPY . .

# Expone el puerto 5000 para que la aplicación sea accesible desde fuera del contenedor

EXPOSE 5000

# Define el comando por defecto para ejecutar la aplicación

CMD ["node", "index.js"]
```

# Paso 2: Crear Dockerfile para el Frontend
### frontend/Dockerfile:

```
#Utiliza la imagen base de Node.js versión 14
  
FROM node:14
  
WORKDIR /app

#Copia los archivos package.json y package-lock.json al directorio de trabajo

COPY package*.json ./

#Instala las dependencias definidas en package.json
  
RUN npm install

#Copia todos los archivos del proyecto al directorio de trabajo

COPY . .

#Expone el puerto 3000 para que la aplicación sea accesible desde fuera del contenedor

EXPOSE 3000

#Define el comando por defecto para iniciar la aplicación

CMD ["npm", "start"]
```

#### Paso 3: Configurar Docker Compose
```
docker-compose.yml:

version: '3.8'

services:
  backend:
    build: ./backend
    ports:
      - "5000:5000"
    volumes:
      - ./backend:/app
    environment:
      - DATABASE_URL=sqlite:///app/db.sqlite

  frontend:
    build: ./frontend
    ports:
      - "3000:3000"
    volumes:
      - ./frontend:/app
    environment:
      - REACT_APP_API_URL=http://localhost:5000

```

# Iniciar Aplicación:
Navegar al directorio del proyecto y ejecutar 
```
docker-compose up --build.
```

### Despliegue de la Aplicación
Navegar al directorio del proyecto:
```
cd 
```
### Construir y ejecutar los contenedores:
```
docker-compose up --build
```
### Esto construirá las imágenes Docker para el frontend y el backend, y las ejecutará. 

- La aplicación backend estará disponible en
```
  http://localhost:5000
```
- la aplicación frontend en
```
  http://localhost:3000.
```
