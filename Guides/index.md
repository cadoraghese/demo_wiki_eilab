---
layout: default
title: Guides Debug
---

# Guides Debug Mode

<p>The build log shows an error when sorting pages by title. This page will list every file that Jekyll is trying to sort, and will point out the one that is missing a title.</p>

<hr>

<h2>Files being processed in the 'Guides' folder:</h2>

<ol>
  {% assign files_to_debug = site.pages | where_exp: "item", "item.dir == '/Guides/'" | where_exp: "item", "item.name != 'index.md'" %}
  {% for file in files_to_debug %}
    <li>
      <strong>File Path:</strong> <code>{{ file.path }}</code><br>
      <strong>File Name:</strong> <code>{{ file.name }}</code><br>
      <strong>Extracted Title:</strong> <code>{{ file.title | default: "NIL! <-- THIS IS THE PROBLEM FILE" }}</code>
    </li>
  {% endfor %}
</ol>
