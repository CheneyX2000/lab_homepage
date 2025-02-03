---
layout: page
title_nav: team
title: Team
permalink: /team
nav: true
nav_order: 1
---

<style>
.team-member-image {
  width: 100%; 
  height: 200px; 
  object-fit: cover; 
}
.card {
  margin: 1rem; 
  display: flex;
  flex-direction: column;
  height: 100%; 
}
.card-body {
  flex-grow: 1; 
}
</style>

{% assign groups = "Faculty,Postdoc,PhD Student,Visiting Scholar,Visiting Student,Research Assistant" | split: "," %}
{% for group in groups %}
{% assign group_members = site.members | where_exp: "member", "member.group == group" %}
{% if group_members.size > 0 %}

<h2 style="padding-top: 30px;">{{ group }}</h2>
    {% assign members = site.members | sort: "lastname" | where: "group", group %}
    {% for member in members %}
<div class="card {% if member.inline == false %}hoverable{% endif %}" style="margin-bottom: 1rem;">
    <div class="row no-gutters">
        <div class="col-sm-4 col-md-3">
            {% assign img_src = member.profile.image | default: 'husky2.jpg' %}
            <img class="team-member-image" src="{{ '/assets/img/' | append: img_src | relative_url }}" alt="{{ member.profile.name | default: 'Unknown' }}" />
        </div>
        <div class="team col-sm-8 col-md-9">
            <div class="card-body">
                    {% if member.inline == false %}
                    {% if member.profile.website %}
                    <a href="{{ member.profile.website }}">
                    {% endif %}
                    {% endif %}
                    <h5 class="card-title">{{ member.profile.name | default: 'Unknown' }}</h5>
                    {% if member.profile.position %}<h6 class="card-subtitle mb-2 text-muted">{{ member.profile.position }}</h6>{% endif %}
                    <p class="card-text">
                        {{ member.teaser }}
                    </p>
                    {% if member.inline == false and member.profile.website %}</a>{% endif %}
                    {% if member.profile.email %}
                        <a href="mailto:{{ member.profile.email }}" class="card-link"><i class="fas fa-envelope"></i></a>
                    {% endif %}
                    {% if member.profile.phone %}
                        <a href="tel:{{ member.profile.phone }}" class="card-link"><i class="fas fa-phone"></i></a>
                    {% endif %}
                    {% if member.profile.orcid %}
                        <a href="https://orcid.org/{{ member.profile.orcid }}" class="card-link" target="_blank"><i class="fab fa-orcid"></i></a>
                    {% endif %}
                    {% if member.profile.twitter %}
                        <a href="https://twitter.com/{{ member.profile.twitter }}" class="card-link" target="_blank"><i class="fab fa-twitter"></i></a>
                    {% endif %}
                    {% if member.profile.github %}
                        <a href="https://github.com/{{ member.profile.github }}" class="card-link" target="_blank"><i class="fab fa-github"></i></a>
                    {% endif %}
                    {% if member.profile.website %}
                        <a href="{{ member.profile.website }}" class="card-link" target="_blank"><i class="fas fa-globe"></i></a>
                    {% endif %}
                    <p class="card-text">
                        <small class="test-muted"><i class="fas fa-thumbtack"></i> {{ member.profile.address | default: 'No Address' | replace: '<br />', ', ' }}</small>
                    </p>
                </div>
        </div>
    </div>
</div>
    {% endfor %}
{% endif %}
{% endfor %}
