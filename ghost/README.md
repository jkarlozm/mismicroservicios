# Ghost con docker

![Ghost](./ghost.png)

## Requisitos

- MySQL como gestor de base de datos.
- Imagen de Ghost

## Instalación gestor DB

1. Instalamos el gestor de BD MySQL.

Receta docker compose:
~~~ [yml]
mysql:
  image: mysql
  container_name: mysql
  environment:
    - MYSQL_ROOT_PASSWORD=${PASSSQL}
  volumes:
    - mysqldb:/var/lib/mysql
  networks:
    - database
~~~

Comando de instalación:

~~~ [bash]
dokcer compose up -d mysql
~~~

2. Configuramos usuario, contraseña y permisos.

Accedemos al contenedor:

~~~ [bash]
docker exec -it mysql bash
~~~

Iniciamos sesion con la cuenta **root** en el gestor de BD:

~~~ [bash]
mysql -u root -p
~~~

Creamos usuario y contraseña:

~~~ [myslq]
CREATE USER 'ghost'@'%' IDENTIFIED BY 'contraseña';
~~~

Otorgamos permisos al usuario **ghost**.

~~~ [mysql]
GRANT ALL PRIVILEGES ON ghost_db.* TO 'ghost'@'%';
~~~

Salimos del gestor y del contenedor.

## Instalación de Ghost

1. Instalamos Ghost.

Receta docker compose:

~~~ [yml]
  ghost:
    image: ghost:5-alpine
    container_name: ghost
    environment:
      database__client: mysql
      database__connection__host: mysql
      database__connection__user: ${DBUGHOST}
      database__connection__password: ${DBPGHOST}
      database__connection__database: ${DBGHOST}
      url: http://localhost:8080
    volumes:
      - ghost:/var/lib/ghost/content
    ports:
      - 4200:2368
    restart: always
    links:
      - mysql
    depends_on:
      - mysql
    networks:
      - database
~~~

Comando de instalación:

~~~ [bash]
docker compose up -d ghost && docker compose logs -f ghost
~~~

2. Accedemos a Ghost desde el navegador colocando la IP del servidor mas el puerto.

4. Para acceder a la pagina de administración es necesario colocar `/ghost` despues de la IP:Puerto