# Pi-hole

![Pi-hole](Pihole.png)

## Problemas en la instalación

Durante la puesta en marcha del contenedor me enfrente con el siguientes problema:

`docker-compose up -d pihole && docker logs -f pihole` 

- - -
~~~
ERROR: for pihole Cannot start service pihole: driver failed programming external connectivity on endpoint pihole (c6ddeb24bf33865868ea14647e136d1e343ab7d4e149e866e04d840c4edab28a): Error starting userland proxy: listen udp 0.0.0.0:53: bind: address already in use
~~~
- - -
Investigando en la red di con esta solución:

`sudo lsof -iTCP -sTCP:LISTEN -P -n +c 10`

El comando enlista los servicios que estan dados de alta y el puerto que estan ocupando, de esta manera identifique que el puerto 53 estaba siendo usuado por `systemd-resolved`, procedi a darlo de baja.

`systemctl stop systemd-resolved`

Con el proceso realizado se puedo levantar el contenedor.