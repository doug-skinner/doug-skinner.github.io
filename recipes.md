---
layout: page
title: Recipes
permalink: /recipes/
---

<ul>
{% for recipe in site.recipes %}
  <li>
    <a href="{{ recipe.url }}">
      {{ recipe.name }}
    </a>
  </li>
{% endfor %}
</ul>
