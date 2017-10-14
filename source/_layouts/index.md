---
layout: default
title: Govlab Documentation
---

<main role="main" class="main-wrapper"> <!-- main content starts here -->

<aside class="sidebar">
<h1 class="main-logo">
  <img src="{{ '/images/govlab-logo-white.png' | absolute_url}}" alt="">
  Docs
</h1>
{% include sidebar.html %}
</aside>

<section class="main-content long-text docs">
  <h1 class="page-title">{{page.title}}</h1>
  {% for doc in site.docs %}
  <h1>{{doc.title}}</h1>
  {{doc.content}}
  {% endfor %}
</section>
</main>
