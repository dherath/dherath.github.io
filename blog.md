---
layout: page
title: Blog Posts
permalink : /blog/
---

Hi All! Thank you for stopping by, as you probably noticed down below is a list of my blog posts that I have written over time. I try to be periodic in my writing but usually it doesn't work out so most of the time I tend to churn out a new post every three or four months. Most of what I write are related to **Computer Science** and the research work I do. Happy reading !!!

<br>

<ul class="post-list">
    {% for post in site.posts %}
      <!--{% unless post.next %}
        <h3 class="category-title">{{ post.date | date: '%Y' }}</h3>
      {% else %}
        {% capture year %}{{ post.date | date: '%Y' }}{% endcapture %}
        {% capture nyear %}{{ post.next.date | date: '%Y' }}{% endcapture %}
        {% if year != nyear %}
          <h3 class="category-title">{{ post.date | date: '%Y' }}</h3>
        {% endif %}
      {% endunless %}-->
      <article class="post-item">
        <span class="post-meta date-label">{{ post.date | date: "%b %d %Y" }}</span>
        <div class="article-title"><a class="post-link" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a></div>
      </article>
    {% endfor %}
</ul>
