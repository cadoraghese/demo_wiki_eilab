---
layout: default
title: All Updates
---

# All Updates

Here is a list of all updates, with the most recent first.

<ul>
  {% comment %}
    This code finds all pages in the /Updates/ directory,
    sorts them by filename in reverse order (newest first),
    and then creates a list of links.
  {% endcomment %}
  {% assign updates = site.pages | where_exp: "item", "item.dir == '/Updates/'" | where_exp: "item", "item.name != 'index.md'" | sort: 'name' | reverse %}
  {% for update in updates %}
    <li>
      <h3><a href="{{ update.url | relative_url }}">{{ update.title }}</a></h3>
    </li>
  {% endfor %}
</ul>
