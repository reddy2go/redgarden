---
layout: page
title: Archive
---

<ul class="archive">
    {% assign notes = site.notes | sort: 'note.date_updated' | reverse %}
    {% for note in site.notes %}
        <li>
            <a href="{{ note.url }}{%- if site.use_html_extension -%}.html{%- endif -%}" class="internal-link">
                {{note.title}}
            </a>
            {% if note.category != null %} in {{note.category}}{% endif %} 
            <span>
                {% if note.date_updated %}
                    ({{ note.date_updated | date: "%d %b %Y" }})
                {% elsif note.last_modified_at  %}
                    ({{ note.last_modified_at | date: "%d %b %Y" }})
                {% endif %}
            </span>
            <p>
                {{ note.excerpt | strip_html | truncate: 60, "..." }}
            </p>
        </li>
    {% endfor %}
</ul>