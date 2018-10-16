---
layout: default
title: Como ejecutar pihole en docker
categories: docker
---

# ¿Que es PI-HOLE
* * *

Pi-hole es un **servidor dns** concebido para ayudarnos a bloquear publicidad, malware, mineria de monedas y sitios no deseados mientras navegamos.

Las **ventajas** de tener a pihole son muchas, entre ellas, menor consumo de ancho (ahorrarás datos), mejora en la experiencia de navegación, rapidez de carga, etc...

Cuando tengamos Pi-hole funcionando podremos asignar la ip de este a nuestro router como DNS único. De este modo cuando hagamos una consulta con nuestro navegador, esta será filtrada por Pi-hole y este la bloqueará o la rediccionará a nuestro dns alternativo que configuremos desde el panel de administración.

Pi-hole Funciona en nuestra red interna pero **podremos extender su capacidad si nos conectamos por VPN**, de este modo las consultas que hagamos pasarán por nuestro DNS.

Pi-hole **no filtrará el 100% de publicidad o webs fraudulentas** y en algunas ocasiones desechará contenido que realmente queremos, para esto tendremos que acceder al panel de administración de Pi-hole y poner la web que queramos **acceder en la lista de whitelist** o la que queramos **bloquear en blacklist**.

Pi-hole se nutre de listados de webs realizado por la comunidad de usuarios.

En mi caso uso el listado de **Block list project** que lo podrás encontrar en el siguiente [enlace](https://tspprs.com/ "Block list project").

# Ejecutando PI-HOLE por primera vez
* * *

Para ejecutar este docker lanzamos desde un **cmd si estamos en windows**, o un **terminal si estamos en mac o linux**.

```
docker run -d \
--name='pihole' \
--net='br0' \
--ip='192.168.1.22' \
-e TZ="Europe/Madrid" \
-e HOST_OS="Unraid" \
-e 'TCP_PORT_53'='5355' \
-e 'UDP_PORT_53'='5355' \
-e 'TCP_PORT_80'='8055' \
-e 'PUID'='99' \
-e 'PGID'='100' \
-e 'ServerIP'='192.168.1.22' \
-e 'ServerIPv6'='' \
-e 'DNS1'='8.8.8.8' \
-e 'DNS2'='8.8.4.4' \
-e 'IPv6'='False' \
-e 'WEBPASSWORD'='YOURPASSWORD' \
-e 'DNSMASQ_LISTENING'='all' \
-v '/mnt/user/appdata/pihole/pihole/':'/etc/pihole/':'rw' \
-v '/mnt/user/appdata/pihole/dnsmasq.d/':'/etc/dnsmasq.d/':'rw' \
--cap-add=NET_ADMIN \
--dns 127.0.0.1 \
--dns 1.1.1.1 \
--restart=unless-stopped \
'pihole/pihole:latest' \
```
{% comment %}
## Explicado:
* * *


<table>
<colgroup>
<col width="15%" />
<col width="85%" />
</colgroup>
<thead>
<tr class="header" bgcolor="#F8F8F8">
<th>Parametro</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr>
<td markdown="span">docker run -d</td>
<td markdown="span">Ejecutar contenedor en background</td>
</tr>
<tr bgcolor="#F8F8F8">
<td markdown="span">--name='pihole'</td>
<td markdown="span">Nombre contenedor
</td>
<tr>
<td markdown="span">--net='br0'</td>
<td markdown="span">Interfaz de red de docker
</td>
<tr bgcolor="#F8F8F8">
<td markdown="span">--ip='192.168.1.22'</td>
<td markdown="span">Ip que asignamos al Pi-hole
</td>
<tr>
<td markdown="span">-e TZ="Europe/Madrid"</td>
<td markdown="span">Agrega el timezone
</td>
<tr bgcolor="#F8F8F8">
<td markdown="span">-e HOST_OS="Unraid"</td>
<td markdown="span">SO del cliente de docker
</td>
<tr>
<td markdown="span">-e 'TCP_PORT_53'='5355'</td>
<td markdown="span">Mapeo Puerto TCP
</td>
<tr bgcolor="#F8F8F8">
<td markdown="span">-e 'UDP_PORT_53'='5355'</td>
<td markdown="span">Mapeo Puerto UDP
</td>
<tr>
<td markdown="span">-e 'TCP_PORT_80'='8055'</td>
<td markdown="span">Mapeo Puerto TCP
</td>
<tr bgcolor="#F8F8F8">
<td markdown="span">-e 'PUID'='99'</td>
<td markdown="span">User ID (por si hay problemas de permisos)
</td>
<tr>
<td markdown="span">-e 'PGID'='100'</td>
<td markdown="span">Group ID (por si hay problemas de permisos)
</td>
<tr bgcolor="#F8F8F8">
<td markdown="span">-e 'ServerIP'='192.168.1.22'</td>
<td markdown="span">Ip que asignamos al Pi-hole
</td>
<tr>
<td markdown="span">-e 'ServerIPv6'=''</td>
<td markdown="span">Ipv6 (no usaremos, la dejamos en blanco)
</td>
<tr bgcolor="#F8F8F8">
<td markdown="span">-e 'DNS1'='8.8.8.8'</td>
<td markdown="span">DNS para el formward
</td>
<tr>
<td markdown="span">-e 'DNS2'='8.8.4.4'</td>
<td markdown="span">DNS alternativo para el forward
</td>
<tr bgcolor="#F8F8F8">
<td markdown="span">-e 'IPv6'='False'</td>
<td markdown="span">Ipv6 (no usaremos, la dejamos en blanco)
</td>
<tr>
<td markdown="span">-e 'WEBPASSWORD'='YOURPASSWORD'</td>
<td markdown="span">Contraseña panel admin Pi-Hole
</td>
<tr bgcolor="#F8F8F8">
<td markdown="span">-e 'DNSMASQ_LISTENING'='all'</td>
<td markdown="span">Habilitamos DNSMASQ
</td>
<tr>
<td markdown="span">-v '/pihole/pihole/':'/etc/pihole/':'rw'</td>
<td markdown="span">Mapeo de carpeta para guardar config
</td>
<tr bgcolor="#F8F8F8">
<td markdown="span">-v '/pihole/dnsmasq.d/':'/etc/dnsmasq.d/':'rw'</td>
<td markdown="span">Mapeo de carpeta para guardar config
</td>
<tr>
<td markdown="span">--cap-add=NET_ADMIN</td>
<td markdown="span">Parametro que necesita DNSMASQ
</td>
<tr bgcolor="#F8F8F8">
<td markdown="span">--dns 127.0.0.1</td>
<td markdown="span">Ip interna
</td>
<tr>
<td markdown="span">--dns 1.1.1.1</td>
<td markdown="span">DNS interno
</td>
<tr bgcolor="#F8F8F8">
<td markdown="span">--restart=unless-stopped</td>
<td markdown="span">Restart container unless it is stopped
</td>
<tr>
<td markdown="span">'pihole/pihole:latest'</td>
<td markdown="span">Imagen del contenedor
</td>
<tbody>
<table>
<br>
{% endcomment %}

# Nos conectamos por web a nuestra instancia de Pi-HOLE
* * *

Este es el aspecto que tendrá nuestra web si se ha cargado bien.

![pihole1](/blog/assets/img/pihole1.png)

Si seguimos el link o vamos directamente a la url del panel **/admin**

![pihole2](/blog/assets/img/pihole2.png)

Pinchamos en Login y metemos el password que hemos puesto en la config del contenedor

![pihole3](/blog/assets/img/pihole3.png)

Por defecto pihole viene con una blocklist extensa, pero si queremos mas, podremos añadir la lista que queramos en **settings > blocklists**

![pihole4](/blog/assets/img/pihole4.png)
