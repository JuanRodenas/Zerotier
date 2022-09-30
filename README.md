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

## Inspiration

Fuente
    [Github](https://github.com/zerotier/ZeroTierOne)
    [Docker HUB](https://hub.docker.com/r/zerotier/zerotier)
