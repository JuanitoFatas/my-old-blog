---
layout: page
title: "簡單學Scheme"
date: 2011-12-11 01:26
comments: false
sharing: true
footer: false
---
<div id="blog-archives">
{% for post in site.categories["簡單學Scheme"] %}
{% capture this_year %}{{ post.date | date: "%Y" }}{% endcapture %}
{% unless year == this_year %}
  {% assign year = this_year %}
  <h2>{{ year }}</h2>
{% endunless %}
<article>
  {% include category_post.html %}
</article>
{% endfor %}
</div>