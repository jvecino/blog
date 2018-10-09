---
layout: default
---
<center><img src="/blog/assets/img/unraidlogo.jpg" height="100x" width="30%"></center>
* * *

><center>unRAID is software for storing and managing digital files on a mass-storage server.  In more technical terms, unRAID® is an embedded Network Attached Storage (NAS) server operating system.  It was >specifically designed for digital media storage (e.g., videos, photos, music, & movies).  It allows you to build an array of hard drives and share the data from those drives across the local network >(typically within a house or business).  Importantly, it protects all the data on the drives if one should fail.</center>

<h1>Unraid Posts</h1>

<div class="home">
  {%- if page.title -%}
    <h1 class="page-heading">{{ page.title }}</h1>
  {%- endif -%}

    {%- if site.posts.size > 0 -%}
    <h2 class="post-list-heading">{{ page.list_title | default: "Posts" }}</h2>
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
