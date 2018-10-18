---
layout: default
title: Duckdns en Docker
categories: docker
---

# Ducksdns en Docker
* * *

>El DNS dinámico (DDNS) es un servicio que permite la actualización en tiempo real de la información sobre nombres de dominio situada en un servidor de nombres. El uso más común que se le da es permitir la asignación de un nombre de dominio de Internet a un dispositivo con dirección IP variable (dinámica). Esto permite conectarse con la máquina en cuestión sin necesidad de tener conocimiento de que dirección IP posee en ese momento.
>
El DNS dinámico hace posible utilizar un software de servidor en un dispositivo con dirección IP dinámica (como la suelen facilitar muchos ISP) para, por ejemplo, alojar un sitio web en la PC de nuestra casa, sin necesidad de contratar un hosting de terceros.

## Creación del subdominio

Entramos a la web de duckdns por este [enlace](https://www.duckdns.org "duckdns").

![duckdns1](/blog/assets/img/duckdns1.png)

Elegimos el subdominio que queramos y le damos a add domain y nos apuntamos el token para mas adelante.

![duckdns2](/blog/assets/img/duckdns2.png)

## Creación del contenedor de docker

Creamos el contenemos de duckdns para que tengamos siempre nuestro subdominio actualizado con nuestra ip actual, con los datos proporcionados al crear el subdominio en duckdns.

```
docker run -d --name='duckdns' \
--net='host' \
-e TZ="Europe/Paris" \
-e 'SUBDOMAINS'='NUESTRO SUBDOMINIO DE DUCKDNS' \
-e 'TOKEN'='NUESTRO TOKEN' \
-e 'PUID'='ID USUARIO' \
-e 'PGID'='ID GRUPO' \
--memory=1024m \
'linuxserver/duckdns'
```
Este contenedor tiene habilitado un cron que actualiza la ip, si hace falta, cada 15 minutos.

Si tenemos ip dinámica y necesitamos dar una dirección estática para algún servicio como nextcloud ya podremos usar nuestro ddns.
