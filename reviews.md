---
layout: default
title: Paper Reviews
permalink: /reviews.html
---

Detailed reviews and summaries of interesting AI papers.

<ul class="post-list">
  {% for review in site.reviews %}
    <li>
      <a class="post-link" href="{{ review.url | relative_url }}">{{ review.title }}</a>
      <span class="post-date">{{ review.date | date: "%b %-d, %Y" }}</span>
    </li>
  {% endfor %}
</ul>

