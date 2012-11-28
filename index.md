---
layout: page
title: 索引
tagline: Supporting tagline
---
{% include JB/setup %}

<ul class="posts">
  {% for post in site.posts %}
    {% if forloop.first %}
      <li>
        <h2>
          <a href="{{ post.url }}">{{ post.title }}</a>
        </h2>

        {{ post.content }}
      </li>
    {% else %}
      <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
    {% endif %}
  {% endfor %}
</ul>

