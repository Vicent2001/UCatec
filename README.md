# Configuración de PostgreSQL y MongoDB en Docker

Este README documenta los pasos realizados para levantar contenedores de PostgreSQL y MongoDB usando Docker.

---

## 1. PostgreSQL

### Pasos Realizados:

#### ✅ Creación de un contenedor PostgreSQL

Usamos el siguiente comando de Docker para crear y ejecutar el contenedor de PostgreSQL:

```bash
docker run -d \
  --name postgres_container \
  -e POSTGRES_USER=kevin \
  -e POSTGRES_PASSWORD=secret \
  -e POSTGRES_DB=ucatecdb \
  -p 5434:5432 \
  postgres
```

**Parámetros:**
- `-d`: Ejecuta el contenedor en segundo plano.
- `--name`: Asigna un nombre al contenedor (`postgres_container`).
- `-e`: Define las variables de entorno como el usuario, la contraseña y la base de datos.
- `-p`: Mapea el puerto 5432 del contenedor al puerto 5434 del host.

#### 🔍 Verificación del contenedor PostgreSQL

```bash
docker ps
```

#### 🐚 Acceso al contenedor PostgreSQL

```bash
docker exec -it postgres_container bash
```

Luego, para acceder a la base de datos:

```bash
psql -U kevin --dbname=ucatecdb --password
```

#### 🧪 Consultas SQL dentro del contenedor

```sql
\d
SELECT * FROM estudiantes;
```
### Imagenes del proceso
![alt text](image.png)
![alt text](image-1.png)
![alt text](image-2.png)
---

## 2. MongoDB

### Pasos Realizados:

#### ✅ Creación de un contenedor MongoDB

Usamos el siguiente comando de Docker para crear y ejecutar el contenedor de MongoDB:

```bash
docker run -d \
  --name mongo_container \
  -e MONGO_INITDB_ROOT_USERNAME=kevin \
  -e MONGO_INITDB_ROOT_PASSWORD=secret \
  -p 27017:27017 \
  mongo
```

**Parámetros:**
- `-d`: Ejecuta el contenedor en segundo plano.
- `--name`: Asigna un nombre al contenedor (`mongo_container`).
- `-e`: Define las variables de entorno como el usuario root y la contraseña.
- `-p`: Mapea el puerto 27017 del contenedor al puerto 27017 del host.

#### 🔍 Verificación del contenedor MongoDB

```bash
docker ps
```

#### 🐚 Acceso al contenedor MongoDB

```bash
docker exec -it mongo_container mongosh -u kevin -p secret
```

#### 📋 Consultas dentro del contenedor MongoDB

```javascript
use examenMongo

db.estudiantes.insertMany([
  { nombre: "Luis", carrera: "Ingeniería" },
  { nombre: "Ana", carrera: "Medicina" },
  { nombre: "Pedro", carrera: "Derecho" }
])

db.estudiantes.find()
```

---

## 🛠️ Herramientas Utilizadas

- **Docker**: Para crear, gestionar y ejecutar contenedores.
- **PostgreSQL**: Base de datos relacional utilizada para almacenar información estructurada.
- **MongoDB**: Base de datos NoSQL utilizada para almacenar datos en formato JSON.

### Images del proceso
![alt text](image-3.png)
![alt text](image-4.png)
![alt text](image-5.png)



## 3. Nginx en Docker

Este proyecto muestra cómo ejecutar un contenedor de **Nginx** en Docker con el nombre `kevin1`, sirviendo una página web HTML simple.

---

## 📁 Estructura del Proyecto

```
nginx_kevin1/
├── html/
│   └── index.html
```

---

## 🛠️ Pasos para Ejecutar

### 1. Crear el directorio del proyecto

```bash
mkdir nginx_kevin1
cd nginx_kevin1
mkdir html
echo "<h1>Hola desde Nginx en Docker - Contenedor kevin1</h1>" > html/index.html
```

---

###  Ejecutar el contenedor con Docker

```bash
docker run -d \
  --name kevin1 \
  -p 8080:80 \
  -v $(pwd)/html:/usr/share/nginx/html:ro \
  nginx
```

📌 **Explicación de los parámetros**:

- `-d`: Ejecuta el contenedor en segundo plano.
- `--name kevin1`: Asigna el nombre `kevin1` al contenedor.
- `-p 8080:80`: Mapea el puerto 80 del contenedor al puerto 8080 del host.
- `-v $(pwd)/html:/usr/share/nginx/html:ro`: Monta tu carpeta local `html` como directorio raíz del servidor Nginx.

---

###  Acceder al servidor Nginx

Abre tu navegador y visita:

```
http://localhost:8080
```

Deberías ver el mensaje:

```
Hola desde Nginx en Docker - Contenedor kevin1
```

---

###  Verifica el contenedor en ejecución

```bash
docker ps
```

---

## 🧰 Herramientas Utilizadas

- **Docker**: Plataforma de contenedores.
- **Nginx**: Servidor web liviano y potente.

---

¡Listo! Ahora tienes tu servidor Nginx funcionando dentro de Docker bajo el nombre `kevin1` 🎉

### Imagenes del proceso
![alt text](image-6.png)
![alt text](image-7.png)