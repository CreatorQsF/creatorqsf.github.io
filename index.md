---
layout: default
title: Hello
---

## Articles

<ul class="post-list">
{% for post in site.posts %}
<li>
<ul>
	<li><a href="{{ post.url }}">{{ post.title }}</a></li>
	<li><p>{{ post.date | date:"%Y年%m月%d日" }}</p></li>
</ul>
</li>
{% endfor %}
</ul>

***

## Pages

- [About](/about.html)
