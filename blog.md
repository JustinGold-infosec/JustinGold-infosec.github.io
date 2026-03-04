---
layout: default
title: Blog
permalink: /blog/
---

<h1>Blog</h1>
<p class="blog-intro">Thoughts on cybersecurity, gaming, crypto, tech, and life.</p>

<div class="blog-filters">
  <div class="filter-section">
    <span class="filter-label">Categories:</span>
    <a href="{{ '/blog/' | relative_url }}" class="filter-tag{% unless page.category %} active{% endunless %}">All</a>
    {% assign categories = site.posts | map: "category" | compact | uniq | sort %}
    {% for cat in categories %}
      <a href="{{ '/blog/category/' | append: cat | downcase | relative_url }}/" class="filter-tag">{{ cat }}</a>
    {% endfor %}
  </div>
  
  <div class="filter-section">
    <span class="filter-label">Tags:</span>
    {% assign tags = site.posts | map: "tags" | join: "," | split: "," | uniq | sort %}
    {% for tag in tags %}
      {% if tag != "" %}
        <a href="{{ '/blog/tag/' | append: tag | downcase | relative_url }}/" class="filter-tag">{{ tag }}</a>
      {% endif %}
    {% endfor %}
  </div>
</div>

<div class="posts-list">
  {% for post in site.posts %}
    <a href="{{ post.url | relative_url }}" class="post-card">
      <div class="post-meta">
        <span class="post-date">{{ post.date | date: "%B %d, %Y" }}</span>
        {% if post.category %}
          <span class="post-category">{{ post.category }}</span>
        {% endif %}
      </div>
      <h2>{{ post.title }}</h2>
      <p class="post-excerpt">{{ post.excerpt | strip_html | truncate: 160 }}</p>
      {% if post.tags.size > 0 %}
      <div class="post-tags">
        {% for tag in post.tags %}
          <span class="tag">{{ tag }}</span>
        {% endfor %}
      </div>
      {% endif %}
    </a>
  {% endfor %}
</div>

{% if site.posts.size == 0 %}
<p class="no-posts">No posts yet. Check back soon!</p>
{% endif %}
