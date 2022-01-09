---
layout: page
title: Archive
---

<ul class="archive">
    {% assign notes = site.notes | sort: "title" %}
    {% for note in notes %}
        <li>
            <a href="{{ note.url }}{%- if site.use_html_extension -%}.html{%- endif -%}" class="internal-link">
                {{note.title}}
            </a>
            {% if note.category != null %} in {{note.category}}{% endif %} 
            <span>
                {% if note.date_updated %}
                    ({{ note.date_updated | date: "%d %b %Y" }})
                {% else %}
                    ({{ note.last_modified_at | date: "%d %b %Y" }})
                {% endif %}
            </span>
            <p>
                {{ note.excerpt | strip_html | truncate: 60, "..." }}
            </p>
        </li>
    {% endfor %}
</ul>