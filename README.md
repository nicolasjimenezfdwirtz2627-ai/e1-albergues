E1. Base de datos con Docker Compose
1. Descripción

Este proyecto utiliza Docker Compose para crear una base de datos PostgreSQL y una aplicación web llamada Adminer, que permite consultar los datos de los albergues del Camino de Santiago.

PostgreSQL 17: almacena los datos.
Adminer 4: permite consultar y modificar la base de datos.
Volumen: conserva los datos aunque se detengan los contenedores.
2. Cómo iniciar el proyecto
Paso 1. Crear el archivo .env

Copiamos el archivo de ejemplo:

cp .env.example .env


Editamos el archivo .env y configuramos el usuario, la contraseña y el nombre de la base de datos.

Paso 2. Iniciar los servicios

Ejecutamos el siguiente comando:

docker compose up -d

Paso 3. Acceder a Adminer

Abrimos el navegador y accedemos a la siguiente dirección:

http://localhost:8080

Introducimos los datos de conexión definidos en el archivo .env. El servidor debe ser db.

Paso 4. Comprobar los contenedores

Ejecutamos el siguiente comando:

docker compose ps

3. Prueba de persistencia

| Paso | Comando | Resultado|
|--------------|--------------|--------------|
| 1     | docker compose up -d                         | Se levantan los servicios y aparecen los datos iniciales       |
|2      | Inserir un albergue novo desde Adminer       | Se añade el dato sin problemas      |
|3      | docker compose down e docker compose up -d      | Se apagan los servicios y se reinician pero sin el volumen (ya que quedó creado de la anterior vez)      |
|4      | docker compose down -v e docker compose up -d      | Se apagan los servicios y los volúmenes existentes y luego se inicializa entero de nuevo|

En el paso 3 los datos siguen estando en los volúmenes asi que no se tienen que rehacer
En el 4 se hace docker compose down -v lo que borra los volúmenes existentes y tiene que volver a generarlos cuando se hace 

