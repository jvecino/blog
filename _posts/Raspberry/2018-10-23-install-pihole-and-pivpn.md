---
layout: default
title:  "Instalar Pihole y Pivpn en Raspberry Pi"
categories: raspberry
---

test


Originalmente Escrito por Valný  Ver Mensaje
Ya que esto se ha convertido en una quasi plataforma comparto por aquí un script para reconectar la red cuando se cae por si lo quieres añadir al OP. En mi caso la Raspberry arranca mucho más rápido que mi router y como detecta que no se puede conectar pues así se queda, como la tengo en modo headless lo único que puedo hacer es reiniciarla a la fuerza una vez el router ya está funcionando para que se conecte y empiece a funcionar bien.

Creamos un script vacio con nano dentro de /usr/local/bin/ que se llamará wifi_check.sh:
Código:
sudo nano /usr/local/bin/http://wifi_check.shEl contenido del script es el siguiente:
Código:
#!/bin/bash

SERVER=8.8.8.8

ping -c2 ${SERVER} > /dev/null

if [ $? != 0 ]
then
    sudo ifconfig wlan0 down
    sudo ifconfig wlan0 up
fi
Resumiendo manda dos pings al DNS de Google (8.8.8.8) si el resultado es distinto a 0 significa que no ha podido contactar y entonces reinicia la interfaz inalámbrica (si lo queréis para una Raspberry conectada por cable cambiar wlan0 por eth0)

Guardamos con CTRL+O y salimos con CTRL+X.

Damos permisos de ejecución al script:
Código:
sudo chmod +x /usr/local/bin/http://wifi_check.shAhora editaremos cron para que el script se ejecute automáticamente cada 5 minutos:
Código:
sudo nano /etc/crontab
Y añadimos al final del archivo la siguiente línea:

Y ya está, si queréis probar que funciona podéis parar la red inalámbrica con:

Esto desconectará la sesión SSH (y si lo tenéis configurado como único DNS en el router también desconectará internet en general), esperad 5 minutos y tratad de conectaros a la Raspberry de nuevo, si funciona es que lo habéis hecho bien
