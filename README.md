E1. Base de datos con Docker Compose
1. Descrición

Este proxecto utiliza Docker Compose para crear unha base de datos PostgreSQL e unha aplicación web Adminer para consultar os datos dos albergues do Camiño de Santiago.

PostgreSQL 17: almacena os datos.
Adminer 4: permite consultar e modificar a base de datos.
Volume: conserva os datos aínda que se deteñan os contedores.
2. Como iniciar o proxecto
Paso 1. Crear o ficheiro .env

Copiamos o ficheiro de exemplo:

cp .env.example .env


Editamos o ficheiro .env e configuramos o usuario, o contrasinal e o nome da base de datos.

Paso 2. Iniciar os servizos

Executamos:

docker compose up -d

Paso 3. Acceder a Adminer

Abrimos o navegador e entramos en:

http://localhost:8080

Introducimos os datos de conexión definidos no ficheiro .env. O servidor debe ser db.

Paso 4. Comprobar os contedores
docker compose ps

3. Proba de persistencia
Paso	Comando	Resultado obtido
1	docker compose up -d	Inícianse os servizos e aparecen os datos iniciais.
2	Inserir un albergue desde Adminer	O novo albergue gárdase na base de datos.
3	docker compose down e docker compose up -d	O albergue engadido continúa existindo.
4	docker compose down -v e docker compose up -d	O albergue engadido desaparece e recupéranse os datos iniciais.
Por que cambia o resultado no paso 4?

| Paso | Comando | Resultado|
|--------------|--------------|--------------|
| 1     | docker compose up -d                         | Se levantan los servicios y aparecen los datos iniciales       |
|2      | Inserir un albergue novo desde Adminer       | Se añade el dato sin problemas      |
|3      | docker compose down e docker compose up -d      | Se apagan los servicios y se reinician pero sin el volumen (ya que quedó creado de la anterior vez)      |
|4      | docker compose down -v e docker compose up -d      | Se apagan los servicios y los volúmenes existentes y luego se inicializa entero de nuevo|

En el paso 3 los datos siguen estando en los volúmenes asi que no se tienen que rehacer.
En el 4 se hace docker compose down -v lo que borra los volúmenes existentes y tiene que volver a generarlos cuando se hace docker compose up -d.

