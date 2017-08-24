---
layout: archive
permalink: /presentaciones2/
title: "Presentaciones"
author_profile: true
---

{% include base_path %}
{% include group-by-array collection=site.posts field="categories" %}

  {% for post in posts %}
    {% if post.categories contains "Presentaciones" %}
      {% include archive-single.html %}
    {% endif %}
  {% endfor %}
