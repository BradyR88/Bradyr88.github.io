---
layout: default
title: "Home"
---

## About me.
As for what I'm doing when I'm not programming you can probably find me climbing listening to a podcast or playing chess.

---

{% if site.show_excerpts %}
  {% include home.html %}
{% else %}
  {% include archive.html title="Posts" %}
{% endif %}
