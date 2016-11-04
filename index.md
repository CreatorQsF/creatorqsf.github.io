---
layout: default
title: Hello
---

## Articles

<ul class="post-list">
{% for post in site.posts %}
	<li>
	  <p><a href="{{ post.url }}">{{ post.title }}</a></p>
	  <p class="pub-date">{{ post.date | date:"%Y·%m·%d" }}</p>
    <hr>
	</li>
{% endfor %}
</ul>

***

## Pages

- [About](/about.html)
