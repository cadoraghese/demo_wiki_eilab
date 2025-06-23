---
layout: default
title: Guides
---

# Guides

Browse by category or view individual guides available at this level.

## Categories

<ul>
  {% comment %}
    Step 1: Gather all potential directory names from page paths.
  {% endcomment %}
  {% assign directories = "" | split: "" %}
  {% for page in site.pages %}
    {% if page.path | startswith: 'Guides/' and page.dir != '/Guides/' %}
      {% assign subdir_name = page.dir | remove_first: '/Guides/' | split: '/' | first %}
      {% assign directories = directories | push: subdir_name %}
    {% endif %}
  {% endfor %}
  
  {% comment %}
    Step 2: Clean the list of directories before displaying them.
    - 'compact' removes all 'nil' values from the list.
    - 'where_exp' removes any blank "" values.
    - 'uniq' and 'sort' then operate on the final, clean list.
    This is the key fix that prevents the build error.
  {% endcomment %}
  {% assign unique_directories = directories | compact | where_exp: "item", "item != ''" | uniq | sort %}
  
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
    This section is for files directly inside /Guides/.
    The 'where_exp: "item", "item.title"' filter prevents errors
    if any of these files are missing a title.
  {% endcomment %}
  {% assign files = site.pages | where_exp: "item", "item.dir == '/Guides/'" | where_exp: "item", "item.name != 'index.md'" | where_exp: "item", "item.title" | sort: "title" %}
  {% for file in files %}
    <li>
      <h3>📄 <a href="{{ file.url | relative_url }}">{{ file.title }}</a></h3>
    </li>
  {% endfor %}
</ul>
