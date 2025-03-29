---
layout: default
permalink: /feed/
title: Feed
nav: true
nav_order: 2
pagination:
  enabled: true
  collection: feed_posts
  permalink: /feed/page/:num/
  per_page: 10
  sort_field: date
  sort_reverse: true
  trail:
    before: 1
    after: 3
---

<div class="feed">

  <h1>My Daily Feed</h1>
  <p>Sharing my daily activities and thoughts.</p>

  <ul class="feed-list">

    {% if page.pagination.enabled %}
      {% assign feedlist = paginator.posts %}
    {% else %}
      {% assign feedlist = site.feed_posts %}
    {% endif %}

    {% for post in feedlist %}
    <li class="feed-item">
      <div class="feed-content">
        <h3>
          <a class="feed-title" href="{{ post.url | relative_url }}">{{ post.title }}</a>
        </h3>
        <p>{{ post.content | strip_html | truncatewords: 50 }}</p>
        <p class="feed-meta">
          <i class="fa-solid fa-calendar fa-sm"></i> {{ post.date | date: '%B %d, %Y' }}
          {% if post.tags %}
          &nbsp; &middot; &nbsp;
          {% for tag in post.tags %}
            <a href="{{ tag | slugify | prepend: '/feed/tag/' | prepend: site.baseurl}}">
              <i class="fa-solid fa-hashtag fa-sm"></i> {{ tag }}</a>
              {% unless forloop.last %}
                &nbsp;
              {% endunless %}
          {% endfor %}
          {% endif %}
        </p>
      </div>
    </li>
    {% endfor %}

  </ul>

  {% if page.pagination.enabled %}
    {% include pagination.liquid %}
  {% endif %}

</div>