---
layout: default
---

<h1>Nextcloud</h1>
* * *
><p>Nextcloud es una serie de programas cliente-servidor con el objetivo de crear servicio de alojamiento de archivos. </p>
>
><p>Su funcionalidad es similar al software Dropbox, aunque Nextcloud es de tipo código abierto, permitiendo a quien lo desee instalarlo en un servidor privado. Su arquitectura abierta permite añadir funcionalidad al servidor en forma de aplicaciones. </p>
>
><p>Nextcloud es un proyecto paralelo de ownCloud que también es un software de servicio de alojamiento en la nube.</p>

<h2>Posts de Nextcloud</h2>
* * *
<div class="home">
  {%- if page.title -%}
    <h1 class="page-heading">{{ page.title }}</h1>
  {%- endif -%}

    {%- if site.posts.size > 0 -%}
   {% comment %}<h2 class="post-list-heading">{{ page.list_title | default: "Posts" }}</h2>{% endcomment %}
    <ul class="post-list">
      {%- for post in site.categories.nextcloud -%}
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
