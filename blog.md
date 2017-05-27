---
layout: page
title: Blog
permalink : /blog/
---


<ul class="post-list">
    {% for post in site.posts %}
      {% unless post.next %}
        <h3 class="category-title">{{ post.date | date: '%Y' }}</h3>
      {% else %}
        {% capture year %}{{ post.date | date: '%Y' }}{% endcapture %}
        {% capture nyear %}{{ post.next.date | date: '%Y' }}{% endcapture %}
        {% if year != nyear %}
          <h3 class="category-title">{{ post.date | date: '%Y' }}</h3>
        {% endif %}
      {% endunless %}
      <article class="post-item">
        <span class="post-meta date-label">{{ post.date | date: "%b %d" }}</span>
        <div class="article-title"><a class="post-link" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a></div>
      </article>
    {% endfor %}
</ul>
