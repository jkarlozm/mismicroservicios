# Homelab: Stack Multimedia con Proxmox y Docker

Este proyecto es parte de mi Homelab personal, donde busco crear un entorno de servidores y aplicaciones para gestionar y disfrutar de contenido multimedia de manera eficiente y segura. Este repositorio presenta el stack multimedia configurado sobre Proxmox y Docker.

## Aplicaciones instaladas

* Plex: Servidior de medios para streaming de video, música y fotos.
* Qbittirrent: Cliente de BitTorrent para descarga de archivos.
* Sonarr: Administrador de descargas automáticas de series de TV. 
* Jackett: Buscador de torrents para Sonarr y otros clientes. 
* Bazarr: Administrador de subtítulos para películas y series. 
* Flaresolverr: Resolvedor de problemas de conexión para aplicaciones de descarga. 
* Tiny Media Manager: Organizador de bibliotecas de medios. 

## Requisitos

Proxmox instalado y configurado.
Docker instalado y configurado.

## Instalación

 Crea una carpeta con el nombre "stackmultimedia".

Descarga dentro de la carpera los siguientes archivos docker-compose.yml y .env usando el siguiente comando:

`wget -c https://raw.githubusercontent.com/jkarlozm/mismicroservicios/refs/heads/main/stackMultimedia/docker-compose.yml`

`wget -c https://github.com/jkarlozm/mismicroservicios/blob/main/stackMultimedia/.env`

Instala cada uno de los servicios de manera individual con el siguente comando:

`docker compose up -d [nombre_servicio] && docker logs -f [nombre_servicio]`

## Uso

Accede a cada aplicación a través de su respectiva URL y puerto:   
Plex: http://tu_servidor:32400  
Qbittorrent: http://tu_servidor:8080  
Sonarr: http://tu_servidor:8989  
Jackett: http://tu_servidor:9117  
Bazarr: http://tu_servidor:6767  
Flaresolverr: http://tu_servidor:8192  
Tiny Media Manager: http://tu_servidor:8081  

## Homelab

Este proyecto es parte de un entorno de Homelab más amplio, que incluye otros componenetes como:
Servidor de archivos (NAS)
Servidor de seguridad (VPN, Firewall)
Servidor de monitorización y alertas.
Otros proyectos en desarrollo...

## Contribuciones

Si deseas contribuir a este proyecto, por favor, crea un fork y envía tus pull requests.

## Licencia

Este proyecto se distribuye bajo la licencia GNU General Public License v3.0

## Enlaces Relacionados

* [Mi blog personal](https://vlog-jc.duckdns.org)

* [Administración multimedia Plex](https://github.com/jkarlozm/mismicroservicios/tree/main/plex)

Espero que esto te sea útil. Recuerda personalizarlo según tus necesidades y agregar cualquier información adicional que consideres relevante. ¡Buena suerte con tu proyecto!