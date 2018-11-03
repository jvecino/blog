---
layout: default
permalink: /rclone
---

<h1>Rclone</h1>
* * *

><p>Rclone es un programa de línea de comando utilizado para sincronizar archivos y carpetas desde múltiples servicios de almacenamiento en la nube, incluyendo Amazon Drive, Amazon S3, Google Drive, Google Cloud Storage, Dropbox, OneDrive de Microsoft, almacenamiento de blobs de Microsoft Azure, ownCloud, Nextcloud, DigitalOcean Spaces y muchos otros (WebDAV y SFTP también son compatibles). </p>La herramienta es software gratuito y de código abierto, y está disponible en múltiples plataformas, incluidas Linux, Windows, macOS, BSD y Solaris.

<h2>Posts de Rclone</h2>
* * *
<div class="home">
  {%- if page.title -%}
    <h1 class="page-heading">{{ page.title }}</h1>
  {%- endif -%}

    {%- if site.posts.size > 0 -%}
   {% comment %}<h2 class="post-list-heading">{{ page.list_title | default: "Posts" }}</h2>{% endcomment %}
    <ul class="post-list">
      {%- for post in site.categories.rclone -%}
      <li>
        {%- assign date_format = site.minima.date_format | default: "%b %-d, %Y" -%}
        <span class="post-meta">{{ post.date | date: date_format }}</span>
        <h3>
          <a class="post-link" href="{{ post.url | relative_url }}">
            {{ post.title | escape }}
          </a>
        </h3>
        {%- if site.show_excerpts -%}
          {{ post.excerpt }}
        {%- endif -%}
      </li>
      {%- endfor -%}
    </ul>

    <p class="rss-subscribe">Subscribete <a href="{{ "/feed.xml" | relative_url }}">via RSS</a></p>
  {%- endif -%}

</div>
