---
layout: archive
permalink: /presentaciones/
title: "Presentaciones"
author_profile: true
header:
  overlay_image: /images/servicios/vimcorsa.jpg
  overlay_filter: 0.5 # same as adding an opacity of 0.5 to a black background
---

{% include base_path %}
{% include group-by-array collection=site.posts field="categories" %}

{% for category in group_names %}
  {% assign posts = group_items[forloop.index0] %}
  {% for post in posts %}
    {% if post.categories contains "Presentaciones" %}
      {% include archive-single.html %}
    {% endif %}
  {% endfor %}
{% endfor %}
