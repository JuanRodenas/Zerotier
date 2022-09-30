# zerotier-one-docker

Docker container to run ZeroTier One using Docker.


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
    image: zerotier/zerotier
    container_name: zerotier
    devices:
      - /dev/net/tun
    network_mode: host
    cap_add:
      - NET_ADMIN
      - SYS_ADMIN
    volumes:
      - $HOME/docker/zerotier:/var/lib/zerotier-one
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
sudo zerotier-cli info
```
## Inspiration

Fuente
    [Github](https://github.com/zerotier/ZeroTierOne)
    [Docker HUB](https://hub.docker.com/r/zerotier/zerotier)
