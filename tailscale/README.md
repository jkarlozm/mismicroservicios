# ***Tailscale en contenedor LXC de Proxmox***

## Iniciar contenedor docker de tailscale

`docker-compose up -d tailscale && docker logs -f tailscale`

Al ejecutar el comando anterior el contendor se creará, pero no se iniciará, el contenedor se va a estar reiniciando:
* * *
~~~
NAME	tailscale
IMAGE	tailscale/tailscale
PORT	
STATUS	Restarting (1) 15 seconds ago
CREATED	2023-12-24 01:52:44 +0000 UTC
SIZE	0B (virtual 84.6MB)
~~~
* * *

Al consultar el log del contenedor, este va a estar mostrando las siguientes líneas:
* * *
~~~
tailscale  | 2023/12/24 01:53:16 logtail started
tailscale  | 2023/12/24 01:53:16 Program starting: v1.56.1-tf1ea3161a, Go 1.21.5: []string{"tailscaled"}
tailscale  | 2023/12/24 01:53:16 LogID: b332002c83f10f59a28c925177534078b44eaaf895f656d6210d971c82747f07
tailscale  | 2023/12/24 01:53:16 logpolicy: using system state directory "/var/lib/tailscale"
tailscale  | 2023/12/24 01:53:16 wgengine.NewUserspaceEngine(tun "tailscale0") ...
tailscale  | 2023/12/24 01:53:16 Linux kernel version: 6.5.11-7-pve
tailscale  | 2023/12/24 01:53:16 is CONFIG_TUN enabled in your kernel? `modprobe tun` failed with: modprobe: can't change directory to '/lib/modules': No such file or directory
tailscale  | 2023/12/24 01:53:16 wgengine.NewUserspaceEngine(tun "tailscale0") error: tstun.New("tailscale0"): is a directory
tailscale  | 2023/12/24 01:53:16 flushing log.
tailscale  | 2023/12/24 01:53:16 logger closing down
tailscale  | 2023/12/24 01:53:16 getLocalBackend error: createEngine: tstun.New("tailscale0"): is a directory
tailscale exited with code 1
~~~
* * *
## ***Tailscale en contenedores LXC de Proxmox (SOLUCIÓN)***
Es necesario hacer la siguiente configuración en el archivo `*.conf` de la ruta `/etc/pve/lxc/100.conf` en proxmox para que el contenedor docker pueda iniciar.

1. Modificar archivo `*.conf` en proxmox.
    - En proxmox accedemos al archivo `[ID_CONTENEDOR].conf` para editarlo.
      
      `nano /etc/pve/lxc/100.conf`
      
      *El número 100 corresponde al ID del contender proxmox en el cual se está ejecutando tailscale.*

2. Al final del documento agregamos las siguientes líneas.
   
   `lxc.cgroup2.devices.allow: c 10:200 rwm`     
   `lxc.mount.entry: /dev/net/tun dev/net/tun none bind,create=file`

3. Reiniciamos el contenedor LXC de proxmox, el contendor de tailscale debe de iniciarse sin problema alguno. 

## Iniciar sesión en tailscale

`docker exec tailscale tailscale up`


### ***Fuentes.***

+ [Ugeek - *"DOCKER. TAILSCALE"*](https://ugeek.github.io/blog/post/2021-06-17-docker-tailscale.html)
+ [Tailscale - *"Tailscale in LXC containers"*](https://tailscale.com/kb/1130/lxc-unprivileged)
+ [Tailscale - *"Tailscale on Proxmox host"*](https://tailscale.com/kb/1133/proxmox)
+ [Roger Biderbost - *"CONFIGURAR TAILSCALE en WINDOWS ANDROID y LINUX"*](https://youtu.be/5bgQCknkRI4?si=3jYmQcQUEJ9mjkJ1)
+ [Roger Biderbost - *"CONFIGURAR TAILSCALE en DIFERENTES ROUTERS para CONECTAR REDES"*](https://youtu.be/QLr3pyxUWcE?si=a9NFotyd1-yF2gIl)