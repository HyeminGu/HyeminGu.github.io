---
layout: page
permalink: /repositories/
title: repositories
description: Github repositories for coding works.
nav: true
nav_order: 3
---

<!-- ## GitHub users

{% if site.data.repositories.github_users %}
<div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-between align-items-center">
  {% for user in site.data.repositories.github_users %}
    {% include repository/repo_user.html username=user %}
  {% endfor %}
</div>
{% endif %}

--- 
-->

### Publication 

{% if site.data.repositories.publication_repos %}
<div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-between align-items-center">
  {% for repo in site.data.repositories.publication_repos %}
    {% include repository/repo.html repository=repo %}
  {% endfor %}
</div>
{% endif %}


### Tutorial

{% if site.data.repositories.tutorial_repos %}
<div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-between align-items-center">
  {% for repo in site.data.repositories.tutorial_repos %}
    {% include repository/repo.html repository=repo %}
  {% endfor %}
</div>
{% endif %}
