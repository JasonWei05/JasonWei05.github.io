---
layout: default
title: Paper Reviews
permalink: /reviews.html
---

Detailed reviews and summaries of interesting AI papers.

<ul class="post-list">
  {% for review in site.reviews %}
    <li>
      <div class="post-info">
        <a class="post-link" href="{{ review.url | relative_url }}">{{ review.title }}</a>
        {% if review.tags %}
          <span class="post-tags">
            {% for tag in review.tags %}
              <span class="tag">{{ tag }}</span>
            {% endfor %}
          </span>
        {% endif %}
      </div>
      <span class="post-date">{{ review.date | date: "%b %-d, %Y" }}</span>
    </li>
  {% endfor %}
</ul>
