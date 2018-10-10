---
layout: default
---

<h1>Unraid</h1>
* * *

><p>Unraid es un software para almacenar y manejar archivos digitales en un servidor de almacenamiento masivo. En detalles mas técnicos, unRAID es un sistema operativo de servidor de almacenamiento conectado en red embedido (NAS). Ha sido especialmente diseñado para almacenamiento de media digital (ej., videos, fotos, música y peliculas).</p>
>
><p>Te permite crear un array de discos duros y compartir los datos de esos discos a través de la red local (normalmente en una casa o negocio). Más importante aún, protege toda la información de los discos en caso de que alguno de ellos falle.</p>

<h2>Posts de Unraid</h2>
* * *
<div class="home">
  {%- if page.title -%}
    <h1 class="page-heading">{{ page.title }}</h1>
  {%- endif -%}

    {%- if site.posts.size > 0 -%}
    {% comment %}<h2 class="post-list-heading">{{ page.list_title | default: "Posts" }}</h2>{% endcomment %}
    <ul class="post-list">
      {%- for post in site.categories.unraid -%}
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

    <p class="rss-subscribe">subscribe <a href="{{ "/feed.xml" | relative_url }}">via RSS</a></p>
  {%- endif -%}

</div>
