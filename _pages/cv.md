---
layout: cv
title: CV
permalink: /cv/
---


{% include career-profile.html %}

{% unless site.data.data.sidebar.education %}
{% include education.html %}
{% endunless %}

{% include experiences.html %}


{% include publications.html %}