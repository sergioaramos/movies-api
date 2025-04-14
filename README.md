# Movies API

## Descripción
Este proyecto es una API RESTful para gestionar una base de datos de películas. Permite realizar operaciones CRUD (Crear, Leer, Actualizar, Eliminar) sobre una colección de películas. La API está construida con Node.js y Express, y ofrece múltiples implementaciones de almacenamiento de datos (sistema de archivos local, MySQL y MongoDB).

## Características
- Operaciones CRUD completas para películas
- Validación de datos con Zod
- Múltiples implementaciones de almacenamiento:
  - Sistema de archivos local
  - Base de datos MySQL
  - Base de datos MongoDB
- Middleware CORS para permitir peticiones desde dominios específicos
- Estructura modular y escalable

## Estructura del Proyecto
```
movies-api/
├── app.js                 # Configuración principal de Express
├── utils.js               # Utilidades (lectura de JSON, etc.)
├── server-with-local.js   # Servidor usando almacenamiento local
├── server-with-mysql.js   # Servidor usando MySQL
├── movies.json            # Datos de películas para almacenamiento local
├── controllers/
│   └── movies.js          # Controladores para las rutas de películas
├── middlewares/
│   └── cors.js            # Middleware para manejo de CORS
├── models/
│   ├── local-file-system/ # Modelo para almacenamiento local
│   │   └── movie.js
│   ├── mongodb/           # Modelo para MongoDB
│   │   └── movie.js
│   └── mysql/             # Modelo para MySQL
│       └── movie.js
├── routes/
│   └── movies.js          # Definición de rutas de la API
├── schemas/
│   └── movies.js          # Esquemas de validación con Zod
└── web/
    └── index.html         # Cliente web simple para probar la API
```

## Requisitos
- Node.js (versión recomendada: 16 o superior)
- npm o pnpm
- MySQL (para la implementación con MySQL)
- MongoDB (para la implementación con MongoDB)

## Instalación
1. Clonar el repositorio:
```bash
git clone https://github.com/sergioaramos/movies-api.git
cd movies-api
```

2. Instalar dependencias:
```bash
npm install
# o
pnpm install
```

3. Configurar las variables de entorno (opcional):
Crear un archivo `.env` en la raíz del proyecto con las siguientes variables:
```
PORT=1234
DATABASE_URL=mysql://user:password@localhost:3306/moviesdb
```

## Uso

### Iniciar el servidor
Con almacenamiento local:
```bash
npm run start:local
# o
pnpm run start:local
```

Con MySQL:
```bash
npm run start:mysql
# o
pnpm run start:mysql
```

### Endpoints de la API

#### Obtener todas las películas
```
GET /movies
```
Query params opcionales:
- `genre`: Filtrar por género

#### Obtener una película por ID
```
GET /movies/:id
```

#### Crear una nueva película
```
POST /movies
```
Cuerpo de la petición (JSON):
```json
{
  "title": "Nombre de la película",
  "year": 2023,
  "director": "Nombre del director",
  "duration": 120,
  "poster": "https://url-de-la-imagen.jpg",
  "genre": ["Acción", "Aventura"]
}
```

#### Actualizar una película existente
```
PATCH /movies/:id
```
Cuerpo de la petición (JSON) - campos a actualizar:
```json
{
  "year": 2024,
  "rate": 9.5
}
```

#### Eliminar una película
```
DELETE /movies/:id
```

## Modelos de Datos

### Película
```json
{
  "id": "string (UUID)",
  "title": "string",
  "year": "number",
  "director": "string",
  "duration": "number (minutos)",
  "poster": "string (URL)",
  "genre": "string[]",
  "rate": "number (0-10)"
}
```

## Implementaciones

### Sistema de archivos local
- Usa un archivo JSON para almacenar los datos
- Ideal para desarrollo y pruebas
- No requiere configuración adicional

### MySQL
- Requiere una base de datos MySQL
- Estructura de base de datos:
  - Tabla `movie` para almacenar información básica
  - Tabla `genre` para almacenar géneros
  - Tabla `movie_genres` para la relación muchos a muchos

### MongoDB
- Requiere una instancia de MongoDB
- Almacena documentos JSON directamente

## Cliente Web
Se incluye un cliente web simple (`web/index.html`) que muestra las películas y permite eliminarlas. Para usarlo:
1. Inicia el servidor
2. Abre `web/index.html` en un navegador

## Configuración para Desarrollo
- El proyecto usa ES Modules (import/export)
- Se recomienda usar Node.js con la opción `--watch` para desarrollo
- La validación de datos se realiza con Zod

## Consideraciones
- La API usa UUID para los IDs en el modo local
- En MySQL, se convierten los UUID a formato binario para optimizar el almacenamiento
- CORS está configurado para permitir peticiones solo desde orígenes específicos

## Laboratorio
Este proyecto es un laboratorio educativo para demostrar:
1. Arquitectura de una API RESTful con Node.js y Express
2. Implementación del patrón MVC
3. Múltiples implementaciones de almacenamiento con una misma interfaz
4. Validación de datos con esquemas
5. Configuración de CORS y seguridad básica
6. Estructura modular para facilitar la escalabilidad