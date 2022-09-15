---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults
layout: index
title: flogging
---

## categories

{% for tag in site.categories %}
  <h2>{{ tag[0] }}</h2>
  <ul>
    {% for post in tag[1] %}
      <li>
        <a href="{{ post.url }}">{{ post.title }}</a><br>
        {% if post.date %}
          <span class="page_date">
          <i>{{ post.date | date_to_string }}</i>
          </span>
        {% endif %}
      </li>
    {% endfor %}
  </ul>
{% endfor %}


