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
      This 'if' statement is the crucial part. 
      'page.path startswith 'Guides/'' ensures we ONLY look in the root /Guides folder.
      It will ignore a path like 'Old-Projects/Guides/'.
    {% endcomment %}
    {% if page.path startswith 'Guides/' and page.dir != '/Guides/' %}
      {% assign subdir_name = page.dir | remove_first: '/Guides/' | split: '/' | first %}
      {% assign directories = directories | push: subdir_name %}
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
    Part 2: This section was already correct because 'item.dir == "/Guides/"' is very specific
    and only matches the top-level directory. No changes are needed here.
  {% endcomment %}
  {% assign files = site.pages | where_exp: "item", "item.dir == '/Guides/'" | where_exp: "item", "item.name != 'index.md'" | sort: "title" %}
  {% for file in files %}
    <li>
      <h3>📄 <a href="{{ file.url | relative_url }}">{{ file.title }}</a></h3>
    </li>
  {% endfor %}
</ul>
