---
layout: single
title: Posts by Tag
permalink: /tags/
author_profile: true
classes: wide
---

<style>
  .tag-section {
    margin-bottom: 3em;
  }

  .tag-section h2 {
    margin-top: 1.5em;
    padding-bottom: 0.25em;
    border-bottom: 1px solid #ddd;
  }

  .tag-post-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
    gap: 1rem;
    margin-top: 1rem;
  }

  .tag-post-card {
    display: block;
    padding: 1rem;
    border: 1px solid #ddd;
    border-radius: 6px;
    color: inherit !important;
    text-decoration: none;
  }

  .tag-post-card:hover {
    text-decoration: none;
    border-color: #999;
  }

  .tag-post-card h3 {
    margin-top: 0;
    margin-bottom: 0.4rem;
    font-size: 1.05em;
  }

  .tag-post-card time {
    display: block;
    margin-bottom: 0.5rem;
    font-size: 0.85em;
    color: #666;
  }

  .tag-post-card p {
    margin-bottom: 0;
    font-size: 0.9em;
  }
</style>

{% assign tags_sorted = site.tags | sort %}

{% for tag in tags_sorted %}
  {% assign tag_name = tag[0] %}
  {% assign posts = tag[1] | where_exp: "post", "post.hidden != true" | sort: "date" | reverse %}

  <section class="tag-section" id="{{ tag_name | slugify }}">
    <h2>{{ tag_name }}</h2>
    <div class="tag-post-grid">
      {% for post in posts %}
        <div class="tag-post-card">
          <a class="tag-post-main-link" href="{{ post.url | relative_url }}">
            <h3>{{ post.title }}</h3>
          </a>
          {% if post.date %}
            <time datetime="{{ post.date | date_to_xmlschema }}">
              {{ post.date | date: "%B %-d, %Y" }}
            </time>
          {% endif %}
          {% if post.tags %}
            <div class="post-tags">
              {% for tag in post.tags %}
                <a class="post-tag" href="{{ '/tags/#' | append: tag | slugify | relative_url }}">
                  {{ tag }}
                </a>
              {% endfor %}
            </div>
          {% endif %}
          {% if post.excerpt %}
            <p>{{ post.excerpt | markdownify | strip_html | truncate: 130 }}</p>
          {% endif %}
        </div>
      {% endfor %}
    </div>
  </section>
{% endfor %}
