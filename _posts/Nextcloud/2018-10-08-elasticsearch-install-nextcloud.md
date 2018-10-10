---
layout: default
title:  "ElasticSearch install on Nextcloud"
categories: nextcloud
---
<h1>ElasticSearch install on Nextcloud</h1>
* * *

<p><em>ElasticSearch is an open source, RESTful search engine built on top of Apache Lucene and released under an Apache license. It is Java-based and can search and index document files in diverse formats.</em></p>

<em>It allows fast searches inside Nextcloud from various sources like, local files, external storage, bookmarks etc...</em>

<em>Tested in **ubuntu 16.04**</em>

Here we go!

<h2>Install from Nextcloud appstore</h2>

Login to your Nextcloud server and go to Applications and install the plugin.

![nextclouddownload](/blog/assets/img/elasticsearchdownload.png)

<h2>Install Java</h2>

<code>sudo add-apt-repository ppa:webupd8team/java<br>
sudo apt-get update<br>
sudo apt update && sudo apt install oracle-java8-installer && sudo apt install oracle-java8-set-default</code><br>

<h2>Install and enable elasticsearch</h2>

<code>wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -<br><br> echo "deb https://artifacts.elastic.co/packages/6.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-6.x.list<br><br>
sudo apt update && sudo apt install elasticsearch<br>
sudo systemctl daemon-reload<br>
sudo systemctl enable elasticsearch<br>
sudo systemctl start elasticsearch</code><br>

<h2>Install elasticsearch ingest-attachment plugin</h2>
<em>so Nextcloud can extract file attachments in common formats</em>

<code>sudo /usr/share/elasticsearch/bin/elasticsearch-plugin install ingest-attachment</code><br>

<h2>Set elasticsearch to listen to localhost only</h2>
<code>sudo nano /etc/elasticsearch/elasticsearch.yml</code><br>
and add <code>network.host: 127.0.0.1</code><br>

<h2>Restart elasticsearch</h2>
<code>sudo systemctl restart elasticsearch</code><br>

<h2>Check if elasticsearch is running</h2>
<code>sudo curl 'localhost:9200/?pretty'<br>

<h2>Configure Nextcloud</h2>
Go to **Applications** > **fulltextsearch** and change settings:

![nextcloudconfig](/blog/assets/img/elasticsearchconfig.png)

<h2>Index Everything first</h2>
<code>sudo -u www-data php /var/www/html/nextcloud/occ fulltextsearch:index</code>

<h2>Enjoy!</h2>

 {% comment %}{% youtube "https://www.youtube.com/watch?v=5WsBQZlt9FM" %}{% endcomment %}
