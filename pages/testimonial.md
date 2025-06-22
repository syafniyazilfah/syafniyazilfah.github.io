---
layout: default
title: Testimonial
permalink: /testimonial/
weight: 3
---

<div class="card-columns m-3 mt-5">

  {% for project in site.data.testimonial %}
    <div class="wow animated fadeIn" data-wow-delay=".15s">
      <div class="card text-themed project" style="min-height: 350px; display: flex; flex-direction: column;">
        {% if project.image %}
          <img id="{{ project.name | slugify }}-img" class="card-img-top" src="{{ project.image }}" alt="{{ project.name }}" />
        {% endif %}
        <div class="card-body" style="flex: 1; display: flex; flex-direction: column;">
          <h5 id="{{ project.name | slugify }}-name" class="card-title">{{ project.name }}</h5>

          <p id="{{ project.name | slugify }}-desc" class="card-text" style="font-style: italic; font-weight: bold; font-size: 0.9rem;">
            {{ project.jabatan }}
          </p>

          <!-- Testimonial scrollable jika panjang -->
          <div style="flex: 1; overflow-y: auto; font-size: 0.85rem; color: #555;">
            <p id="{{ project.name | slugify }}-testimonial" class="card-text">
              &ldquo;{{ project.testimonial | newline_to_br }}&rdquo;
            </p>
          </div>

        </div>
      </div>
    </div>
  {% endfor %}

</div>
