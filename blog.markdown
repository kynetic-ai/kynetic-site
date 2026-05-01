---
layout: page
title: Blog
permalink: /blog/
---

<p class="blog-intro">Technical notes, experiment results, and reflections from the lab.</p>

{%- if site.posts.size > 0 -%}
<ul class="post-list">
  {%- for post in site.posts -%}
  <li>
    {%- assign date_format = site.minima.date_format | default: "%b %-d, %Y" -%}
    <span class="post-meta">{{ post.date | date: date_format }}</span>
    <h3>
      <a class="post-link" href="{{ post.url | relative_url }}">{{ post.title | escape }}</a>
    </h3>
    {%- if site.show_excerpts -%}
      <p class="post-excerpt">{{ post.excerpt | strip_html | truncatewords: 75 }}</p>
    {%- endif -%}
  </li>
  {%- endfor -%}
</ul>

<p class="rss-subscribe">Subscribe <a href="{{ "/feed.xml" | relative_url }}">via RSS</a></p>
{%- else -%}
<p>No posts yet. Check back soon.</p>
{%- endif -%}
