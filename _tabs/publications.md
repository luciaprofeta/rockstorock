---
title: Publications
icon: fas fa-book-open
order: 3
permalink: /publications/
---

Below is a selection of my publications, grouped by type.  
For a complete, always-up-to-date list, see my
[Google Scholar profile](https://scholar.google.com/citations?user=_kWTLm4AAAAJ&hl=en).

{% assign groups = site.data.publications | group_by: "type" %}
{% assign sorted_groups = groups | sort: "name" %}

{% for group in sorted_groups %}
<section class="pub-section" aria-labelledby="pub-type-{{ forloop.index }}">
  <h2 id="pub-type-{{ forloop.index }}">{{ group.name }}</h2>

  {% assign items = group.items | sort: "year" | reverse %}

  <ul class="pub-list">
  {% for pub in items %}
    <li class="pub-item">
      <span class="pub-year">{{ pub.year }}</span>
      {% if pub.authors %}
        <span class="pub-authors">{{ pub.authors }}.</span>
      {% endif %}
      {% if pub.title %}
        <strong class="pub-title">{{ pub.title }}</strong>
      {% endif %}
      {% if pub.venue %}
        <em class="pub-venue"> {{ pub.venue }}</em>
      {% endif %}
      {% if pub.volume %}
        <span class="pub-volume"> {{ pub.volume }}</span>
      {% endif %}
      {% if pub.pages %}
        <span class="pub-pages">, {{ pub.pages }}</span>
      {% endif %}
      {% if pub.doi %}
        <span class="pub-doi"> —
          <a href="https://doi.org/{{ pub.doi }}" target="_blank" rel="noopener">
            doi: {{ pub.doi }}
          </a>
        </span>
      {% endif %}
      {% if pub.url and pub.doi == nil %}
        <span class="pub-link"> —
          <a href="{{ pub.url }}" target="_blank" rel="noopener">
            view
          </a>
        </span>
      {% endif %}
    </li>
  {% endfor %}
  </ul>
</section>
{% endfor %}
