---
layout: default
title: Testimonial
permalink: /testimonial/
weight: 3
---

<style>
  .linkedin-icon {
    color: #999; /* abu-abu default */
    transition: color 0.3s ease;
  }

  .linkedin-icon:hover {
    color: #007bb5;
  }
</style>

<div class="card-columns m-3 mt-5">

  {% for project in site.data.testimonial %}
    <div class="wow animated fadeIn" data-wow-delay=".15s">
      <div class="card text-themed project">
        {% if project.image %}
          <img id="{{ project.name | slugify }}-img" class="card-img-top" src="{{ project.image }}" alt="{{ project.name }}" />
        {% endif %}
        <div class="card-body">
          <h5 id="{{ project.name | slugify }}-name" class="card-title">{{ project.name }}</h5>
          <p id="{{ project.name | slugify }}-desc" class="card-text">{{ project.jabatan }}</p>
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
