# zerotier-one-docker

Docker container to run ZeroTier One using Docker.
<p align="center">
        <img src="https://github.com/JuanRodenas/Zerotier/blob/main/zerotier.jpg" alt="zerotier" width="800" height="400"/>
    </a>
    <br>
    <strong>ZeroTier es una de las empresas líderes en SDN</strong>
</p>
<!-- markdownlint-enable MD033 -->


## Instalación desde Respositorios
ZeroTier está disponible en los repositorios de Debian Buster con el nombre zerotier-one

Para instalarlo:
```bash
sudo apt install zerotier-one
```

Instalación de la última versión
```bash
curl -s https://install.zerotier.com/ | sudo bash
```

#### Añadir y Conectarnos a tu Network ID
Tanto la primera vez, como todas aquellas que queremos conectar nuestro dispositivo Linux a ZeroTier, utilizaremos el siguiente comando:
```bash
sudo zerotier-cli join NETWORK-ID
```

#### Desconectarnos del Network ID
Para que nuestro dispositivo Linux se desconecte de la red que hemos creado con ZeroTier, escribiremos los siguiente en la terminal:
```bash
sudo zerotier-cli leave NETWORK-ID
```

## Instalación en Docker
#### Docker-compose
```bash
version: '3.3'

services:
  zerotier:
    image: zerotier/zerotier:latest
    container_name: zerotier
    security_opt:
      - no-new-privileges
    devices:
      - /dev/net/tun
    network_mode: host
    cap_add:
      - NET_ADMIN
      - SYS_ADMIN
    volumes:
      - $HOME/docker/zerotier/data:/var/lib/zerotier-one
    ports:
      - 9993:9993
    environment:
      - PUID=1000
      - PGID=1000
```

Añadir y Conectarnos a tu Network ID
```bash
docker exec -it zerotier-one bash
```
```bash
zerotier-cli join NETWORK-ID
```
En un único comnado
```bash
docker exec -it zerotier-one zerotier-cli join NETWORK-ID
```
Información
```bash
zerotier-cli info
```
Desconectarnos del Network ID
```bash
zerotier-cli leave NETWORK-ID
```
Configuración:
```bash
admin@Ubuntu:~$ sudo zerotier-cli --help
ZeroTier One version 1.10.1 build 0 (platform 1 arch 4)
Copyright (c) 2020 ZeroTier, Inc.
Licensed under the ZeroTier BSL 1.1 (see LICENSE.txt)
Usage: zerotier-cli [-switches] <command/path> [<args>]

Opciones disponibles:
  -h - Mostrar esta ayuda
  -v - Mostrar la versión
  -j - Mostrar la salida JSON completa sin procesar
  -D<ruta> - Ruta de inicio de ZeroTier para la autodetección de parámetros
  -p<puerto> - Puerto HTTP (por defecto: auto)
  -T<token> - Token de autenticación (por defecto: auto)

Comandos disponibles:
  info - Mostrar información de estado
  listpeers - Listar todos los peers
  peers - Listar todos los peers (más bonito)
  listnetworks - Listar todas las redes
  join <identificación de red> - Unirse a una red
  leave <identificación de red> - Abandonar una red
  set <id. de red> <configuración> - Establecer una configuración de red
  get <identificación de red> <configuración> - Obtener una configuración de red
  listmoons - Listar lunas (conjuntos raíz federados)
  orbit <world ID> <seed> - Unirse a una luna a través de cualquier raíz miembro
  deorbit <world ID> - Dejar una luna
  dump - Volcar la configuración de depuración para el soporte


Ajustes disponibles:
  Las configuraciones a utilizar con [get/set] pueden incluir nombres de propiedades de 
  la salida JSON de "zerotier-cli -j listnetworks". Además, 
  (se pueden utilizar ip, ip4, ip6, ip6plane e ip6prefix).Por ejemplo
  zerotier-cli get <network ID> ip6plane devolverá la dirección 6PLANE asignada a este nodo.
```
## Inspiration

Fuente
    [Github](https://github.com/zerotier/ZeroTierOne)
    [Docker HUB](https://hub.docker.com/r/zerotier/zerotier)
