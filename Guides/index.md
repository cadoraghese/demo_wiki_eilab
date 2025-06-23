---
layout: default
title: All Guides
---

# All Guides

Here is a list of all available guides, sorted alphabetically by title.

<ul>
  {% comment %}
    This code finds all pages within the 'Guides/' folder and any subfolders.
    It excludes this index page itself.
    Then, it sorts the results alphabetically based on the page's title.
  {% endcomment %}
  {% assign guides = site.pages | where_exp: "item", "item.path contains 'Guides/'" | where_exp: "item", "item.name != 'index.md'" | sort: "title" %}
  {% for guide in guides %}
    <li>
      <h3><a href="{{ guide.url | relative_url }}">{{ guide.title }}</a></h3>
    </li>
  {% endfor %}
</ul>
