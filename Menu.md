---
layout: page
title: Menu
---

{% for post in site.posts %}
  * {{ post.date | date_to_string }} &mdash; [ {{ post.title }} ]({{ site.baseurl }}{{ post.url }})
{% endfor %}
