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

---

## Top-Level Guides (DEBUG MODE)

<p><strong>Finding the file with no title...</strong></p>
<ol>
  {% assign files_to_debug = site.pages | where_exp: "item", "item.dir == '/Guides/'" | where_exp: "item", "item.name != 'index.md'" %}
  {% for file in files_to_debug %}
    <li>
      <strong>File Path:</strong> <code>{{ file.path }}</code><br>
      <strong>Title:</strong> <code>{{ file.title | default: "NIL! <-- THIS IS THE PROBLEM FILE" }}</code>
    </li>
  {% endfor %}
</ol>
