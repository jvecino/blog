---
layout: default
title:  "Instalar y usar Elasticsearch en nextcloud"
categories: nextcloud
---
<h1>Instalación de Elasticsearch en Nextcloud</h1>
* * *

<h5>Probado en **ubuntu 16.04**</h5>

<h2>Instalación desde la appstore de Nextcloud</h2>

Logeate en tu instancia de Nextcloud, descarga el plugin y activalo

![nextclouddownload](/blog/assets/img/elasticsearchdownload.png)

<h2>Instalar Java</h2>

<code>sudo add-apt-repository ppa:webupd8team/java<br>
sudo apt-get update<br>
sudo apt update && sudo apt install oracle-java8-installer && sudo apt install oracle-java8-set-default</code><br>

<h2>Instalar y habilitar elasticsearch</h2>

<code>wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -<br><br> echo "deb https://artifacts.elastic.co/packages/6.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-6.x.list<br><br>
sudo apt update && sudo apt install elasticsearch<br>
sudo systemctl daemon-reload<br>
sudo systemctl enable elasticsearch<br>
sudo systemctl start elasticsearch</code><br>

<h2>Instalar plugin ingest-attachment de elasticsearch</h2>
<em>Así nextcloud podrá extraer archivos adjuntos en varios formatos</em>

<code>sudo /usr/share/elasticsearch/bin/elasticsearch-plugin install ingest-attachment</code><br>

<h2>Cambiar elasticsearch para que solo escuche en localhost</h2>
<code>sudo nano /etc/elasticsearch/elasticsearch.yml</code><br>
y añade esta linea <code>network.host: 127.0.0.1</code><br>

<h2>Reiniciar elasticsearch</h2>
<code>sudo systemctl restart elasticsearch</code><br>

<h2>Comprobar que se está ejecutando elasticsearch</h2>
<code>sudo curl 'localhost:9200/?pretty'<br>

<h2>Configurar Nextcloud</h2>
Ir a **Aplicaciones** > **fulltextsearch** y cambiar la configuración a la siguiente:

![nextcloudconfig](/blog/assets/img/elasticsearchconfig.png)

<h2>Primera indexación masiva</h2>
<code>sudo -u www-data php /var/www/html/nextcloud/occ fulltextsearch:index</code>

<h2>Enjoy!</h2>

 {% comment %}{% youtube "https://www.youtube.com/watch?v=5WsBQZlt9FM" %}{% endcomment %}
