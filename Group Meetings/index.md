---
layout: default
title: All Group Meetings
---

# All Group Meetings

Here is a list of all Group Meetings, with the most recent first.

<ul>
  {% comment %}
    This code finds all pages in the /Group Meetings/ directory,
    sorts them by filename in reverse order (newest first),
    and then creates a list of links.
  {% endcomment %}
  {% assign group_meetings = site.pages | where_exp: "item", "item.dir == '/Group Meetings/'" | where_exp: "item", "item.name != 'index.md'" | sort: 'name' | reverse %}
  {% for group_meeting in group_meetings %}
    <li>
      <h3><a href="{{ group_meeting.url | relative_url }}">{{ group_meeting.title }}</a></h3>
    </li>
  {% endfor %}
</ul>
