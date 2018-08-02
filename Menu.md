---
layout: page
title: Menu
---

{% for post in site.posts %}
  * {{ post.date | date_to_string }} &mdash; [ {{ site.baseurl }}{{ post.title }} ]({{ post.url }})
{% endfor %}
