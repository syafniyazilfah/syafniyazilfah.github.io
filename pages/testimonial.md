---
layout: default
title: Testimonial
permalink: /testimonial/
weight: 3
---

<div class="card-columns m-3 mt-5">

  {% for project in site.data.testimonial %}
    <div class="wow animated fadeIn" data-wow-delay=".15s">
      <div class="card text-themed project">
        {% if project.image %}
          <img id="{{ project.name | slugify }}-img" class="card-img-top" src="{{ project.image }}" alt="{{ project.name }}" />
        {% endif %}
        <div class="card-body">
          <h5 id="{{ project.name | slugify }}-name" class="card-title">{{ project.name }}</h5>
          <p id="{{ project.name | slugify }}-desc" class="card-text" style="font-style: italic; font-weight: bold; font-size: 0.9rem;">{{ project.jabatan }}</p>
          <p id="{{ project.name | slugify }}-testimonial" class="card-text" style="font-size: 0.85rem; color: #555;">&ldquo;{{ project.testimonial | newline_to_br }}&rdquo;
          </p>
        </div>
      </div>
    </div>
  {% endfor %}

</div>
