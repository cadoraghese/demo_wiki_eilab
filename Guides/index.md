---
layout: default
title: Guides
---

# Guides

Browse by category or view individual guides available at this level.

## Categories

<ul>
  {% assign directories = "" | split: "" %}
  {% for page in site.pages %}
    {% if page.path | startswith: 'Guides/' %}
      {% if page.dir != '/Guides/' %}
        {% assign subdir_name = page.dir | remove_first: '/Guides/' | split: '/' | first %}
        {% assign directories = directories | push: subdir_name %}
      {% endif %}
    {% endif %}
  {% endfor %}
  
  {% assign unique_directories = directories | uniq | sort %}
  
  {% for dir in unique_directories %}
    <li>
      <h3>📂 <a href="{{ site.baseurl }}/Guides/{{ dir }}/">{{ dir | capitalize }}</a></h3>
      <p>Guides related to {{ dir | capitalize }}.</p>
    </li>
  {% endfor %}
</ul>

---

## Top-Level Guides

<ul>
  {% comment %}
    The line below has been updated. We've added a filter:
    'where_exp: "item", "item.title"'
    This safely removes any pages that are missing a title BEFORE attempting to sort.
  {% endcomment %}
  {% assign files = site.pages | where_exp: "item", "item.dir == '/Guides/'" | where_exp: "item", "item.name != 'index.md'" | where_exp: "item", "item.title" | sort: "title" %}
  {% for file in files %}
    <li>
      <h3>📄 <a href="{{ file.url | relative_url }}">{{ file.title }}</a></h3>
    </li>
  {% endfor %}
</ul>
