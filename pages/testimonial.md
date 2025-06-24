---
layout: default
title: Testimonial
permalink: /testimonial/
weight: 3
---

<style>
  .linkedin-icon {
    color: #999;
    transition: color 0.3s ease;
  }
  .linkedin-icon:hover {
    color: #007bb5;
  }

  .jabatan-badge {
    display: inline-block;
    font-size: 0.75rem;
    padding: 2px 8px;
    border-radius: 4px;
    margin-left: 6px;
  }
  .badge-leader { background: #007bb5; }        /* Biru */
  .badge-manager { background: #28a745; }       /* Hijau */
  .badge-senior-staff { background: #343a40; }  /* Hitam */
  .badge-staff { background: #6c757d; }         /* Abu-abu gelap */
</style>

<div class="card-columns m-3 mt-5">

  {% for project in site.data.testimonial %}
    <div class="wow animated fadeIn" data-wow-delay=".15s">
      <div class="card text-themed project">
        {% if project.image %}
          <img id="{{ project.name | slugify }}-img" class="card-img-top" src="{{ project.image }}" alt="{{ project.name }}" />
        {% endif %}
        <div class="card-body">
          <h5 id="{{ project.name | slugify }}-name" class="card-title">
            {{ project.name }}
            {% if project.level %}
              <span class="jabatan-badge 
                {% case project.level | downcase %}
                  {% when 'leader' %}badge-leader
                  {% when 'manager' %}badge-manager
                  {% when 'senior staff' %}badge-senior-staff
                  {% when 'staff' %}badge-staff
                  {% else %}badge-staff
                {% endcase %}
              ">{{ project.level }}</span>
            {% endif %}
          </h5>
          {% if project.jabatan %}
            <p id="{{ project.name | slugify }}-desc" class="card-text" style="font-size: 0.78rem; color: #555; margin-top: 0.25rem;">
              {{ project.jabatan }}
            </p>
          {% endif %}
          {% if project.linkedin %}
            <a href="https://www.linkedin.com/in/{{ project.linkedin }}" target="_blank" rel="noopener noreferrer" class="linkedin-icon" style="margin-right: 7px;">
              <i class="fab fa-linkedin-in"></i>
            </a><br>
          {% endif %}
          <p id="{{ project.name | slugify }}-testimonial" class="card-text" style="font-size: 0.84rem; margin-top: 0.5rem;">&ldquo;{{ project.testimonial | newline_to_br }}&rdquo;</p>
        </div>
      </div>
    </div>
  {% endfor %}

</div>
