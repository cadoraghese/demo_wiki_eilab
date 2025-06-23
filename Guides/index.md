---
layout: default
title: Guides
---

# Guides

Browse by category or view individual guides available at this level.

## Categories

<ul>
  {% comment %}
    Part 1: Find all unique subdirectories inside the top-level 'Guides/' folder.
  {% endcomment %}
  {% assign directories = "" | split: "" %}
  {% for page in site.pages %}
    {% comment %}
      The 'if' statement below was changed to use the 'startswith' FILTER
      instead of the 'startswith' OPERATOR for better Jekyll compatibility.
    {% endcomment %}
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
    Part 2: This section finds pages only in the top-level /Guides/ directory.
  {% endcomment %}
  {% assign files = site.pages | where_exp: "item", "item.dir == '/Guides/'" | where_exp: "item", "item.name != 'index.md'" | sort: "title" %}
  {% for file in files %}
    <li>
      <h3>📄 <a href="{{ file.url | relative_url }}">{{ file.title }}</a></h3>
    </li>
  {% endfor %}
</ul>
