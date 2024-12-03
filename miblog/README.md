
Este proyecto es parte de mi Homelab personal, donde busco crear un blog para poder iniciar el desarro de mi marca personal online. Este repositorio cuenta con las configuraciones y servicios implementados sobre Docker.

## Aplicaciones instaladas

*Ghost: Es una plataforma de código abierto para crear y gestionar blogs o sitios web de publicaciones. Se enfoca en ofrecer una experiencia sencilla y rápida, con herramientas para gestionar contenido, personalizar el diseño y realizar análisis de tráfico.
*Nginx Proxy Manager: Es una interfaz gráfica de usuario para gestionar Nginx como proxy inverso. Permite configurar redirecciones, certificados SSL, y gestionar múltiples servicios web de manera fácil a través de una interfaz web, ideal para usuarios que no están familiarizados con la línea de comandos.
*MySQL: Es un sistema de gestión de bases de datos relacional de código abierto. Utiliza el lenguaje SQL para gestionar y almacenar datos en tablas. Es muy popular en aplicaciones web debido a su rendimiento y fiabilidad.
*DuckDNS: Es un servicio de DNS dinámico gratuito que permite asignar un nombre de dominio a una dirección IP dinámica, útil para acceder a servidores domésticos o redes locales a través de Internet, sin la necesidad de una IP estática.
*Umami: Es una herramienta de análisis de tráfico web de código abierto. Es ligera, fácil de usar y respeta la privacidad del usuario, proporcionando información sobre el rendimiento del sitio web y su audiencia sin depender de servicios de terceros.


## Requisitos

Proxmox instalado y configurado.
Docker instalado y configurado.

## Instalación

Crea una carpeta con el nombre "MiBlog".

Descarga dentro de la carpera los siguientes archivos docker-compose.yml y .env usando el siguiente comando:

`wget -c https://raw.githubusercontent.com/jkarlozm/mismicroservicios/refs/heads/main/stackMultimedia/docker-compose.yml`

`wget -c https://github.com/jkarlozm/mismicroservicios/blob/main/stackMultimedia/.env`

Instala cada uno de los servicios de manera individual con el siguente comando:

`docker compose up -d [nombre_servicio] && docker logs -f [nombre_servicio]`

## Uso

Accede a cada aplicación a través de su respectiva URL y puerto:
Ghost: http://tu_servidor:2368
umami: http://tu_servidor:3000

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

* [Inicia tu blog de forma gratuita con Ghost, Umami y Oracle Cloud: mi aventura](https://github.com/jkarlozm/mismicroservicios/tree/main/plex)

Espero que esto te sea útil. Recuerda personalizarlo según tus necesidades y agregar cualquier información adicional que consideres relevante. ¡Buena suerte con tu proyecto!
