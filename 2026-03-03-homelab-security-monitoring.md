---
layout: default
---

<h1>{{ page.title }}</h1>
<p class="tag-description">Posts tagged with <strong>{{ page.tag }}</strong></p>

<a href="/blog/" class="back-link">← Back to all posts</a>

<div class="posts-container">
  {% assign filtered_posts = site.posts | where_exp: "post", "post.tags contains page.tag" %}
  {% for post in filtered_posts %}
    <article class="post-card">
      <div class="post-meta">
        <span class="post-date">{{ post.date | date: "%B %d, %Y" }}</span>
        {% if post.category %}
          <span class="post-category">{{ post.category }}</span>
        {% endif %}
      </div>
      <h2 class="post-title">
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      </h2>
      <p class="post-excerpt">{{ post.excerpt | strip_html | truncate: 160 }}</p>
      <div class="post-tags">
        {% for tag in post.tags %}
          <span class="tag {% if tag == page.tag %}active{% endif %}">{{ tag }}</span>
        {% endfor %}
      </div>
    </article>
  {% endfor %}
</div>

{% if filtered_posts.size == 0 %}
<p class="no-posts">No posts with this tag yet.</p>
{% endif %}
