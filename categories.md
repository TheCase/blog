---
layout: about
#image: /assets/img/blog/hydejack-9.jpg
description: >
  categories 
hide_description: true
---
<div class="tags-expo">
  <div class="tags-expo-list">
    {% assign sorted = site.categories | sort %}
    {% for cat in sorted %}
    <a href="#{{ cat[0] | slugify }}" class="post-tag">{{ cat[0] }}</a>&nbsp;&nbsp;||&nbsp;&nbsp;
    {% endfor %}
  </div>
  <hr />
  <div class="tags-expo-section">
    {% for cat in sorted %}
    <h2 id="{{ cat[0] | slugify }}">{{ cat | first }}</h2>
    <ul class="tags-expo-posts">
      {% for post in cat[1] %}
      <a class="post-title" href="{{ site.baseurl }}{{ post.url }}">
        <li>
          {{ post.title }}
          <!-- <small class="post-date">{{ post.date | date_to_string }}</small> -->
        </li>
      </a>
      {% endfor %}
    </ul>
    {% endfor %}
  </div>
</div>
