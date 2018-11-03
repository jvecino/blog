---
layout: default
title:  "Instalar Pihole y Pivpn en Raspberry Pi"
categories: raspberry
---

## Requisitos:

* Raspberry pi (Cualquier version)
* microsd (2gb+)
* Cable Ethernet
* Cable microusb +

# Preparamos la SD y instalamos Raspbian.
* * *

Insertamos la SD. Si no tenemos lector de tarjetas sd en nuestro pc, nos valemos de cualquier adaptador de sd a usb.

![pihole1](/blog/assets/img/piholerasp1.png)

Sacamos un CMD (Windows + R) y ejecutamos Diskpart

Seguimos las siguientes instrucciones:

![pihole2](/blog/assets/img/piholerasp2.png)

Descargamos Raspbian stretch lite (sin escritorio) desde la página oficial de raspbian [AQUI](https://www.raspberrypi.org/downloads/raspbian/) y lo descomprimimos.

![pihole3](/blog/assets/img/piholerasp3.png)

Abrimos el programa Win32 Disk Imager y seleccionamos nuestra imagen. Nos lo descargamos gratuitamente desde [AQUI](https://sourceforge.net/projects/win32diskimager/)
![pihole4](/blog/assets/img/piholerasp4.png)

Le damos a write para escribirla en la SD.

![pihole5](/blog/assets/img/piholerasp5.png)

Ya tenemos nuestra SD preparada!

![pihole6](/blog/assets/img/piholerasp6.png)

**Importante**: Si queremos conectarnos a nuestra raspberry por ssh sin necesidad de un monitor, previamente tendremos que crear un archivo vacio sin extensión que se llame "usb" en la raiz de nuestra SD después de haberle instalado Raspbian, así:

![pihole7](/blog/assets/img/piholerasp7.png)

# Instalamos Pihole en nuestro Raspbian.
* * *


































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
