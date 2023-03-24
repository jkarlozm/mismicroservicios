# **Pi-hole**

![Pi-hole](Pihole.png)

## Problemas durante el despliegue.

Durante el despliegue del servicio me enfrente con el siguiente error:

Despliegue del contenedor:

`docker-compose up -d pihole && docker logs -f pihole` 

Error:
- - -
~~~
ERROR: for pihole Cannot start service pihole: driver failed programming external connectivity on endpoint pihole (c6ddeb24bf33865868ea14647e136d1e343ab7d4e149e866e04d840c4edab28a): Error starting userland proxy: listen udp 0.0.0.0:53: bind: address already in use
~~~
- - -

## **Solución.**

Investigando en la red di con está solución:

Enliste los servicios que están dados de alta con su correspondiente puerto en el que están escuchando.

`sudo lsof -iTCP -sTCP:LISTEN -P -n +c 10`

De está manera identifique que en el puerto 53 estaba trabajando el servicio `systemd-resolved`, procedí a detenerlo.

`systemctl stop systemd-resolved`

Tras realizar la acción pude desplegar el servicio.

### **Enlaces de referencia**

+ [stackoverflow - *"cant run pihole in docker-compose"*](https://stackoverflow.com/questions/64402111/cant-run-pihole-in-docker-compose)
+ [discourse.pi-hole - *"Setup on Pi in Docker - Bind Error"*](https://discourse.pi-hole.net/t/setup-on-pi-in-docker-bind-error/19137)
