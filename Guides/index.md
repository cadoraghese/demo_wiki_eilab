---
layout: default
title: Guides Category Debug
---

# Guides Category Debug

<p>This page will show the raw list of directory names being collected right before the sort filter that is causing the error.</p>

<hr>

{% assign directories = "" | split: "" %}
{% for page in site.pages %}
  {% if page.path | startswith: 'Guides/' %}
    {% if page.dir != '/Guides/' %}
      {% assign subdir_name = page.dir | remove_first: '/Guides/' | split: '/' | first %}
      {% assign directories = directories | push: subdir_name %}
    {% endif %}
  {% endif %}
{% endfor %}

<p><strong>Raw 'directories' array before `uniq` and `sort`:</strong></p>
<pre><code>{{ directories | inspect }}</code></pre>
