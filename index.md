---
layout: default
---

<h2>Intro</h2>

<p>
Blunt, unsolicited advice for people trying to do useful work on AI risk.
Each guide below is a standalone page you can send to someone directly.
</p>

<h2>Guides</h2>

{% assign guides_by_category = site.guides | group_by: "category" | sort: "name" %}

{% for group in guides_by_category %}
  {% if group.name and group.name != "" %}
<h3>{{ group.name | capitalize }}</h3>
  {% else %}
<h3>Uncategorized</h3>
  {% endif %}
<ul>
  {% assign sorted = group.items | sort: "title" %}
  {% for guide in sorted %}
  <li>
    <a href="{{ guide.url | relative_url }}">{{ guide.title }}</a>{% if guide.summary %} — {{ guide.summary }}{% endif %}
  </li>
  {% endfor %}
</ul>
{% endfor %}

<h2>Contact</h2>

<p>
<a href="mailto:dan@canaryinstitute.ai">dan@canaryinstitute.ai</a>
</p>
