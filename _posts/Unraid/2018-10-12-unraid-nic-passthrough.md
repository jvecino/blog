---
layout: default
title:  "Como hacer passthrough the una NIC a una VM en Unraid"
categories: unraid
---
<h1>Como hacer passthrough the una NIC a una VM en Unraid</h1>
* * *
<h5><em>Acrónimos: VM (máquina virtual), NIC (tarjeta de red)</em></h5>

<p>A la hora de crear una VM, si el rendimiento es una prioridad, la VM necesita tener acceso directo a todo el hardware posible de nuestro servidor.</p>

<p>Con esto nos quitamos los problemas que pueden surgir de la virtualización dado que este hardware no estará emulado. Conseguiremos un rendimiento máximo del componente y evitaremos que unraid intervenga en el funcionamiento de este.</p>

<p>Para este proposito necesitamos unraid y una tarjeta de red que vayamos a dedicar a una o varias VM (en el caso de que tenga mas de un puerto)</p>

<p>Cada puerto se puede asignar individualmente a una VM.</p>

Vamos allá:

<h2>Asegurarse de que nuestra cpu admita IOMMU</h2>
* * *
![iommu](/blog/assets/img/nic-pass-1.png)

<h2>Verificar si nuestra NIC esta en un grupo de IOMMU separado</h2>
* * *
![iommu](/blog/assets/img/nic-pass-2.png)

En nuestro caso no lo está

Para solucionar esto hay que ir a **Settings** > **Vm Manager** > **PCIe ACS override** > **Enable**

<em>Nota: Antes tendremos que parar el servicio de VM desde el VM manager</em>

Nos pedirá reiniciar el servidor.

<h2>Identificar nuestra NIC en Unraid</h2>
* * *
Abrimos una terminal en el servidor y ejecutamos

<code>root@Tower:~#lspci -n</code>

>09:00.0 Ethernet controller: Intel Corporation 82571EB/82571GB Gigabit Ethernet Controller (Copper) (rev 06)<br>
>09:00.1 Ethernet controller: Intel Corporation 82571EB/82571GB Gigabit Ethernet Controller (Copper) (rev 06)<br>
>0a:00.1 Ethernet controller: Intel Corporation 82571EB/82571GB Gigabit Ethernet Controller (Copper) (rev 06)<br>
>0a:00.0 Ethernet controller: Intel Corporation 82571EB/82571GB Gigabit Ethernet Controller (Copper) (rev 06)<br>

Nos saldrá nuestra NIC y todo el demás hardware.

En nuestro caso es una nic de 4 puertos.

Ejecutamos

<code>root@Tower:~# lspci -n</code>

>09:00.0 0200: 8086:10bc (rev 06)<br>
>09:00.1 0200: 8086:10bc (rev 06)<br>
>0a:00.0 0200: 8086:10bc (rev 06)<br>
>0a:00.1 0200: 8086:10bc (rev 06)<br>

Buscamos los ids que coincidan y el dato que necesitamos es el de la parte derecha. En nuestro caso **8086:10bc**

<h2>Decirle a Unraid que no use la NIC</h2>
* * *
Nos vamos a **Main** > **Flash** > **Syslinux Configuration**

Y en label UNRAID OS cambiamos la linea de append y agregamos 'pci-stub.ids=8086:10bc':

>label unRAID OS<br>
>&nbsp;&nbsp;  menu default<br>
>&nbsp;&nbsp;  kernel /bzimage<br>
>&nbsp;&nbsp;  append pci-stub.ids=8086:10bc initrd=/bzroot<br>   

Guardamos y reiniciamos el servidor.

Con esto a la hora de crear una VM ya podremos seleccionar del listado la NIC para asignarla directamente.

Este mismo proceso se puede usar para hacer passthrough a otros componentes y periféricos, como GPUs, hubs usb, discos duros etc...
