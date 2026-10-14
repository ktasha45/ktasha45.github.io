---
layout: index
title: flogging
---

{% assign sorted_cats = site.categories | sort %}
{% for tag in sorted_cats %}
  <h2>{{ tag[0] }}</h2>
  <ul class="post-list">
    {% for post in tag[1] %}
      <li>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
        {% if post.date %}
          <time class="page_date" datetime="{{ post.date | date: '%Y-%m-%d' }}">{{ post.date | date: '%Y.%m.%d' }}</time>
        {% endif %}
      </li>
    {% endfor %}
  </ul>
{% endfor %}
